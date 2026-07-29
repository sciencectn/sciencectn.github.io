
I remember waking up one morning and reading this headline: ["California's AB 1043 could regulate every Linux command."](https://shujisado.org/2026/03/02/californias-ab-1043-could-regulate-every-linux-command/) It seemed like clickbait. I thought California was good at regulating technology. Why would they do this?

Then I read the bill. 

Through threats of huge fines, California's plan was to forcibly enlist all OS or app developers to be part of its age assurance scheme. In this scheme, the operating system would be required to collect your age, and *all applications* required to request the age. Not the exact age, but an age "signal" with downgraded precision to protect privacy. This would give the apps "actual knowledge" of the user's age and remove companies' favorite liability shield of not knowing that their users are minors. This, in turn, would trigger liability for other laws, like California's upcoming under-16 social media ban. 

(diagram). 

Meta, Apple, Microsoft, et al can survive this liability. But for open source developers, it is financially ruinous. The bill hits developers with a fine of $2500 - $7500 "per affected child" if they fail to comply. And that's "affected", not "harmed". If a kid finds your app on GitHub, and California gets wind of it, you're on the hook. 

(i just took it down so i won't get fined)

This bill made me really angry for a number of reasons. 
- Open source software brought me great joy and learnings as a child. I owe a lot of my embedded systems knowledge to Adafruit Industries. And now the state was nerfing something that brings great educational joy to children in the name of...protecting the children? 
- Open source feels like one of the few escape hatches we have against enshittification. Big Tech is moving toward locked-down devices, DRM, devices that you can't repair. For example, your Kindle books aren't really yours, and if you try to move your book off the Kindle and on to another non-Amazon device, you're committing a felony. Apple doesn't let you download any iOS app unless it comes from its app store and they take a 30% cut (Epic Games fought like hell against this). Google nerfs GrapheneOS, a competing Android distribution, by downgrading the functionality of its apps. But with open source apps, the gate is wide open. You can draw diagrams with [draw.io](https://app.diagrams.net/) or [Excalidraw](https://excalidraw.com/) and avoid getting locked in to a LucidChart or Figma subscription. [yt-dlp](https://github.com/yt-dlp/yt-dlp) lets you take YouTube videos offline for safekeeping or analysis. [uBlock Origin](https://github.com/gorhill/ublock) blocks ads. [Privacy Badger](https://privacybadger.org/) protects you from tracking cookies (as opposed to useless permission banners, thanks EU). Big Tech gouges you with ads and fee hikes, but open source is yours to use as you please. 
- I'm struggling massively with burnout right now and one contributing factor is the feeling of powerlessness against increasingly oligarchic tech companies. Many of my peers in the tech industry also feel this way: they're not getting jobs, they feel stuck in the job that they have, and they're mentally checked out and basically "sever" themselves when they go to work. It's terrible for our mental health (and our kids!). Cracking down on open source widens Big Tech's moat even more by hurting competition and home-grown alternatives. And the reason is to improve kids' mental health? Fuuuck you!

I penned a [letter](/letter) to my reps to share my feelings. I thought that'd be the end of it but a really friendly staffer with Senator Roger Niello's office told me (a) there was an amendment bill (AB 1856) in play that we could work with and (b) you can submit position letters to tell the legislature how you feel about legislation (anyone can do it!) and (c) there are public hearings for which you can show up in person so the lawmakers actually hear you! 

So, on April 21st, I attended the hearing with the Assembly Privacy and Consumer Protection (P&CP) Committee. It turned out the bill's author, Buffy Wicks, did get the memo about damage to open source and mentioned it in her opening statement. 

When it came time for public comment, I voiced my 10 seconds of fame and thanked Wicks for mentioning us. Unknown to me, another OS developer @snow independently had the same idea that I had. He's behind me in the hearing video. Thanks to his persistence, we both got a meeting with Wicks's staff and explained the issues with their bill in person. 

But a week before the meeting, they expanded the scope of the bill even more. Not content with regulating apps and operating systems, they expanded it to all *websites*. That is, if you were under 13, your browser would be required to share this fact with every website that asked.

I didn't really think much of it at the time. I was focused on protecting open source apps and operating systems. I figured websites would just be a necessary casualty. You can't win every battle. 

Our meeting with Wicks's staffers seemed productive. This is what we discussed:
- The DAAA regulates all "applications" but @snow mentioned that most open source applications are completely harmless. He mentioned a compiler as an example, and explained to the staffers that, no, a compiler doesn't geolocate you and, no, it doesn't track you and share your data with Big Tech. Wicks's staff was particularly concerned about the profiling and surveillance of children (I am too).
- The staffers weren't that familiar with open source, so I explained it like this: for the general non-technical public, open source software is like the plumbing in your house. You only learn about it when it doesn't work. For example, in the 2017 Equifax hack which exposed personal data on millions of Americans, a major cause was them not updating an open source application (Apache). 
- I believe @snow mentioned that open source is often created by volunteers, hobbyists, and nonprofits without a lot of resources. He mentioned maintainer burnout and how the DAAA would burn out the maintainers even more. This has major cybersecurity implications. It's like an overworked stressed-out locksmith trying to keep a building secure suddenly getting slapped with more regulations about child-proofing the building. 

The meeting came and went and that website age-gating really started to gnaw at me. So far, our efforts had not created any tangible results. No open-source carveout amendment, no promises in writing from staffers. Only a bill with amendments to expand the age gating even *more*, to websites. 

I noticed that my Assemblymember, Josh Hoover, was also a member on the P&CP committee. So far, Hoover's staff had not responded to my letter (Niello's staff did). I noticed that he was having a campaign event so I decided to show up to get his attention. I told him that AB 1856 "scared the crap out of me" and it was supposed to reign in Big Tech but it would actually hurt independent developers and small businesses. 

(picture)

For the record, I'm very much an introvert and I hated doing this. But it worked, and the next day his staff got back to me and got all the details on the overbroad DAAA that Hoover co-sponsored. 

Then on May 14th, the unexpected happened: Hoover actually abstained from voting on it at the Assembly Appropriations Committee. A staffer confirmed that the abstention was for this specific bill and not just abstaining en-masse. Did I do that? Who knows. I don't think I have that much influence. 

Four days later, we got our FOSS exemption. About two tweets worth of text sparing thousands of developers from unnecessary pain: 

> _(2) “Application” does not include software components that are not themselves offered to 
> consumers as a stand-alone executable application through a covered application store._
> 
> _(2) “Operating system provider” does not mean a person or entity that distributes an operating system or application under license terms that permit a recipient to copy, redistribute, and modify the software._

I emailed the staffers and thanked them and suggested some [improvements](https://mastodon.world/@wallfacer/116652445797672294). I felt that the "Application" carveout could be stronger: the carveout should be based on whether an app is open source or not, as opposed to it being in an app store. What if the CA AG decides that a package manager is an app store? What about open source apps that end up in app stores (like Python in Windows App Store)? 

In addition, I felt that the operating system carveout might let Google loophole themselves out of Android since it's based on open source software but they use hardware restrictions via the Google Play Integrity API to [nerf custom builds of Android](https://grapheneos.social/@GrapheneOS/116550899908879585). This is essentially [Tivoization](https://en.wikipedia.org/wiki/Tivoization). 

The staffers didn't reply to me. Oh well. 

A few days after that, I met with Rin from EFF and Molly (formerly with EFF) to compare notes on advocacy, since we'd both been fighting the same bill. Here they convinced me just how damaging the website age gating requirement was and that they were mainly focused on that as opposed to the FOSS exemption. As Molly put it: [One step forward, two steps back](https://www.eff.org/deeplinks/2026/05/one-step-forward-two-steps-back-cas-ab-1856-exempts-open-source-expands-age-gating). 

The bill was headed to the Senate equivalent of P&CP so I sent them a position letter with this diagram to make it obvious how bad the website signaling was: 

(I'm under 13!)

A few weeks later, on July 1st, they removed the website signaling requirement. They worked around it by considering the age that an app receives to apply "across all platforms of an application, including an internet website \[made by the same developer\]". For example, if the your iPhone sends the Facebook App your age, now that same age will apply on facebook.com. 

All in all, not bad for my first engagement with a bill. We got our FOSS exemption and they backed down on a privacy-damaging age signal. I don't know how much influence @snow and I had. They won't tell you. This was a huge team effort of multiple groups fighting from different angles:
- EFF, in particular Molly and Rin. 
- Lots of independent developers who sent letters to their reps or got the word out, like @snow, [@bzdev](https://mastodon.world/@bzdev@fosstodon.org/116644723679402377), agelesslinux.com, the Lunduke Journal, Louis Rossman (todo did he?)
- Oakland Privacy. Turns out they lobbied not just on a privacy basis, but for the FOSS exclusion too. They're in Buffy Wicks's district so they're well positioned to fight this. 

