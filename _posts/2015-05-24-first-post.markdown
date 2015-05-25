---
layout: post
title: Welcome to BrokenOpenApp – Android crash reporting backend for ACRA with ProGuard and multi-project support.
slug: first-post
created: 2015-05-24 21:30:00
---

So another project I'm slowly working on is to do with Android crash reporting.

During a recent contract I got annoyed at the crash reporting tool I was using,
and finally decided to check out [ACRA](http://www.acra.ch/), an Open Source Android
crash reporting library I'd been meaning to try for a while. This can report a massive
range of info on each exception (naturally occurring or manually raised).

Originally, ACRA fed it's data in to a Google Doc – until Google got in touch and
kindly asked them to stop doing that. So now ACRA sends it's data over HTTP to a
back end you set up. There is an official back end now in development called
[Acralyzer](https://github.com/ACRA/acralyzer), but I cast round the PHP ones and
picked up one written in Symfony2. It basically seemed to work and it was in a
language and framework I know if I needed to hack on it.

I ended up using a slightly hacked version of this for the contract, and it did
help – tho to be honestly mostly it helped me realise that I didn't have a clue
why the app was crashing and as most of the crashes were around integration with
other apps on the device that worked fine for me, it just helped me realise I had
no chance of replicating these bugs in my environment. But it helped me think
through and fix some problems, so it was a plus.

Anyway, I am now hacking some more on this project and as I just got a major bit
of it working, time to post.

It's a back end for ACRA that stores crashes and sorts them into issues.

It supports multiple users and multiple projects, with access rights for this.

Each project can take crashes from one or multiple apps.

It supports ProGuard deobfuscation of your code.

The official backend Acralyzer seems focused on being very easy to install, which
I guess is aimed at Android devs who maybe aren't system admins. While that's a good
goal, I suspect this means it will be very hard or impossible for them to add ProGuard
support in a nice way.

BrokenOpenApp in contrast, requires PHP, Postgresql and a mail server. If you want
ProGuard support it requires Java, file store space and some ProGuard libs also
installing. Ideally cron is needed, and maybe a message que will be an optional
requirement later. Adding features at the expense of an easy install is a deliberate
decision for the project, and I know that means it won't be for everyone.

I owe a thanks to [ACRA Server from Marvin Labs](https://github.com/marvinlabs/acra-server).
This is the project I started with and have heavily hacked on, and my work is under
the same Apache Open Source license as it is.

So for now, it's there, it very basically works. A lot of the web pages for common
tasks are missing; such as ones to add other users to a project or even change a
users password.

The plan is to set this up, find some projects that can start sending in some real
data and slowly build up the feature set.

Anyone who wants to play, email james at jar of green dot co dot uk but this should
be considered alpha software for now. When it's beta software, I'll post again and
more widely.
