---
layout: post
title: Navigating Development in a Hyper Growth Startup (Pt 2)
categories: tech,personal
---

In [Pt.1](https://annanay25.github.io/navigating-development-in-a-hyper-growth-startup/), I explained that kind of growth I was lucky to witness in my first few years at Grafana. In this post, I'd love to highlight my observations on things that worked well for us. There's a few things in here that we can do as an IC (Individual Contributor),
and a few at the bottom of this list that can be implemented by company leadership. So lets' get into it.

### Processes and Reliability
Ship fewer things, improve the quality of existing pieces - Learnt this from my (then) manager [David Kitchen](https://www.linkedin.com/in/deekitchen). If you need other tweets as validation, [here's one](https://twitter.com/amasad/status/1488713434208169986) from Amjad Masad:

![Amjad Masad Tweet](../../images/amjad_tweet.png)

Before you pick something new to work on, check whether there are existing pieces that are slowing the team down. Focus on the small things - automated deployments, a fast CI pipeline, a flaky alert that wakes engineers up at night? Investing in processes and refining them pays dividends in the long run. In the Tempo squad (of 7 people) we started out with manual releases for the single ops and prod cluster we used to run, and today we’re managing ~10 production clusters all through weekly release automations. This is an example of the PRs our internal release bot creates:

![Tempo Rollout PRs](../../images/tempo_rollout_prs_1.png)

And the clusters we are able to manage with this kind of setup:

![Tempo Clusters (old screenshot, there are 20+ Tempo clusters today)](../../images/tempo_rollout_prs_2.png)

_Tempo Release Automation (old screenshot, there are 20+ Tempo clusters today)_.

Credit to _Koenraad Verheyden_ for setting this up for the Tempo team!

### Pay attention to metrics

Find the most important things to improve and find the easiest way to improve them. These are my favorite kinds of PRs. 

Some examples of the PRs and the effect they had on our system:

1) Hedged requests. Reduce our p99 query latency from 9.8s to 2.5s.

![Hedged requests. Reduce our p99 query latency from 9.8s to 2.5s](../../images/cpu_optimisation.png)

Tempo makes hundreds of parallel requests to the object store backend to fetch data for every query, but our response latency was bottleneck'ed on the slowest request. Hedging requests was a neat way to solve this!

2) Reducing TCO with bucket index.

![Reducing TCO with bucket index](../../images/bucket_index.png).

Adding a tenant index to reduce the number of calls to the object store backend. This simple change halved our TCO because that number of requests to GCS was a large part of our costs. 

3) A simple change to improve trace batching at the distributors reduced our CPU utilization by 40%!

![Better batching at the distributors reduced our CPU utilization by 40%!](../../images/hedged_requests.png)

### Async Communication
Write extensive meeting notes whenever possible and record important meetings. With the growing size of the company, not all teammates will be able to make every meeting, especially when it is a globally distributed workforce. 
Sharing context through notes is a great way to ensure everyone can contribute as well as feel connected to the ongoing development. Write, blog, document, present, record content.

### Delivery Planning and Ownership
If you promise to deliver something, ensure that you do. Regardless of the roadblocks in your way. You will be surprised how effective this super simple formula is in the workplace. 
Your team and company leadership will begin to take notice, and rely on you to pick larger projects.

### Communicating updates
Communicating updates is often two fold.

- Did someone in a different part of the company build a cool tool that could be useful to your team as well? Did they ship a new feature that’s gaining traction? Did they build a dashboard that you liked? Talk about it, because fresh ideas spark innovation.
Bring these updates to the team. Be vocal and bridge communication between teams. There is so much benefit in this as an organization grows large and its important to build upon each other's successes.

