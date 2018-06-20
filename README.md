# OSARS
Open Source Automated Radio Station







MSP Waves  Broadcasting
IT/Ops
June 2018

# Software Requirement Specification (SRS)
## Open Source Automated Radio Station IT and Operations Management Solution
### Deliverable # 1:  Automated IT Solution OSAR
#### June  2018




# 1. INTRODUCTION

## 1.1 Purpose of this Document
The purpose of this document is to specify requirements for a software solution to replace MSP Waves’s current server hosted Master OBS (MOBS) solution, with an automated, low cost command line management system. The team also wishes this document to become part of our blue print for an Open Source Automated Radio Station that will allow anyone to incorporate a low cost community radio station solution.




## 1.2 Scope of the Development Project 
- The development of a stand-alone, automated software solution for managing stream capture, encoding and sending of one or more rtmp stream sources and their broadcast to one or more rtmp destinations and thus eliminate the use of the MOBS server hosted solution currently employed.
- The solution must include confirmation/status messages to alert IT and Operations of any corrective actions.

## 1.3 Limitations
- This part of the solution does not necessarily include a GUI, but it must provide an easy to manage control system that allows non-developers to manage the solution.


# 2.  GENERAL DESCRIPTION

NOTE: This section gives an “executive overview” and is very client-oriented.

## 2.1 Glossary (Definitions, Acronyms, and Abbreviations)
CRON: Unix based job scheduler
MOBS: Master Open Broadcast System
MSP: Minnow Support Project minnowsupportproject.org
MSPW: MSP Waves, the station name
OBS Open Broadcaster Software 
OSAR: Open Source Automated Radio 
rtmp: A stream protocol for audio and video broadcasts

  

## 2.2 User Characteristics

This section considers the needs of the anticipated users. List critical characteristics of the system’s human interfaces based on the anticipated users’ characteristics. “Who will use the system”?
The MSP Waves Ops team is a voluntary organization. Due to its nature, knowledgable and reliable staff is not available in abundance. The IT/OPS team requires a automated radio management solution that:

1) Reduces MSP Waves’s server cost by eliminating the need for a resource intensive OBS solution
2) Reduces need for manual transitions from one program to another
3) Simplifies manual intervention by IT/OPS when down and upstreams fail due to user error or technical problems, such as encoding errors, loss of internet by sender, etc.
4) Delivers status and error messages that can be used for error correction and/or manual intervention
5) Is scalable to potentially allow the implementation of additional radio stations/channels to deliver subject related programming.

## 2.3 Product Perspective

    • The solution must be able to accept rtmp streams from any system that delivers such streams.
    • The solution must deliver rtmp streams to any system that accepts such streams
    • The solution must be configurable in terms of
    • - multiple and simultaneous senders
    • - multiple and simultaneous recipients
    • - routing of captured streams to one or more recipients based on pre-defined categories

    • If the product is part of a larger product, then identify its interface to the other products.
    • If the product uses existing hardware, describe the hardware.
    • Any other relevant information.


## 2.4 Overview of Functional Requirements

A short description of the functions to be performed by the software, i.e. what the product should do.  This description must be in a form understandable to users, operators, and clients.  The detailed requirements specifications are left to Section 3.2 in this SRS.  Number the Functional Requirements in a systematic manner so the team can refer to them in Section 3.2 of the SRS, in the SDD, and in the testing documents. This section should not be design-oriented, a common mistake.     

(1) DJs produce live audio and video content which they deliver via rtmp audio/video stream using a DJ hosted software solution, which in most cases is open source OBS (Open Broadcast Software) for the purpose of that stream being 
(2) captured via an NGINX engine,
(3) scheduled  via CRON or similar, and
transmitted by MSPW via (2) to its
(5) audience on mspwaves.com/listen, dlive.io, an MSPW mobile radio application as well as non MSP streaming outlets.

During non-live air-times,
(6) Steemix, a playlist of categorized music performances by Steemians is transmitted to provide a 24x7 listening experience for the audience.


