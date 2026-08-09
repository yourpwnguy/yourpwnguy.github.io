---
title: "Reverse Engineering My Way Back Into 010 Editor"
description: "The license expired mid-development. I opened IDA. You can probably guess what happened next... >ᴗ< !!"
date: 2026-08-08
categories: [Reverse Engineering, Fuck Around & Reverse Engineer]
tags: [Reverse Engineering, Patching, Licensing, IDA Pro]
# image:
  # path: assets/temp/windows-internals/concepts/part2-concepts.png
---

## I Just Wanted to Inspect an ELF

So as always, I was working on some random shit, this time it's Strix ( [Strix](https://github.com/yourpwnguy/strix), shameless plug ), my replacement for readelf but, y'know, colored and actually fucking pretty because apparently I can't leave anything alone. 

I was doing some development on it and needed to inspect a bunch of ELF structures, so obviously I fired up 010 Editor because that shit is basically crack for anyone who likes staring at binary structures. I'm sitting there happily poking around the ELF, checking structures, doing my usual thing, everything is chill, life is good.

## And Then the License Expired

And then suddenly... **BOOM**, 010 Editor hits me with the fucking license expiration.

![010editor License Expired](/assets/temp/reverse-engineering/fuck_around_and_reverse_engineer/010editor_license_expired.png)
Now, apparently these mfs give you a **30-day trial**. Thirty days. That's it. And mine had decided that today was the day it was going to fucking die. I just sat there looking at the popup like, bro... seriously? I'm literally trying to inspect an ELF, why are we doing this right now? And yeah, I'm broke, so buying a license wasn't exactly sitting at the top of my financial master plan. So I accepted my fate for approximately **three seconds**.

Because then I remembered something...

I have **IDA**.

And that's when the intrusive thoughts won.

## Fine. I'll Open IDA.

Instead of closing 010 Editor like a normal functioning member of society, I opened IDA and started hunting for the license check. No plan, no idea where the fuck to start, just me, IDA, and way too much confidence.

**WHERE THE FUCK ARE YOU, IDAAAAAA-SAAAAAAN?**

At this point, Strix had officially been put on hold. The ELF wasn't getting inspected anymore. The actual target was now the thing preventing me from inspecting the ELF in the first place.

And honestly?

I was having way more fun.
