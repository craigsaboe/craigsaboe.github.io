---
layout: post
title: Craig's Rules of Development
author: @craigsaboe
published: 2021-08-30
---

1: WBAE
WITHOUT BREAKING ANYTHING ELSE!

Rule number one. Whatever you are going to do, is there a non-trivial chance that this could break a production system or process?  Whether it's an update, a new software application, restarting a server, just tweaking a config file - the *first thing* to consider is whether this could impact our customers or co-workers in a negative way.  Sometimes it's unavoidable; sometimes the higher-ups will override those concerns and tell you to do it anyway.  But at the end of the day, working production applications are what customers are paying for, and if they don't work, they don't pay for them, which is bad.

2B: IIHUT
    Is It a Higher-Ups Thing

Inevitably, you get the request.  It's a non-negotiable request, that comes from the higher-ups as an order that isn't meant for discussion.  Regardless of your hesitancy, your opinion that it's not the right way to do it, or your frustration that it's not up for discussion, you have to just grit your teeth and do it.  Hack some feature on to something that is just going to give you a ton more work later on?  Push to production something that is half-finished and you aren't even sure it will work?  Yup, just gotta do it.  
There are two important things to keep in mind here.  First, the request DOES make sense - to someone in authority.  Yes, they may be misguided, misinformed, or just stupid.  However, they might also know more about the big picture that makes this idiotic request actually make sense.  Say the boss tells you to push that feature out ASAP that is barely more than scaffolding yet - hard-code stuff, fake other stuff if necessary, just push it out half-done so it can pass at least basic scrutiny.  
This goes against everything you stand for as a developer!  It's stupid, wait 'til you're done!  They don't get it!!  
Well, what you don't know is that there's a huge deal that sales almost has signed - except the client's CEO is hung up on your app not having this one feature while your competitors do.  Who knows why that's the case, but if sales can just show him the feature is in beta/about to go live/just being polished, then your company is going to land a really significant contract.  By the time they come on-system, you will be done with the 'real' feature and all will be well.  You won't know about the deal, or the situation, but from that perspective, making "something" is worth whatever time you have to spend to make it happen.
Second, WBAE is #1 because it still needs to be evaluated before doing this.  If fulfilling the request will likely break/destabilize/otherwise damage your existing systems, then that should be made very clear, even to the very top.  You might still have to, crossing fingers that all will be well, and hope you won't get the blowback if all hell breaks loose.  But if there's one thing that the higher-up might care about more than selling or making the feature available, it would be all the angry calls from customers who no longer can use the system they are paying for because something broke. 





2: WWHUS
What Would Higher-Ups Say

3: UMNS
    Users Make No Sense

4: TINS
    There Is No Spec

5: ITFAR
It’s There For A Reason 

6: DIRM
Does it REALLY matter?


Subject to revision, modification and reordering at any time whenever Craig feels like it.