## 2.5 General Constraints and Assumptions
 
	OSAR should not be require a resource intensive hosting solution, but should be able to be hosted off of a virtual Linux machine with minimum (?) requirements. It may also be hosted on a shared or dedicated Linux machine. (Spedify hardware limitations or requirements, the amount of memory available, etc.) 

An IT and Operations team will monitor automated program transition, confirm to the DJ that their stream has been captured 30 minutes before DJ goes live, and perform an audio/video quality check to guide the talent to achieve acceptable broadcast and vide settings where necessary.

The IT Operations team will initiate/maintain the distribution of the stream to its intended destinations. 

The MSPW Ops team is monitoring any live stream for its reliability and quality. In the event of a technical failure on either DJ or MSPW side, the IT/Ops team will immediately switch to alternative programming to avoid dead air and communicate in discord audience chat progress of the fix, while working on the technical solution to restore live programming. This takes place in real-time with no delay. 

A DJ should at a minimum have a 1mbps upstream with the following min. encoding and bitrate settings: 200 VBR, 128 kbps audio, H.264…

It is not recommended to stream via WIFI where cabled ethernet connections are available, due    environmental instabilities in WIFI connections.

Constraints: This SRS does not discuss streaming to MSP/PAL Discord audio.

## 2.6 User View of Product Use

	The initial version of the product is command-line with no GUI. However, a messaging system for status and error should be implemented and displayed on screen accordingly. 

Access to the solution to the MSPW team is provided through SSH or RDP.

NOTE: Technical information needed to design the software 

# Requirements
## 3.1 Interface Requirements
## 3.1.1 User Interface
The user interface will be an ssh terminal window or an JAVA capable browser for RDP connections.
	
### 3.1.2 Hardware Interface
	A work station connected to the internet plus mouse and mousepad.

### 3.1.3 Software Interface
Java-capable web browser with access to the internet, the Java Development Kit (JDK) from Sun Microsystems or Integrated Development Environment (IDE), an ssh capable terminal, and a text editor.

### 3.1.4 Communication Interfaces
Internet access
VLC for audio/video checks

## 3.2 Detailed Description of Functional Requirements

###	3.2.1 Template for describing functional requirements
This lists the exact template your SRS will apply in describing each of the functional components that were identified in Section 2.4.  This section should have (for each requirement) at least the following:

##### (1)  DJ Live Show Content Provider
	• Content provision by DJ via OBS or similar
• Inputs: Video codec/settings: ; in what form/format will  inputs arrive; from what sources input will be, derived, legal domains of each input element
• Streaming/broadcasting with zero dropped network or encoding frames, status green at all times. Should dropped network frames occur, check if it is a WIFI issue, a router issue, and ISP issue. . Should it be an encoding issue, check settings guidelines. Should the stream not connect at all, liase with a member of the MSPW Ops team.
• The DJ will produce a rtmp stream with a personal key unique to that DJ.

##### (2)  NGINX
• Purpose / description of the NGINX HLS stream engine go here. Incorporate scaleability, multi-platform, multi-destination streaming where applicable.
• Inputs: which inputs; in what form/format will  inputs arrive; from what sources input will be
 	derived, legal domains of each input element
• processing: describes the outcome rather than the implementation; include any validity 

**inputs:**
Ngnix+rtmp
icecast+liquidsoap+azurecast (steemix audio)
OBS ($show key source)
ffmpeg+ffprobe (encode and detect media)
gstreamer (allows unique overlays with text, images, and http feed capibilities added to audio stream)
CRON (3) but potentially use schedule api instead of CRON (3) ? A pre-dev conference with interested developers should be held prior to dev, so as to agree on the architecture.

**outputs:**
nginx config:
catch/push rtmp $show key (all OBS show streams are captured and published with the same name)
catch/push rtmp `live`key; exec ffmpeg for distrubution:
-dlive (disabled and manually ran until we stream there 24/7)
-twitch
-icecast 320kbps `live320` mount
-icecast 96kbps `live96` mount
-hls native resolution
-hls 720p
-hls 360p
-rtmp 720p
-rtmp 360p

