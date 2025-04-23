---
layout: post
title: "My Site Got Hijacked"
tags:
  - coding
created: 2025-04-23
---
My site (this one), started serving weird stuff and I didn't know why.

### Hijacked or Hacked?

A couple days ago, I got an email from Google Search Console Team, which I used for indexing and monitoring the quality of this site. It said that there was a new owner added. Umm. What? Rather than click the link from the email. I pulled up Google Search Console and checked from there. Yup. I saw the notification there too. So not a phishing attempt.

Okay, so what's the damage. I still owned the domain and I was in control of serving the site. Wasn't I? I opened up a browser and went to this domain. Oh no. Rather than showing this blog, I got some strange spammy site in Indonesian.

Mind you, I've also been sick the past few days, so I didn't have enough energy to deal with this. But I knew I needed to at least make sure my accounts weren't hacked, so I hopped on to AWS to make sure Route 53 didn't have anything weird and that my S3 bucket also didn't have content that wasn't mine. Phew. My AWS account was at least intact.

### Debugging

From the infrequency at which I update this site, I had basically forgotten how I had configured to host this site. I finally got around to debugging after feeling better (today). I was serving my website using GitHub Pages (GHP). In order to keep my repo private, I'd signed up for the Pro plan years ago. Up until now everything was fine.

About a week ago, I decided I wasn't getting $4 of value out of the plan. So to save a few bucks a month, I cancelled the plan.

That was the issue. I knew the Pro plan was letting me serve GHP from private repos, but I didn't realize the implications of letting the plan lapse without changing my repo to public.

### Lessons Learned

So what's the lesson here? I think there's two things:

1. Make sure you remember how you serve your website (or keep it really simple).

2. If you cancel a subscription you know has a dependency, make sure you think through what needs to be done for the dependecy.

For the first point, it really helped that I had [simplified how I serve my site]({% post_url 2023-01-21-learning-everything-again %}). Even though I didn't remember how I had configured it, it was easy to figure it out again because it was relatively simple.

Clearly I didn't think through the second point, otherwise I couldv'e avoided this altogether. Though this is the bigger lesson. Although I remember GitHub Pro allowed something with public/private repos, I hadn't followed up.