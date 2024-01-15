---
layout: post
title: My process for code review
categories: tech
---

Pull requests (PRs) are the fundamental building block in any tech company. Every day we create, review and merge hundreds of PRs. 
Some add features, some fix bugs, some introduce bugs and some are so large nobody wants to review them. 
However, each of these plays a crucial part in pushing the product and company forward. I previously wrote about best practices for creating a PR [here](https://annanay25.github.io/contributing-to-open-source/), check that out if you are interested.

Each of these PRs comes with the responsibility of a thorough code review. Reviews are incredibly important. 
They help spot issues with code correctness, performance, styling and documentation that the author might have overlooked. 
Apart from the software-related benefits, they also provide a sense of gratification for helping another team member move their work forward and get it merged! 

When I started my journey as a software developer, I had the impression that reviews are done by going through code in the UI. Boy was I wrong about that. 
Over time I learnt that there is a methodical process for performing reviews, one that requires a balance between thoroughness and efficiency. 
Here is a process that has worked well for me, feel free to adapt and change it to your liking!

### Phase 1: Understanding the purpose
- Check out the PR branch locally - This helps place the changes in context with the rest of the codebase, something that’s hard when viewed in just the Github UI.
- Understand _what_ the change is from the PR description/ticket linked to it.
- Understand _how_ the author is trying to implement the said change.

### Phase 2: Spotting bugs/changes (Everyone has their own checklist, so fork and change this if needed)
- Implementation
  - Does the PR do what the author claims it does?
  - Are there tests to prove it?
  - Edge cases - does it fail when inputs are not in the expected format?
  - Is there a better way to implement the same functionality?
  - Does the change affect other parts of the service that it is not supposed to?
- Performance
  - Is it the most efficient approach to implement the change?
- Code design
  - Are the classes/structures organized according to the style of the codebase?
- Final few important ones
  - Is there sufficient documentation for the changes - both in code comments, as well as any public facing docs?
  - Are there sufficient metrics/logs/traces to track the new functionality?

### Phase 3: Writing feedback
- Be verbose when you’re requesting changes - point to examples, drop links, screenshots - anything to help the author understand why you’re asking for the change.
- Be blameless in the review - this is not about pointing faults with the author :)
- Don’t feel bad about pointing out things even if the PR is opened by someone senior to you - everyone assumes positive intent and knows reviews are healthy for the codebase.
- There’s often a misconception that only one person can review a PR, but feel free to add reviews even if a PR has been reviewed already. Of-course this doesn’t mean you spam every PR but if you see a meaningful change feel free to point it out even if the PR has been reviewed or even merged!
- Reviews should not be rushed, take time to perform your review. I haven’t timed my own process but I agree with some statistics on the internet about taking 60-90 mins to perform a review containing ~200 lines of code. Reference: [Smartbear survey](https://smartbear.com/learn/code-review/best-practices-for-peer-code-review/).


And that’s all! Reviews should be fun and rewarding, and as with everything we are all learning, so we’ll get better at this with time. Happy reviewing!
