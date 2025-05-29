# wavetable-synth-tips
Making the Windows Synth sound good

## What?
You've probably heard it. Those cheesy instruments associated with playing MIDI files on Windows. The so-called Microsoft GS Wavetable Synth or MSGS for short. The sound set's copyright dates back to 1996, so no wonder it sounds bad in 2025. For some, it may be nostalgic or iconic, being used in games like Doom, but for most, these instruments sound lifeless and artificial. But now, almost 30 years later, I've found a way to make it sound better. A LOT better. And I'm gonna tell you how. Maybe it has been discovered before, but I couldn't find any info on it.

## Why?
Nowadays there are way better alternatives, mostly using soundfonts, like:
- FluidSynth
- CoolSoft Virtual MIDI Synth (drop-in replacement for MSGS)
- SpessaSynth (by me ;-)

So one might ask: what's the point of making the stock windows synth sound good when there are better alternatives?
That's a very good question!

My answer to that is:

> Science isn't about *why* - it's about *why not*. *Why* is so much of our science dangerous? Why not *marry* safe science if you love it so much? In fact, why not invent a special safety door that won't hit you in the butt on the way out, because *you are fired!* Not you, test subject. You're doing fine. Yes, *you*. Box. Your stuff. Out the front door. Parking lot. Car. Goodbye.
> 
> ~ Cave Johnson, 2011

## How?
So, the infamous gm.dls sits in `C:\windows\System32\drivers\`. Once you remove it, the synth won't play sound. So one might think that you can just drop in a different DLS file and expect it to work. I tried that, but it doesn't. Upon inspecting the gm.dls file, there's a proprietary `msyn` chunk in it, presumably to prevent exactly what we're trying to achieve.

### Microsoft DirectMusic Producer
So back in late 90's and early 2000's, the MIDI was at it's peak, including the popularity of user-defined banks with cards such as the SoundBlaster AWE32. MIDI Manufacturer's Association along with Microsoft also had their take at this custom soundbank format, so this is how DLS was born.
It wasn't a big success, given how SF2 files are still created and used, yet I've yet to find a proper DLS synthesizer and editor.
Anyway, in 2000s MS released DirectMusic Producer. In short, it allowed users to create complex Musical arrangements including MIDI sequences with custom DLS files and even WAV files as vocals.

### Alright, enough with the backstory, how to make it sound good?
So the DM Producer uses the MSGS wavetable synth as well. But:
- It allows reverb effect
- It allows custom sample rate

And most importantly: it doesn't verify the `msyn` chunk!

### Step by step

1. Make sure that you're on a 64-bit system. This is important
2. Make sure that you're on Windows (duh)
3. Grab DirectMusic Producer from *somewhere*
4. Get your SF2/DLS file of choice (I recommend LiveHQ Natural SoundFont GM.sf2)
5. If it's an SF2, convert it to DLS using SpessaSynth (load -> load any demo song -> Save Audio -> DLS)
6. rename the file to `GM.DLS` (has to be all caps)
7. put the file in `C:\windows\SysWoW64\drivers\`, replacing the existing file if necessary (I recommend renaming the original to avoid losing it first)
8. Open DirectMusic Producer
9. In the top left corner there's a MIDI port icon, click it.
10. Set number of Voices to 999
11. Set sample rate to 44,1kHz or higher
12. Make sure that "Microsoft Synthesizer" is selected
13. Create a new project 
14. Right click, import file as
15. import a MIDI of your choice.
16. Play it. Voila! 
17. If the reverb is too much, in the top left corner there's a selector that allows you to disable it.
