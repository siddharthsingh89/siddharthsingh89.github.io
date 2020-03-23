---
layout: post
title: Technologies behind Video Streaming
description : videostreaming, dash, system design, prime, interview
---

#### How system like Amazon Prime serves its content?
There are many technologies involved.

#### Streaming

##### Dash( MPEG-Dash):  
Dynamic Adaptive Streaming over HTTP (DASH), also known as MPEG-DASH, is an adaptive bitrate streaming technique that enables high quality streaming of media content over the Internet delivered from conventional HTTP web server.

MPEG-DASH works by breaking the content into a sequence of small HTTP-based file segments, each segment containing a short interval of playback time of content that is potentially many hours in duration, such as a movie or the live broadcast of a sports event. The content is made available at a variety of different bit rates, i.e., alternative segments encoded at different bit rates covering aligned short intervals of playback time. While the content is being played back by an MPEG-DASH client, the client automatically selects from the alternatives the next segment to download and play based on current network conditions. The client automatically selects the segment with the highest bit rate possible that can be downloaded in time for playback without causing stalls or re-buffering events in the playback. Thus, an MPEG-DASH client can seamlessly adapt to changing network conditions and provide high quality playback with fewer stalls or re-buffering events.

DASH is an adaptive bitrate streaming technology where a multimedia file is partitioned into one or more segments and delivered to a client using HTTP.  A media presentation description (MPD) describes segment information (timing, URL, media characteristics like video resolution and bit rates), and can be organized in different ways such as SegmentList, SegmentTemplate, SegmentBase and SegmentTimeline, depending on the use case. Segments can contain any media data, however the specification provides specific guidance and formats for use with two types of containers: ISO base media file format (e.g. MP4 file format) or MPEG-2 Transport Stream.

Adaptive bitrate streaming is a technique used in streaming multimedia over computer networks. Today's adaptive streaming technologies are almost exclusively based on HTTP[1] and designed to work efficiently over large distributed HTTP networks such as the Internet.
It works by detecting a user's bandwidth and CPU capacity in real time and adjusting the quality of the media stream accordingly. [2] It requires the use of an encoder which can encode a single source media (video or audio) at multiple bit rates. The player client[3]switches between streaming the different encodings depending on available resources.[4] "The result: very little buffering, fast start time and a good experience for both high-end and low-end connections."[5]


#### Security
Prime uses Widevine DRM for security. Widevine was purchased by google in 2010. It is used in chrome and android browsers.
DRM is digital rights management.
It operates as an encryption scheme to securely distribute video content to consumer devices.
DRM technology has considerably matured since Hal’s answer from way back in 2012. Netflix uses the Widevine DRM on Android Phones (more details on Widevine DRM here). The System-on-Chip architecture is indeed the fundamental technology underlying secure streaming of premium video content.
Most mobile devices out there follow the ARM design architecture for their Systems-on-Chip ICs. The actual chip manufacturers, such as Qualcomm and MediaTek, license the ARM design and customize it as per market requirements.
Now, ARM has introduced a Trusted Execution Environment (TEE) as part of its instruction design. The TEE separates the secure components of the device from the non-secure components, making sure that untrusted apps do not get access to the trusted environment. This separation is at a hardware level. Along with the trusted hardware layer (called TrustZone), a Trusted Execution Environment requires:
A trusted boot process, to ensure that the OS has not been tampered with, and that only trusted softwares get access to the TrustZone.
Trusted OS
Secure apps
The usual use cases for the Trusted Execution Environment are the protection of authentication mechanisms - cryptography, content decryption keys, and Digital Rights Management licenses.
What this boils down to, for Netflix’s streaming on Android, is that Google, as part of Android OS, installs the Widevine Content Decryption Module in the TrustZone (trusted hardware layer). All video decryption, decoding and rendering occur in the Trusted environment. The video is rendered directly to the screen from this Trusted Execution Environment. This TEE-to-screen process ensures that at no point does any non-trusted app get access to either the premium content or to the content keys themselves.

