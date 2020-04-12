# Hashgate
Proof-of-work driven anti-spam.

## Preface
For as long as computers have been able to talk to one another we have had to deal with spam.
Spam comes in many forms that range from minor annoyances (Comments promising to "earn $1000/week working from home!")
to completely catastrophic (Useless network traffic intended to overwhelm a system, i.e. DDOS attacks).

Good firewalls can mitigate these attacks for internal systems but when you want to have a public-facing service,
such as a website or email, blocking outside traffic isn't advisible.

Recognizing that most spam comes as a result of automation (1 bot can produce the output of hundreds of thousands of humans),
we developed CAPTCHAs to identify who the humans are. By only permitting access to users who can "prove being human",
we were able to cut out much of the automated spam in the world. Obviously, humans could still send spam themselves, but 
the impact of human-driven spam is much less than robot-users. 

As time goes on, we find that robots are becoming increasingly good at breaking CAPTCHA tests. We improve our criteria,
they improve their abilities. It's a constant game of cat-and-mouse that will likely never end. The entire concept of
extending trust to whoever we think is "human" will not prevent spam going forward. Users should not be granted different
security levels simply based on wether that user is made of flesh or code. 

*If we can't trust measurments of humanity, how do we prevent the bots from overwhelming us while still providing public services?*

## Concept
By utilizing the *proof-of-work* concept implemented by [hashcash](http://www.hashcash.org/) and popularized by [Bitcoin](https://bitcoin.org)
we can prevent spam by making widespread distribution of junk an expensive feat to carry out. The goal of this system would not be to
prevent robots from gaining access in the first place, but to make them do some intensive calculations before their request was
authorized.

Let's propose a scenario in which a user wants to post a comment on an online article. We will assume that the server the
comments are sent to is able to keep up and not be overwhelmed by any amount of data we send to it.
We have two users, *Human* and *Bot*. Without any sort of rate-limits in our system, Human is able to write and post comments
at a rate of 1 comment-per-minute (1 cpm). Bot is able to write and post comments at a rate of 10000 comments-per-minute (10000 cpm).
This means Bot is able to post comments at a rate of **~167 per-second**.

What if, in addition to the comment itself, we required the user to submit the answer to a math problem? This math problem would need to be complex enough to make a
computer spend a fair bit of time processing it, but not take so long that it makes the system seem "unusably slow" by our Human user.

Even if our equation only took 1 second to solve, this means that our Human user is only slowed down by ~1.7%, meanwhile our Bot user is effectively
capped at posting 60 comments-per-minute (a reduction of *99.4%*). 

For this system to work, we need our equation to meet a few criteria:
1. The question (and answer) needs to be unique and only valid for 1 use
  - If this isn't true, then Bot could solve the problem once and reuse the answer forever
2. We need to be able to verify the answer without solving the equation ourself
  - The goal is to limit how fast users can send in data, not limit our ability to receive it
3. It should not be possible to "pre-calculate" answers to the equation
