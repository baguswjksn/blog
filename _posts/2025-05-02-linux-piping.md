---
layout: post
title: Linux Piping
tags: tutorial linux shell
permalink: linux-piping
desc: Unlock the power of Linux pipes to build efficient and elegant command-line workflows.
---

Piping is a method of connecting the output of one command directly into the input of another. In Linux, the `|` character is used to create this connection. The basic syntax looks like this:

```bash
command1 | command2
```

This structure tells the shell to run `command1`, take its output, and use it as the input to `command2`. It’s a simple concept, but one that opens the door to an incredible range of functionality when working with the command line.

# Simple and Useful Examples

### 1. Filter Output with `grep`

```bash
ps aux | grep nginx
```

This command lists all running processes using `ps aux`, and then filters that list to show only those containing the word “nginx” by piping the output to `grep`.

### 2. Count Matching Lines with `wc -l`

```bash
ls -l | grep ".txt" | wc -l
```

Here, the `ls -l` command lists all files in long format. That output is sent to `grep` to filter for lines containing “.txt,” and finally piped into `wc -l` to count how many matching lines were found.

### 3. Sort and Uniquely Count with `sort` and `uniq`

```bash
cat access.log | cut -d ' ' -f1 | sort | uniq -c | sort -nr | head
```

This command processes a log file to extract the IP addresses (using `cut`), sorts them, counts unique occurrences with `uniq -c`, sorts them again in reverse numeric order (`sort -nr`), and displays the top results using `head`.

# Intermediate Techniques

### 4. Combine `find`, `xargs`, and `grep`

```bash
find . -name "*.php" | xargs grep "mysqli"
```

This example searches for all PHP files recursively in the current directory using `find`, then pipes those results to `xargs`, which passes them as arguments to `grep`. The result is a search for the string “mysqli” across all PHP files.

*Tip: Use `-print0` with `find` and `-0` with `xargs` to handle filenames with spaces safely.*

### 5. Use `tee` to Save and Display Output

```bash
ls -l | tee filelist.txt | grep ".sh"
```

This command lists files, writes the output to a file using `tee`, and simultaneously filters for `.sh` files using `grep` so you can view them right away.

### 6. Real-Time Log Monitoring

```bash
tail -f /var/log/syslog | grep "error"
```

This lets you monitor system logs in real time using `tail -f`, while highlighting error messages using `grep`.

# Advanced Usage Scenarios

### 7. Piping into a While Loop

```bash
cat urls.txt | while read url; do curl -Is $url | head -n 1; done
```

This command reads a list of URLs from a file and checks the HTTP status of each one using `curl`. The response is limited to the first line (status line) with `head -n 1`. It’s a useful technique for checking link health or server uptime.

### 8. Data Transformation with `awk`

```bash
df -h | awk '{print $1, $5}'
```

This example displays disk usage by piping the output of `df -h` to `awk`, which extracts and prints only the filesystem name and usage percentage columns.

### 9. JSON Pretty Print with `jq`

```bash
curl -s https://api.github.com/users/octocat | jq .
```

When working with APIs, this command fetches JSON data using `curl` and then uses `jq` to format it for easy reading.

# Creative Possibilities

Pipes enable a wide array of creative and practical workflows. You can automate database backups with a command like:

```bash
mysqldump -u root -p mydb | gzip > backup.sql.gz
```

Or download multiple files in a batch:

```bash
cat urls.txt | xargs -n 1 curl -O
```

You can even identify top memory-consuming processes by sorting process output:

```bash
ps aux | sort -nk +4 | tail
```

# Gotchas to Avoid

While piping is powerful, there are a few common pitfalls. Be careful when piping into commands that require elevated privileges; for example, use `sudo tee` if you need to write to a file with root permissions. Always quote variables inside loops to avoid issues with spaces or special characters. And when dealing with filenames that may contain spaces or unusual characters, prefer `find -print0` in combination with `xargs -0`.

# Final Thoughts

The Linux pipe is a cornerstone of shell scripting and terminal workflows. It lets you break down complex problems into smaller, manageable parts and chain them together in elegant ways. This reflects the Unix philosophy: simple tools, composed to perform powerful tasks.

Next time you’re working in the terminal, ask yourself:

“Can I pipe this?”

More often than not, the answer will be yes.
