---
title: "Tiny Fixes, Meaningful Change"
seoTitle: "Tiny Fixes, Meaningful Change"
seoDescription: "Discover my journey as an intern tackling documentation, reducing Sentry noise, and building a Status UI—small steps toward meaningful, lasting impact."
datePublished: Sun Jan 19 2025 15:38:55 GMT+0000 (Coordinated Universal Time)
cuid: cm63s8nhb000109l1czflf8le
slug: tiny-fixes-meaningful-change
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1737300948517/a3f417be-af8b-44fc-85b3-c01460501c4e.png
tags: opensource, progress, outreachy, reflections, wikimedia, wiki-edu-dashboard

---

Today’s article is a progress report of what I have accomplished so far, six weeks into my internship and what I intend to accomplish by the end of it all.

### Documentation

I started my efforts on the documentation weeks ago and in [this article](https://emptycodesalsowrites.hashnode.dev/everybody-struggles#heading-improving-documentation), I detailed some struggles I went through in the process. I am proud to have completed it by week 4 🎉 and you can find the Admin Guide [here](https://github.com/WikiEducationFoundation/WikiEduDashboard/blob/master/docs/admin_guide.md)!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736251078664/9e4538bc-15a4-40eb-abac-0731d19280e2.png align="center")

### Reducing Noise

I kicked off my efforts to optimize Sentry error reporting with a comprehensive analysis of the Sentry configuration, followed by implementing initial filtering actions to reduce noise by week 2 which involved marking currently unactionable issues as ‘Archived’ and already resolved issues as ‘Resolved’. This helped declutter the dashboards to some extent.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737296774712/72a9a580-8d01-4719-ab4f-e9958ba761a5.png align="center")

However, the goal isn’t just to clean up Sentry but to address the root causes of errors so they don’t occur in the first place. Over the past two weeks, I’ve focused on debugging persistent issues like `NoMethodError`s (a common challenge in Rails codebases) and `TypeError`s (often seen in React codebases). Refining error-handling logic has been crucial, and one highlight is the introduction of a custom error class, which I implemented in [this PR](https://github.com/WikiEducationFoundation/WikiEduDashboard/pull/6114).

### Status UI

The current main feature of the work-in-progress Status UI is the latency-based queue status display, which uses Sidekiq queue data to show whether there’s a backlog or if everything is running smoothly. As I mentioned in my previous article, the goal of the UI is to communicate system status—whether things are working fine and, if not, what’s wrong—rather than focusing on technical stats like CPU usage.

While the UI hasn’t been launched yet, it’s coming together steadily, and I expect it will go through several revisions before it’s ready. Below is a snapshot of the current interface (which is still subject to change):

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737297601121/8bb6748d-2cd1-44cc-a31a-c02b23c8a210.png align="center")

### Reflections

Overall, I’m on track with my internship timeline and project goals, which you can check out [here](https://phabricator.wikimedia.org/T378119). Looking back, I laugh a little at how meticulously I outlined my timeline—especially for the noise reduction work, as debugging is never so straightforward.

As someone relatively new to Rails and Ruby, I’ve had to dedicate extra time to learning the concepts in depth. Writing new code has been a bit challenging because I try to ensure it’s not just functional but also maintainable. Some parts of the codebase haven’t been touched since they were written about eight years ago, and I want the code I contribute to be just as robust and long-lasting.

Another learning curve has been testing. Writing tests for bug fixes and running them to ensure they work as expected (and don’t break anything) has become part of my routine. The same goes for my UI implementation. While testing isn’t as foreign to me as it was a few months ago, I still have a lot to learn about writing “perfect” tests.

Moving forward, I aim to push myself even more in terms of learning and productivity. Thank you for reading—I hope you found this update insightful! 😊✨