These outputs must be soft-configurable and must be able to be switched on the fly while live.

##### (3) CRON
• Purpose / description of the CRON scheduler goes here. If/then statements included, so an UML diagram can be drawn based on the statements.
• Inputs: which inputs; in what form/format will  inputs arrive; from what sources input will be
 	derived, legal domains of each input element
• processing: describes the outcome rather than the implementation; include any validity
- Start: During non-live shows: Initiate (6) Steemix Backfill
- Is Live show scheduled?
	No → Continue Steemix Transmission
	Yes → Does DJ Live Stream exist? Yes → Capture → Goto (4) Transmit
	No → Does Replay Exist? Yes → Play Replay. If No → Continue Live Stream

**Input/output**
*Default Operation:*
`steemix` rtmp stream key is always on, even when not pushed live.
*Delivery Flow:*
gstreamer → icecast audio stream + video overlay> push to rtmp `live` key (in other words: SteeMix+gif+text_overlay=backfill video feed)

*Live Show Scheduler:*
Show Based Triggers- `$show` will correlate with show OBS host steem name
- 2 mins before scheduled $show time, detect $show hosts stream key (ffprobe)
	- if no stream is detected, gstreamer mp4 $show archive on loop with "replay" text to rtmp `live` key exactly on the hour
		- if no $show archive is available, failover to Default Operation
		- if $show key appears during time slot, 
	- if stream is detected, ffmpeg $show rtmp key to `live` key exactly on the hour
		- if $show connection drops during show, switch to Default Operation until $show stream re-appears

**Override**
- if $override stream key detected, ffmpeg to `live`, ignoring timed triggers until stream disconnects

##### (5) AUDIENCE

This list must be configurable. It must not be hard-coded. Any destination can be turned on/off even during live stream.
- Dlive
- MSPwaves.com/listen (html5)
- Icecast
- TuneIn
- …

A short description of the functions to be performed by the software, i.e. what the product should do.  This description must be in a form understandable to users, operators, and clients.  The detailed requirements specifications are left to Section 3.2 in this SRS.  Number the Functional Requirements in a systematic manner so your team can refer to them in Section 3.2 of the SRS, in the SDD, and in the testing documents. This section should not be design-oriented, a common mistake.     


##### (6) STEEMIX

Steemix is our non-live backfill content which is delivered via Azuracast.com. It is our “Always-on” Default broadcast on MSPW.  Azuracast delivers a configurable playlist, which incorporates webhooks to display a Now Played notification via webhooks, which must be part of the Steemix video overlay. These webhooks should automatically be enabled when Steemix is actively streaming live and disabled during live or replay programming.

Although Steemix is ‘Always-On’, its live status is determined by (3) CRON

	
### 3.2.2 Data Dictionary

		Data dictionary supplies information such as data item, data type, how data is used.

## 3.3 Non-Functional requirements

Issues such as number of connections to the system, number of simultaneous users, response time, number of files, size of files and tables, number of files, size of files and tables, number of transactions per interval, security, and performance issues.


# 4. Object Oriented Analysis (OOA) -UML (to be developed based on each  Use Case UC)

## 4.1. For OOA, Complete the following:

### 4.1.1 Draw use case diagram. (Not sure which format UML/SDL or simple flow chart as in Illustration1) We may not have to be as specific, depending on developers requirements. We need to talk to people like Jedigeiss and/or kodaxx who can give us guidance.
### 4.1.2 Describe most Use Cases (the more dynamic and interesting ones) as shown in the example below:

Use Case Name: 
Use Case Number: UC01
Authors: r0nd0n/globocop
Actors: DJ (Host), Live show content provider
Overview: This use case captures the process of capturing and scheduling the live performance of a DJ
References: .
Related Use Cases: UCxx
Typical Flow Description: (include precondition & post-condition)
Alternative Flow Description: (include precondition & post-condition)

### 4.1.3 List potential / analysis classes based on the problem statement and use cases.

    • Provide clean drawings of your models. 
    • Include explanatory text as needed. 

# 5. Special remarks or comments

# 6. References or resources used
