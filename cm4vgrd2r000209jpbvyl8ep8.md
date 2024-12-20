---
title: "The Growing Pains of an Open Source Contributor"
seoTitle: "The Growing Pains of an Open Source Contributor"
seoDescription: "Explore the challenges and growth of an open source contributor and learn how setbacks lead to valuable lessons."
datePublished: Thu Dec 19 2024 15:15:41 GMT+0000 (Coordinated Universal Time)
cuid: cm4vgrd2r000209jpbvyl8ep8
slug: everybody-struggles
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1734620903574/8b0fc636-30bc-4c5c-81d9-efaeccab6baa.png
tags: internships, opensource, reflection, outreachy, asking-for-help, wikimedia, wiki-edu-dashboard

---

For me, the best way to get things done is to dive right in without overthinking, as I tend to overanalyze everything. This is most obvious when I need to write comments or questions to my mentor. I can spend over 20 minutes trying to phrase things perfectly to avoid sounding stupid, too long, or unclear.

The irony is my mentor is super chill, encourages all questions, and responds quickly. So, I remind myself: **stop worrying about asking questions**. No one learns everything in a day, and experience is the best teacher—hence why jobs value years of experience.

## Lessons from my Outreachy Contribution period

My first issue, titled *"*[*Research and improve spec/lib/importers/revision\_score\_importer\_spec.rb*](https://github.com/WikiEducationFoundation/WikiEduDashboard/issues/5854)*,"* involved figuring out why a spec was behaving unexpectedly and fixing it. At the time, I had no idea what specs, fixture files, or VCR cassettes were—I hadn’t even written a test before. Instead of researching the concepts in depth, I chose to simply follow the steps to reproduce the issue, mapped the requests to the code making the API calls, and eventually understood the problem and its cause. This strategy worked for most issues I tackled.

However, it had downsides. I often started with a specific idea, only to realize later I’d misunderstood the issue entirely.

The lesson? **Don’t skip over unfamiliar terms—research them immediately**. It helps more than you think.

My second contribution, *"*[*Article Viewer displays raw wikicode for 'Health effects of electronic cigarettes*](https://github.com/WikiEducationFoundation/WikiEduDashboard/issues/5957)*,'"* was the most mentally exhausting. The issue remains unsolved, as the problem lies with a third-party WikiWho API integrated into the dashboard—something I didn’t realize at the time.

Riding the high of merging my first PR, I eagerly chose this issue, thinking I could fix it. I spent nearly three weeks debugging, finding leads but no solutions, and spiraled into self-doubt—wondering if I’d look incompetent or weak for giving up. Eventually, I documented everything I tried and posted a detailed report on GitHub. My mentor (also the maintainer of the dashboard) confirmed it wasn’t an issue with our codebase, so it wasn’t something I could have fixed.

The lesson? **Ask for help when you’re stuck—it saves time**. Also, **document every step you take**, even failed attempts. It proves your effort and makes revisiting the issue easier.

## Internship Struggles

I am working on 3 sub projects: Building a UI, Reducing noise in Sentry and Documentation efforts. Learn more about my project [here](https://phabricator.wikimedia.org/T378119).

### Building a UI using Rails

I am currently using [The Odin Project](https://www.theodinproject.com/paths/full-stack-ruby-on-rails) to learn more about Ruby and Rails. It’s a comprehensive, long-term resource that pairs well with official documentation.

Working with `.html.haml` templates was new but manageable, given my experience with `.cshtml` in C#. However, I did hit some challenges along the way. After completing the first draft of the MVP, I ran [RuboCop](https://rubocop.org/) on each file I changed/created but my `index.html.haml` file kept getting flagged.

```bash
app/views/system_status/index.html.haml:1:1: E: Lint/Syntax: unexpected token tDOT
.container.queues
^

1 file inspected, 1 offense detected

this is line 1: .container.queues
```

When I changed the first line to `%div.container.queues`, a similar error still appeared:

```bash
app/views/system_status/index.html.haml:1:1: F: Lint/Syntax: unterminated string meets end of file
%div.container.queues
^
```

Fed up, I decided to just add a RuboCop special comment to the file so it would be ignored:

```haml
# rubocop:disable Lint/Syntax
# rubocop:enable Lint/Syntax
```

Then the page would not render because `#` is unsupported syntax in haml. I finally thought to check the `rubocop.yml` file and guess what, the whole `../app/views/` directory was already excluded to start with! 🤡

The lesson? **Check relevant config files before trying to troubleshoot an error**; it could save you time and effort by confirming whether the issue is even applicable in the current context.

Later, while pushing commits to GitHub, I encountered a git issue:

```bash
~/WikiEduDashboard$ git checkout system-status-ui
Switched to branch 'system-status-ui'
Your branch and 'origin/system-status-ui' have diverged,
and have 19 and 1 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)
```

ChatGPT advised merging remote changes, but that resulted in 21 commits instead of the intended 2. Panicked, I had to turn to interactive rebasing. With some effort, I dropped unwanted commits and force-pushed my branch, resolving the mess.

The lesson? **Understand the git commands you use**. **Be cautious with ChatGPT advice** (searching forums like Stack Overflow might’ve saved time). Lastly, **embrace the power of** `rebase` —it’s a lifesaver.

### Improving Documentation

This task feels most familiar to me because I enjoy writing freely. The challenge lies in sourcing, compiling, and filtering information to decide what’s truly useful.

For example, I needed to understand the CI/CD pipeline and deployment tools the dashboard uses ([Toolforge](https://wikitech.wikimedia.org/wiki/Portal:Toolforge) and [Wikimedia Cloud VPS](https://wikitech.wikimedia.org/wiki/Portal:Cloud_VPS)). While it involved many new concepts, I pieced it together through MediaWiki and GitHub documentation, Phabricator tasks, Slack conversations, and my mentor’s guidance. It also made me realize DevOps isn’t as intimidating as I thought! 😅

### Reducing noise in Sentry

My first reaction to the Sentry dashboards was, “This is cool!” There was so much data—many errors I’d never seen. I started by creating a spreadsheet to analyze the errors and decide on an action plan.

I learned a lot about `TypeErrors` caused by the React frontend. Since JavaScript is dynamically typed, it doesn’t enforce strict type checks, leading to runtime errors. Most of these errors are unactionable and just create noise. My current focus is on finding an effective strategy to handle them..

This whole process has been a learning journey, and I love it—it means I’m getting smarter. (For example, I just learned “indepthly” isn’t a word while writing this! 🤦🏾‍♀️)

I plan to write an article soon explaining my project in more detail. Thanks for reading my word vomit—I hope you learned something! 😊✨