- Find reasons to talk to neighbor squads/teams. [A simple tweet](https://twitter.com/mrannanay/status/1480492206662111232) reaching out to developers working on common technologies led to a collaboration between Grafana and Segment in the development of an open source Parquet SDK for Golang.

![Engaging in Twitter threads](../../images/twitter_thread.png)

_Engaging in Twitter threads_.

### Handling Burnout

When innovation is all around you, it is up to you to make the most of it. At first we would prepare for a major launch once a quarter. Fast forward two years, new launches are happening every week. 
You hear about your own company from the news (this actually happened) and it’s really tough to keep up with the pace of development. 
Extremely talented peers in the team means that while you learn a tremendous amount every day, you also burn-out trying to match pace with the team. This also makes it very hard to disconnect from work, as you find yourself thinking about work related problems long after you walk away from your keyboard.
Sometimes, this pace of innovation can be overwhelming and make you feel alone / feel like you're not doing enough.
Taking time off to reconnect with family and friends, and working on your hobbies is important to recharge and engage with work again.

### Blogging online

[This tweet](https://twitter.com/aaditsh/status/1490374753554776075) sums this up well

![Aadit Sheth's List of Highest ROIs](../../images/blog_online_tweet.png)

_Aadit Sheth's List of Highest ROIs_.

Talk about your work and all the internals of projects that only you know about. Engineers love reading about other team's work and sharing the details internally to see if its valuable to them as well.

### Be a thinker-doer!

Probably the most important one that warrants its own blog post - be a thinker-doer. It is **so** important to do both. Don’t be just a thinker because you’ll never execute in the pursuit for perfection, and don’t be just a doer because you’ll never think about whether what you’re building is going to be useful at all. 
Force yourself to think about the impact your work will have. Are you going to spend 2 weeks working on a rather complex feature with very low adoption? (That would probably make sense if there are large customer asking for it though $$$ 😀). 
Will your work add value and improve the state of the system? These are tough questions and often don’t have a clear answer, but exercising these muscles is important for every developer.

### Hackathons

Hackathons are a great way to surface innovation from teams. In December 2021, I had an urge to try and store traces in a columnar format that promised much higher query performance by reducing i/o throughput from the object store backend.

![My hackathon that inspired Tempo's Columnar Backend](../../images/parquet_hackathon.png)

_My hackathon that inspired Tempo's Columnar Backend_.

After months of research and experimentation, Apache Parquet was adapted as the official storage format for Tempo, and powered TraceQL - the query language for traces.
There are lots of such examples of internal hackathon projects turning into full blown products within a year or two at Grafana. Some of these include [Adaptive Metrics](https://grafana.com/blog/2023/05/09/adaptive-metrics-grafana-cloud-announcement/) and the [collaboration between k6 & Tempo](https://grafana.com/blog/2022/11/03/how-to-correlate-performance-testing-and-distributed-tracing-to-proactively-improve-reliability/).

### Virtual and Regional Offsites
Meet with a set cadence, this could be once a quarter or twice a year, and a mix of virtual and in-person offsites; but take the time and get together to celebrate wins, challenges, hardships, and strengthen relationship between team members.
This is a great way to scale the team and increase belongingness. Here’s a [great guide from Myrle Krantz](https://grafana.com/blog/2022/01/13/virtual-offsite-ideas-that-work-how-the-grafana-cloud-team-brings-together-150-people-online/) to how to make virtual offsites work. 
In-person offsites are very valuable and a lot of fun too!

![Grafana Labs Monaco Offsite 2023](../../images/grafana_labs_monaco_offsite.png)

_All-hands pic from Grafana Labs Monaco Offsite 2023_.

### Invest in culture
Take care of your employees and your employees will take care of you. [We got named in the inc42 best places to work in 2021 and 2023](https://grafana.com/blog/2023/05/09/grafana-labs-named-to-the-inc.-best-workplaces-2023-list/).
Culture is a _hard_ problem. And its easy to talk about it in a hand-wavy sort of way. But asking the right questions is helpful in charting the right course. Here's a few to start: Is it clear to everyone why certain strategic decisions are made at the company level?
Do teams have a clear vision on what to execute on? Does leadership trust the teams enough to give them enough room to experiment and execute?

--- 

I know this is a long list and probably not everything applies to every company/employee. But thinking about some of these has been helpful to us. Thanks for reading this far and I hope you found this blog valuable!

Thanks to _Pablo.chachin_ and _Goutham Veeramachaneni_ for help in reviewing this blog post.
