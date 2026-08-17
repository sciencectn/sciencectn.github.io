---
title: My crash course in lobbying for open source
layout: post
date: 2026-08-15
permalink: daaa
---



One morning, this headline greeted me: ["California's AB 1043 could regulate every Linux command."](https://shujisado.org/2026/03/02/californias-ab-1043-could-regulate-every-linux-command/) It seemed like clickbait. I thought California was good at regulating technology. Why would they do this?

Then I read the law, called the *Digital Age Assurance Act* (DAAA). Here's what it requires:
- The operating system asks you for your age on account setup. 
- The OS stores your age.
- All applications, when launched, ask the OS for your age. 
- The OS provides an age "signal", a rough estimate of your age with downgraded precision to protect privacy. 

Once the application receives the age signal, the app now has "actual knowledge" of the user's age, and the developer who created the app is now liable for any other age-related regulation out there, such as California's upcoming under-16 social media ban ([AB 1709](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202520260AB1709)) or their upcoming chatbot regulations ([AB 2023](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202520260AB2023)). OS developers are liable for creating the age signaling mechanism. There was no distinction between commercial and open source software. 

![](assets/daaa-diagram-initial.png)

Meta, Apple, Microsoft, et al can survive this liability. But for open source developers, it is financially ruinous. The bill hits developers with a fine of $2500 - $7500 "per affected child" if they fail to comply. And that's "affected", not "harmed". If a kid finds your app on GitHub, if you didn't request the age signal, if you didn't follow the patchwork of protect-the-children regulations emerging, you are liable. This would have a predictable effect on the open source community. 

![](assets/dont-get-fined.jpg)

(It's worth noting that this bill might be weakened under *Bernstein v. US* precedent as compelled speech. But that's not a guarantee, the courts haven't decided yet, and until they do, [a corrupt attorney general](https://www.thebarbedwire.com/ken-paxton-scandal-timeline/) can still [ruin your day](https://www.chron.com/culture/article/texas-bluesky-age-verification-22328414.php) to score political points for "protecting the children".)

This bill made me angry for a number of reasons. 
- You can't just coerce a technology standard into existence by threatening developers with fines. One type of tech standard, called an [RFC](https://www.ietf.org/process/rfcs/), literally stands for "Request for Comment". You know, like, *requesting comments and feedback before you introduce some major change to every application and operating system.* When politicians feel stupid enough to ignore the experts and ram through tech-by-fiat anyway, we get idiocy like the CALEA wiretapping system, which has been [hacked by Chinese state actors](https://www.wsj.com/tech/cybersecurity/u-s-wiretap-systems-targeted-in-china-linked-hack-327fc63b) to spy on Americans. 
- Open source software brought me great joy and learnings as a child. I owe a lot of my embedded systems knowledge to Adafruit Industries. And now the state was nerfing something that brings great educational joy to children in the name of...protecting the children? 
- Open source feels like one of the few escape hatches we have against enshittification. Big Tech doesn't want you to own your own stuff in the name of profits. For example, your Kindle books aren't really yours, and if you try to move your book off the Kindle and on to another non-Amazon device, you're committing a felony under DMCA § 1201. Apple doesn't let you download any iOS app unless it comes from its app store and they take a 30% fee cut (Epic Games fought like hell against this). Google [nerfs GrapheneOS](https://grapheneos.social/@GrapheneOS/116550899908879585), a competing Android distribution, by downgrading the functionality of its apps. But with open source apps, the gate is wide open. You can draw diagrams with [draw.io](https://app.diagrams.net/) or [Excalidraw](https://excalidraw.com/) and avoid getting locked into a LucidChart or Figma subscription. [yt-dlp](https://github.com/yt-dlp/yt-dlp) lets you take YouTube videos offline for safekeeping or analysis. [uBlock Origin](https://github.com/gorhill/ublock) blocks ads. [Privacy Badger](https://privacybadger.org/) protects you from tracking cookies (as opposed to useless permission banners, thanks EU). Big Tech gouges you with ads and fee hikes, but open source is yours to use as you please. 
- I'm massively struggling with burnout right now and one contributing factor is the feeling of powerlessness against increasingly oligarchic tech companies. Many of my peers in the tech industry also feel this way: they're not getting jobs, they feel stuck in the job that they have, and they're mentally checked out and basically "[sever](https://severance-tv.fandom.com/wiki/Severance_Procedure)" themselves when they go to work. It's terrible for our mental health (and our kids!). Cracking down on open source widens Big Tech's moat even more by hurting competition and home-grown alternatives. And the reason is to improve kids' mental health? 🤬🤬🤬🤬

I penned a [letter](/letter) to my reps to share my feelings. I thought that'd be the end of it, until a friendly staffer with Senator Roger Niello's office told me:
- there was an amendment bill (AB 1856) in play that would modify the DAAA, 
- you can submit position letters to the legislature to tell them how you feel about bills,
- there are public hearings you can attend so the lawmakers can see you are a real person with thoughts on their legislation.

So, on April 21st, I attended the hearing with the Assembly Privacy and Consumer Protection (P&CP) Committee and [voiced my opposition](https://calmatters.digitaldemocracy.org/hearings/279266#t=1092&f=7b87059bf53b0b4642282c875e6bd43c). It turned out the bill's author, Buffy Wicks, did get the memo about damage to open source and mentioned it in her opening statement. 

![me standing in front of a microphone to voice my opposition to legislators](assets/p-cp-hearing.jpg)

Another developer, the guy standing behind me ([@snow](https://mastodon.world/@snow@teardrop.net)), independently had the same idea that I had to show up and voice opposition. Thanks to his persistence, we secured a meeting with Wicks's staff and explained the issues with their bill:
- @snow mentioned that most open source applications are completely harmless. He mentioned a compiler as an example, and explained to the staffers that, no, a compiler doesn't geolocate you and, no, it doesn't track you and share your data with Big Tech. Wicks's staff was particularly concerned about the profiling and surveillance of children (I am too).
- The staffers weren't familiar with open source, so I explained it like this: for the general non-technical public, open source software is like the plumbing in your house. You only learn about it when it doesn't work. For example, in the 2017 Equifax hack which exposed personal data on millions of Americans, a major cause was them not updating open source software (Apache Struts). 
- @snow mentioned that open source is often created by volunteers, hobbyists, and nonprofits without a lot of resources. He mentioned maintainer burnout and how the DAAA would burn out the maintainers even more. This has major [cybersecurity implications](https://www.youtube.com/watch?v=aoag03mSuXQ). It's like an overworked stressed-out locksmith trying to keep a building secure suddenly getting slapped with more regulations about child-proofing the building. 
- We told them about [SB26-051](https://leg.colorado.gov/bills/SB26-051), Colorado's similar bill, which had very strong open source carveouts. 

The meeting was pleasant. We sent them some suggested amendments. And then, silence. I learned this is the way of things with legislative activism. A lot of screaming into the void and hoping the void heard you. 

I later found out that a week before the meeting, they [expanded the scope](https://legiscan.com/CA/text/AB1856/id/3425439) of the bill even more. Not content with regulating apps and operating systems, they expanded it to all *websites*. That is, if you were under 13, your browser would be required to share this fact with every website that asked.

![](assets/daaa-websites.png)

This seemed stupid and ripe for abuse. But I was focused on protecting open source apps and operating systems. I figured websites would just be a necessary casualty. You can't win every battle. 

Days went by and we had heard nothing. The browser age signal expansion was starting to bother me. 

I noticed that my Assemblymember, Josh Hoover, was also a member on the Privacy and Consumer Protection committee. I also noticed that Hoover's staff never returned my calls or emails about AB 1856. By a stroke of luck, I noticed he was having a campaign event and I decided to show up and tell him in person. I told him that AB 1856 scared the crap out of me and it was supposed to rein in Big Tech but it would actually hurt independent developers and small businesses. 

![](assets/activism%201.jpg)

For the record, I'm very much an introvert and I hated doing this. But it worked, and the next day his staff got back to me and I sent them all the details on how to fix the DAAA.

A week after I crashed the campaign event, the unexpected happened: Hoover actually abstained from voting on it at the Assembly Appropriations Committee. A staffer confirmed that the abstention was for this specific bill and not just abstaining en masse. Did I do that? Who knows. 

(Also, I want to credit Hoover here, I think he has actually done a way better job than other CA politicians at child-protection legislation. He's one of the few lawmakers who actually [listened to kids and co-authored a bill](https://edsource.org/2026/social-media-ai-mental-health/755990) with them. EFF endorsed this bill. I'll probably vote for Hoover in his reelection campaign).

Four days later, we got our open source [carveout](https://legiscan.com/CA/text/AB1856/id/3438064). Two tweets worth of text sparing thousands of developers from unnecessary pain: 

> _(2) “Application” does not include software components that are not themselves offered to 
> consumers as a stand-alone executable application through a covered application store._
> 
> _(2) “Operating system provider” does not mean a person or entity that distributes an operating system or application under license terms that permit a recipient to copy, redistribute, and modify the software._

With this amendment, only commercial operating systems would supply the signal and only to applications in an app store...
![](assets/daaa-diagram-commercial-os.png)

...while open source operating systems would be left alone. 
![](assets/daaa-diagram-foss-hacker.png)

I emailed the staffers and thanked them and suggested some [improvements](https://mastodon.world/@wallfacer/116652445797672294). I felt that the "Application" carveout could be stronger: the carveout should be based on whether an app is open source or not, as opposed to it being in an app store. What if the AG decides that a package manager like [homebrew](https://brew.sh/) is an app store? What about open source apps that end up in commercial app stores (like [Python in Windows App Store](https://apps.microsoft.com/detail/9pnrbtzxmb4z?hl=en-US&gl=US))?

I also felt that the operating system carveout might introduce a loophole that Google could abuse. The Android operating system is technically open source, but Google uses clever hardware restrictions built into Android phones via something called the Google Play Integrity API to [nerf custom builds of Android](https://grapheneos.social/@GrapheneOS/116550899908879585) like Graphene. Technically, you can "copy, redistribute, and modify" Android, but once you do, your apps get nerfed. This is a sneaky form of [Tivoization](https://en.wikipedia.org/wiki/Tivoization). 

The staffers didn't reply to me. Oh well. 

A few days after that, I met with [Rin](https://www.eff.org/about/staff/rindala-alajaji) & Molly from EFF to compare notes on advocacy, since we'd both been fighting the same bill. They were very concerned about the browser age signaling requirement and felt that we shouldn't celebrate the open source carveout yet. As Molly put it: [One step forward, two steps back](https://www.eff.org/deeplinks/2026/05/one-step-forward-two-steps-back-cas-ab-1856-exempts-open-source-expands-age-gating). 

The bill was headed to the Senate P&CP&DT Committee, so I sent them a position letter with that diagram above (I'm under 13!) to get my point across.

A few weeks later, on July 1st, lawmakers [removed the website signaling requirement](https://legiscan.com/CA/text/AB1856/id/3451963). They worked around it by considering the age that an app receives to apply "across all platforms of an application, including an internet website \[made by the same developer\]". For example, if your iPhone sends the Facebook App your age, that same age will apply on facebook.com. 

The bill is headed to the Senate now for a final vote.

All in all, not bad for my first engagement with a bill. We got our FOSS exemption and they backed down on a privacy-damaging age signal. I don't know how much influence @snow and I had. They won't tell us. This was a huge team effort of many individuals and organizations working together:
- [EFF](https://www.eff.org/), in particular Molly and Rin. EFF is awesome. I don't think the public knows what a hellscape we'd be living in without EFF. 
- [Oakland Privacy](https://oaklandprivacy.org/). I thought they were fighting this bill because of its disturbing implications for privacy, but it turns out they fought for the open source carveout too. They're in Buffy Wicks's district so they're well positioned to fight this. 
- [Carl Richell and System76](https://system76.com/blog/post/system76-on-age-verification), who helped get an open source carveout in Colorado's similar bill.  
- Lots of independent developers who sent letters to their reps or got the word out, like @snow, [@bzdev](https://mastodon.world/@bzdev@fosstodon.org/116644723679402377), [agelesslinux.org](https://agelesslinux.org/), the [Lunduke Journal](https://www.youtube.com/watch?v=Ie9-kgxKjIc), [Louis Rossmann](https://www.youtube.com/watch?v=wZonPM4aXFY), and many others. 

When I got into this, I told myself *I may have little influence, but if I say nothing, and this stupid bill passes, I'm gonna regret it for the rest of my life.*

I have no idea how much influence I had. I found the whole process of dealing with the legislature exhausting. But meeting other activists passionate about the same things made it worth it. 

I'm hoping by throwing this article out there, that it inspires more people to copy me and get involved. Hopefully more extroverted people who can comfortably crash town halls and campaign events.