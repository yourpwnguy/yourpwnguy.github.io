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

So, the first thing I did was a string search. The plan was pretty simple: reverse our way backwards from anything related to the license until we eventually land on the routine actually handling the license check.

I searched for `"Evaluation Period Expired"`.

Well... technically, I only typed the first three characters because IDA immediately started showing me the string, so obviously I wasn't going to sit there typing the whole fucking thing like some NPC.

And there it was.

**Our first fucking lead**.

## Where the Fuck Is the License Check?

From the above image, you can see that we found the string we were looking for. So naturally, the next question was: where the fuck is this thing being used?

That's where X-refs come in.

I checked the cross-references to the specific label holding our `"Evaluation Period Expired"` string. If we're lucky, something in the license-checking logic should be referencing it.

And guess what? There was only **one** X-ref.

One.

That's exactly what we fucking wanted. So I followed it.

And this is where things started getting interesting.

The reference dropped us straight into a routine that looked suspicious as hell. So obviously, I opened IDA's decompiler because reading raw assembly for every single fucking instruction is a great way to turn your brain into mashed potatoes.

IDA gave us the decompiled view, and sitting right there was the routine name:

GetStatus

Now, I don't know about you, but a function called GetStatus sitting directly behind a string screaming **"Evaluation Period Expired"** is about as subtle as a fucking neon sign saying **"LOOK HERE, DUMBASS."**

We had a lead.

Now it was time to follow the fucking rabbit hole.
