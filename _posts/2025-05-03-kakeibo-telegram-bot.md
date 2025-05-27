---
layout: post
title: How I Turned Kakeibo Budgeting Simpler
tags: tutorial 
permalink: kakeibo-telegram-bot
desc: From reading a traditional Japanese budgeting book to building a digital companion that fits in my pocket.
featured: true
---

Last week, I read a book on personal finance called _Kakeibo_ — the traditional Japanese method of mindful budgeting. It’s a simple, elegant system designed to make you think before spending, reflect regularly, and build a stronger relationship with your money. The approach emphasizes intention and awareness over complex tools, and it resonated with me immediately.

But there was one major drawback: it was all on paper. Kakeibo encourages you to carry a notebook, record expenses manually, reflect weekly and monthly, and write down your financial goals. While beautiful in theory, the physical format quickly became inconvenient in daily life — especially for someone constantly on the move and already managing most tasks digitally.

That’s when I had the idea: what if I could build a Telegram bot to help me follow the Kakeibo method in a more practical, accessible way? I already use Telegram every day — it’s fast, always with me, and supports bots well. I didn’t want a full-fledged budgeting app with graphs and dashboards. I wanted a simple, minimal tool that asked the right questions and supported the reflective process without adding complexity.

To build the bot, I chose **Go** as the main backbone for handling Telegram interactions. Go is fast, efficient, and once compiled, it's incredibly easy to deploy across different environments. I liked the idea of having a single binary that just runs without the need for a complex runtime or virtual environment. It made the bot reliable and portable — perfect for a small, personal project like this.

For data storage, I used **SQLite**. Since this bot is primarily for my own use, I didn’t need a full-blown server-based database like MySQL or PostgreSQL. SQLite is lightweight, file-based, and requires zero setup. It integrates cleanly with Go, and it handles the task of storing expenses, categories, and summaries without any hassle.

To process the data and generate reports, I leaned on **Python**. It’s my go-to tool when it comes to data manipulation, exporting to Excel, or visualizing summaries. I wrote a few Python scripts that read the SQLite data and output weekly or monthly reports. This separation between the bot logic in Go and the reporting logic in Python kept the code modular, and made it easy to iterate on each part independently.
