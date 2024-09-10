+++
title = "Trying to automate saddlestitching"
date = 2024-09-03
weight = "20"
meta = "false"
+++

## Introduction

I only recently started to listen to the older issues of the [Acquired](https://www.acquired.fm/) podcast (can only recommend!). One of the episodes is about Hermès (watch the accent) and their affinity towards manufacturing instead of industrialized production. One of the key components is the saddlestitch, used for any leather goods they produce. To this day, saddlestitched goods are manufactured, as no machine lives up to the quality of a human.

Let's try to change that.

## What is the saddlestitch?

The saddlestitch is a method to handstitch two edges of a leather strip together. It is used to manufacture any leather good, from a simple pouch to a Birkin bag. The process is simple and can be summarized as follows:

1. Pre-stretch the leather strip
2. Pass the needle through the leather, from the back to the front
3. Pull the thread through the leather, from the front to the back

If you want to have a visual cue, I can highly recommend [this video](https://www.youtube.com/watch?v=jmDJFnejt3cs) on YouTube. For anybody who sewed in their life, you would be surprised that this includes a dual-needle approach. You would have to run one needle after another and check after passing both needles whether the thread is tight enough and only then move on to the next hole.

## How does it compare to "regular" stitching?

You can of course run needle by hand, yet most industrial sewing machines would run automatically based on a simple approach: You poke a hole whilst pushing the garn through it. At the bottom, you have a spool of the same garn which is covered by a rotating wheel. This wheel is special, as it is partly open to catch the garn coming from above. By interlacing the two garns and the needle from above going back up, you can easily stitch two pieces together. If this was too high-level, have a look at the following gif:

{{< figure src="/stitch.gif" class="mid"  caption="How your regular sewing machine works" >}}

As you can see, regular sewing machines do not have a dual-needle approach. They simply pass the same garn over another rather than interweaving the two garns on either side.

## Why saddlestitching is tough to automate

Hold on, you would say, why do not simply set up a regular sewing machine with two needles and run the same process? This is mainly due to two reasons:

- **Precision**: As with handstitching, a saddlestitch has to be mounted vertically to get all corners/angles and surfaces. This comes with the caveat that that you would have to set your needles vertically to the material, exposing you to potential large free play and wiggly stichtes along the seam. Plus, mounting two sweing machines might be tougher than you think.

- **Leather**: If you tried sewing any leather good (I tried with my gloves), you know what kind of needles are necessary to go through the material. Now imagine the power a machine and of course the mechanic to push a massive needle through without harming the leather. It's called *feeling* and the reason why humans are still better.

- **Coordination & Machinery**: You would have to coordinate two machines, one pushing the needle through and one pulling it out. This requires a lot of precision and coordination to set up from a mechanical perspective: Needles have to go in one after the other with a defined period in between, followed by a defined pull of the thread. As you see, this is rather cumbersome, especially if you are competing with a human and high quality standards.

Even my wildest imagination could not come up with a solution (flux1 btw):

{{< figure src="/flux.png" class="mid"  caption=":(" >}}


## Closing thoughts

This is of course a high-level overview and by no means an in-depth analysis. I simply wanted to dive deeper into why these topics might seem easy at the beggining but grow easily very complex, even on a 0 to 1 basis. Lastly, I still enjoy craftmanship and, although a dying breed, the quality that comes with it, especially because it is often longlasting (hello again leather gloves).
