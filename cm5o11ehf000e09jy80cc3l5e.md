---
title: "Improving Observability: Breaking Down My Work"
seoTitle: "Improving Observability of Wiki Education Dashboard: What it entails"
seoDescription: "Explore how I'm enhancing the observability of the Wiki Education Dashboard, from improving system monitoring to refining error handling."
datePublished: Wed Jan 08 2025 15:00:55 GMT+0000 (Coordinated Universal Time)
cuid: cm5o11ehf000e09jy80cc3l5e
slug: improving-observability-breaking-down-my-work
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1736263935435/5d08663d-9e2b-49e9-95de-631ef6b879e3.png
tags: opensource, outreachy, outreachyinternship, wikimedia, wiki-edu-dashboard

---

## Introducing the Wiki Education Dashboard 🔬

First thing to note is that the Wiki Education Dashboard actually has 2 different sites the Wiki Education Dashboard — [dashboard.wikiedu.org](http://dashboard.wikiedu.org) and the Wikimedia Programs & Events Dashboard — [outreachdashboard.wmflabs.org](http://outreachdashboard.wmflabs.org)(explained better [here](https://github.com/WikiEducationFoundation/WikiEduDashboard/blob/master/README.md#:~:text=The%20Dashboard%20code,and%20other%20events.)). The term ‘Dashboard’—and sometimes ‘Wiki Education Dashboard’—is used as an umbrella term to refer to both sites, as they run the same general dashboard code, with environment-specific code where needed. The current homepage of the two sites are displayed below, can you spot the difference?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736251905571/fc81864a-cbf7-4c32-b5d3-dfcc8d03df7b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736251931325/48a23574-788f-439e-b374-5470f51fce59.png align="center")

My project is titled ‘**Improve observability of Wiki Education Dashboard**'—pretty straightforward, right? Well unless you don’t know what observability is. A few months ago, I did not.

According to [Wikipedia](https://en.wikipedia.org/wiki/Observability_\(software\)#:~:text=observability%20measures%20how%20well%20a%20system%27s%20state%20can%20be%20understood%20from%20the%20obtained%20telemetry%20\(metrics%2C%20logs%2C%20traces%2C%20profiling\).), “Observability measures how well a system's state can be understood from obtained telemetry (metrics, logs, traces, profiling)”. Basically how much information can be gleamed using data in form of system metrics, logs and other information. So in short, the purpose of my project is to make it easier for system administrators and end-users (course instructors, students, and others) to detect and understand problems with the system - the Dashboard.

Observability is typically the responsibility of [Site Reliability Engineers](https://en.wikipedia.org/wiki/Site_reliability_engineering) (SREs), but in full-stack environments, it often falls to Backend or Full-Stack Engineers as well. As a Full-Stack Engineer with a backend focus, this project is a great fit for me.

My project can be sub-divided into three sub projects which I detail below:

## 1\. Improving Existing documentation of the Dashboard’s Infrastructure and Deployment(s) 🖹

[Phabricator](https://phabricator.wikimedia.org/) is Wikimedia’s open-source tool for managing issues and projects and this task was actually born out of a Phabricator ticket. A Wikimedia SRE was trying to debug a downtime incident with the Programs & Events Dashboard but initially, could not find any details about where or how it was deployed. It took a while to figure it out, so they created a ticket requesting documentation of the Dashboard’s deployments.

In short, improving the existing documentation makes the system more observable by providing clear reference points for diagnosing issues. By clarifying how the different parts of the system interact—the servers, APIs, tools used, and others—I’m helping ensure that future incidents like this can be resolved faster.

## 2\. Reducing Noise in Sentry (and New Relic) 🔇

**What is noise, and why does it matter?** Noise is the clutter of irrelevant or low-priority error reports in monitoring tools that makes it harder to focus on critical issues. [Sentry](https://sentry.io/) helps track errors and performance, while [New Relic](https://newrelic.com/welcome-back) focuses on system metrics like response times and error rates. Together, they provide a full picture of system health, but only if they’re showing the right data. Reducing noise in Sentry is key to making it more effective—helping us focus on actionable issues and giving clear insights into what really matters.

I’ve started tackling this by archiving redundant errors and addressing the actionable ones. It’s a work in progress, but I’m excited to see the difference this will make once it’s complete.

## 3\. Building a User-facing System Status and Performance User Interface (UI) 👩‍💻

A typical system status site is used to provide essential context to admins and users about the system's status, helping reduce confusion during outages or slowdowns. For example, platforms like [Reddit Status](https://www.redditstatus.com/) and [Wikimedia Status](https://www.wikimediastatus.net/) use such sites to communicate the current state of their systems, including ongoing issues, scheduled maintenance, or performance disruptions. Status UIs display key metrics and historical data, providing a comprehensive overview of performance and reliability. This allows admins to address concerns proactively, while users can quickly determine whether the problems they face are system-wide or specific to their usage.

The proposed UI is a work in progress and it will be integrated into the existing Dashboard code, with its frontend server-rendered using Rails. An important part of my work involves deciding the level of detail to show and how to convert raw system data into user-friendly metrics that anyone—regardless of their technical knowledge—can understand. These metrics should clearly indicate whether the system components are functioning normally and, if not, provide insights like when the issue might be resolved.

## The Why

The Dashboard is an application that’s more important than it might seem. While on Phabricator, I stumbled upon comments thanking my mentor and longtime maintainer, Sage Ross, for getting the Dashboard back up and running after a downtime:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736259985561/a35c5cd4-4383-4bcb-859a-c4aaa3d9ffa8.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736260281224/7721e387-52af-46c1-8fd0-2597fe67fff2.png align="center")

This is what excites me about working on this project: the opportunity to contribute to something genuinely needed by people. This is the biggest project I’ve ever worked on, and the fact that it’s open source means my efforts are out there in the open for anyone to see. Contributing to the Wiki Education Dashboard felt daunting at first, but I’m so glad I took the chance. It’s helped me grow so much as a software developer, and I can’t wait to keep making meaningful contributions and learning even more along the way.

This is all for now, Thanks for reading and I hope you learned something! 😊✨