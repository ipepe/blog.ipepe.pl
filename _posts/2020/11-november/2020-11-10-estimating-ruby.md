---
title: Three things you need to know to produce an accurate estimate
categories: programming
author: Rahoul Baruah
---
This post actually was created by Rahoul Baruah on September 8, 2015. Unfortunately Rahoul's blog is unavailable that's why I remade it. Sources avaialbe at the end of post.

Estimating is the bane of most developers’ lives. Your boss asks you how long something will take, with the caveat

`I know it’s hard to do and I won’t hold you to it but I have to tell the customer something.`

You calculate your best answer, then double it. The boss walks away, performing some sort of mental spreadsheet calculation. And you get to work.

And then you find out that the deadline for that task you carefully doubled is approaching fast. Suddenly you’re actually running over, the customer’s constantly on the phone and your boss is constantly staring at you from their enormous air-conditioned office.

Eventually, you get the work done, it ships, the customer stops moaning and then the boss stops staring and you swear there must be a better way (continued below).

Well there is.

Because an estimate isn’t just about figuring out how long a piece of work will take. That’s not the half of it. In fact it’s only a third.

A good estimate has three parts to it.


## The size of the job
 * `I can build that in a couple of hours.`
 * `That’s about half a day to implement.`
 * `Oooh, I reckon we’re looking at a week’s worth of work there`

That’s what we’ve all done – looked at a job and based upon experience and some guesswork, tried to figure out how long it will take.

But that’s not all.

## The risks
 * `Simple; I’ve done that loads of times before`
 * `On the surface it looks pretty simple, but there may be a couple of knock-on effects we’ll need to watch out for`
 * `Hmmm, the 3rd party component claims to be able to handle this, but we’ve never tried it and it’s quite tricky to set up`

If it’s something you’ve done a thousand times before you can be sure you can gauge the size of the job pretty accurately. If you’re not familiar with the whole code-base or you feel that there’s likely to be some hidden depths to the request, your assessment of the size is necessarily less accurate. And if it involves data imports, 3rd party APIs or something you’ve never done before, you can be pretty sure that something unexpected is going to crop up and eat up a big chunk of your time.

## How quickly will you get it done?

You’ve already said it’s a 24 hour job – so between 4 and 5 days. The boss tells the client it will be ready on Friday.

And on Monday you get a solid 6 hours into it. 1 day down, 18 hours left and it’s looking good.

On Tuesday, you make a good start, then get called into a meeting that lasts for ages. Then a whole series of phone calls with a client who thinks they’ve found a bug. Interruptions galore. You’ve only really done 3 hours. 2 days in, 15 hours of work left. Tomorrow needs to be a good day.

Wednesday and you forgot it was Dave in accounts’ birthday. A solid 3 hours work and the fire alarm goes off. You manage to squeeze in a couple more hours, but you’re not happy with your work – better do it again tomorrow. Only 2 days to go and you’ve got at least 12 hours of work left.

You get the picture.

An 8 hour job never takes 8 hours.

In fact measuring the size of the job in hours is misleading – project management types refer to it as the difference between elapsed versus effort time.

But to reduce confusion (from your boss, at the very least), I prefer to separate them completely.

Each estimate should be presented in terms of its complexity rating, its risk rating and the project velocity.

The complexity rating is a simple measure of how big the job is. Choose a scale and stick to it.

 * 1 is “trivial”
 * 2 is “a bit of work”
 * 4 is “a lot of work”
 * 8 is “oh blimey, do you really want that?”
The risk rating is a simple measure of how confident you are about the job.

 * 1 is “I can do this in my sleep”
 * 2 is “OK, but there may be a few issues”
 * 3 is “not sure about this, it’s doable but…”
Take your feature request, write down a complexity and risk score and multiply them together.

A big job that you know how to do could be equivalent to a small job that’s all new. The higher the score, the more time or effort it’s going to take. A really high score suggests you probably want to break it down into smaller tasks or try to remove the risk.

Then, when you start working on a feature, track your time. It doesn’t need to be exact; to the hour is probably good enough.

As you complete the piece of work, write down the time it took you and the points score. Keep a tally of the total number of points completed and the total number of hours spent.

After each feature, divide the total points by the total hours.

This is your velocity – points per hour.

Every now and then (once a week, once every two weeks, depending upon your client), go back to your list of unfinished features, take the number of outstanding points and use your velocity to calculate a possible end-date for the project.

Send this to your client.

The next time you recalculate the end-date and send it to your client, add a short note explaining why it’s different to last time (X took longer than expected, we couldn’t complete Y because we were waiting for some content from you, Z looked really difficult but turned out to be 2 lines of code).

And the absolute best thing about this method?

It’s self-correcting.

If you consistently underestimate the risk in pieces of work, your velocity will plummet.

If you keep on expecting things to take longer than they do, your velocity will increase.

And in both cases, the project end-date will move to reflect this – based upon real evidence – the velocity you have been calculating as the project progresses. Not only will your client have confidence in the end-date you’ve supplied but they’ll understand exactly why the project end-date is where it is.

Sources: 
 * https://web.archive.org/web/20171008185545/http://theartandscienceofruby.com/2015/09/08/three-things-you-need-to-know-to-produce-an-accurate-estimate/