#### Video Encoding

AWS Elemental MediaConvert is a file-based video processing service that provides scalable video processing for content owners and distributors with media libraries of any size. MediaConvert offers advanced features that enable premium content experiences, including:
professional broadcast codecs that support increased bit depth and HDR content creation
still graphic overlays
advanced audio
digital rights management (DRM)
closed captioning support
AWS Elemental MediaConvert offers support for various input formats and adaptive bitrate (ABR) packaging output formats for delivering high-quality content from a range of sources onto primary and multiscreen devices.

#### Ad Insertion

AWS Elemental MediaTailor is a scalable ad insertion service that runs in the AWS Cloud. With MediaTailor, you can serve targeted ads to viewers while maintaining broadcast quality in over-the-top (OTT) video applications.
AWS Elemental MediaTailor offers important advances over traditional ad-tracking systems: ads are better monetized, more consistent in video quality and resolution, and easier to manage across multi-platform environments. MediaTailor simplifies your ad workflow by allowing all IP-connected devices to render ads in the same way as other content. The service also offers advanced tracking of ad views, which further increases the monetization of content.
For live workflows, MediaTailor supports Apple HTTP Live Streaming (HLS) and MPEG Dynamic Adaptive Streaming over HTTP (DASH). For video on demand (VOD), MediaTailor supports HLS.


#### Video Packaging
AWS Elemental MediaTailor serves personalized content to viewers while maintaining broadcast quality-of-service in over-the-top (OTT) applications.
Here is the general AWS Elemental MediaTailor processing flow:
A player or content distribution network (CDN) such as Amazon CloudFront sends a request to MediaTailor for HLS or DASH content. The request contains parameters from the player that includes information about the viewer that is used for ad customization. The format of the request varies depending on whether you use server-side or client-side reporting to track how much of an ad the viewer watches.
For information about how the requests differ between the two reporting methods, see Ad Tracking Reporting in AWS Elemental MediaTailor. For information about configuring the ad targeting parameters, see Dynamic Ad Variables in AWS Elemental MediaTailor.
Based on the request, MediaTailor retrieves the content manifest and ad specifications as follows:
MediaTailor sends a manifest request to its origin server, typically AWS Elemental MediaPackage. The origin server returns a fully formed template manifest with ad markers, so that MediaTailor knows where to perform ad insertion or replacement.
MediaTailor sends a request that includes the viewer information to its ADS. The ADS chooses ads based on the viewer information and current ad campaigns. It returns the ad URLs in a VAST or VMAP response.
MediaTailor manipulates the manifest to include the URLs for the appropriate ads from the VAST or VMAP response. For the logic behind how ads are inserted, see Ad Behavior in AWS Elemental MediaTailor.
MediaTailor provides the fully customized manifest to the requesting CDN or player.
As playback progresses, either MediaTailor or the video player reports how much of an ad is played to the ADS ad tracking URL. For more information about ad reporting, see Ad Tracking Reporting in AWS Elemental MediaTailor. The player requests ad segments throughout content playback. When MediaTailor receives an ad segment request, if the ad is not already transcoded in a format that matches the video content, MediaTailor transcodes the ad. If an ad is not already transcoded, MediaTailor doesn't present it for playback at the first request.


#### CDN

Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment. CloudFront is integrated with AWS – both physical locations that are directly connected to the AWS global infrastructure, as well as other AWS services. CloudFront works seamlessly with services including AWS Shield for DDoS mitigation, Amazon S3, Elastic Load Balancing or Amazon EC2 as origins for your applications, and Lambda@Edge to run custom code closer to customers’ users and to customize the user experience.  You can get started with the Content Delivery Network in minutes, using the same AWS tools that you're already familiar with: APIs, AWS Management Console, AWS CloudFormation, CLIs, and SDKs. Amazon's CDN offers a simple, pay-as-you-go pricing model with no upfront fees or required long-term contracts, and support for the CDN is included in your existing AWS Support subscription.
