---
layout: post
title: Solving the Too-Many-Web-Servers Problem
tags: internal-tools productivity html css
permalink: too-many-web-servers
desc: How I built a lightweight internal portal to manage dozens of production and pre-production web servers.
featured: true
---

When I first joined my company, one of the biggest headaches I faced wasn't the work itself—it was just trying to figure out _where everything was_. We had a **ton of web servers**. Some were for **production**, others were for **pre-production**, and each had its own quirks. On top of that, different systems required different levels of access—some were admin-only, others for testers or developers. To make it more complicated, the URLs were scattered across internal docs, chat messages, and the occasional browser bookmark. It was chaos.

At first, I tried using bookmarks to organize the mess, but it quickly became clear that wasn’t enough. Bookmarks rely on the browser environment—some of our internal servers only work with specific secure browsers. If I opened the wrong link in the wrong browser, I’d either get an error or worse, be told the session couldn’t even start. It just didn’t scale. The friction was constant, and frankly, it made onboarding painful.

And so, I decided to build something better. I created a **unified web access portal**, completely written in **plain HTML and CSS**—nothing fancy, just solid and simple. Think of it like a dashboard, but inspired by the minimalist aesthetic of **imageboards like 4chan**. I liked the idea of separating things visually and conceptually by **app and operation type**, just like how threads are broken up by topic.

![Selamat Pagi](/assets/img/e5284689a95bd5a0c2bcb7367de7a8673a7a55b122586a0539d4dfb8fa90dcdf.webp)

Instead of searching through bookmarks or wikis, I could now go to a single page, click the relevant app group—say, "Payment Service – Prod" or "User API – Preprod"—and go directly to the login page, knowing it was the right environment and that my browser was compatible. I even tagged which environments required certain access roles, like admin or test accounts. The design was intentionally **low-stimulation and functional**, which helped me focus.

I’ll be honest: this also played to how my brain works. As much as I hate to admit it, **I’m not a great multitasker**—and science has some backing that male brains in general aren’t naturally wired for heavy multitasking. The more cognitive overhead I could offload, the better. I didn’t want to have to _remember_ server names, environments, access rules, or which browser to use. I just wanted to do my work.

This portal turned into one of the most helpful tools in my daily workflow. What started as a personal hack became something teammates began asking for. Now, we’re considering making it part of our onboarding process. It’s lightweight, secure (since it’s just local static HTML), and surprisingly effective.

No frameworks, no JavaScript, no servers. Just **HTML, CSS**, and a little inspiration from imageboard culture.

Sometimes, the best solutions are the ones that strip things down to the essentials.
