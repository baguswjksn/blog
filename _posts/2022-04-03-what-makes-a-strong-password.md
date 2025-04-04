---
layout: post
title: What Makes a Password Strong
tags: tutorial 
permalink: what-makes-a-strong-password
---

Before we start, try to forget everything you know about passwords. Rules like “Passwords must include a capital letter and a number” or those little “strength meters” that give you the reassuring green checkmark that your password is impenetrable are dangerously misleading and incomplete. Some of the reasons are mathematical, but a lot of it has to do with human behavior as well. Let’s take a look at the math behind the curtain, and why an understanding of human habits can defeat the most powerful algorithms.

## Part 1: How do passwords work?

When you type your password and press enter to log in to an account, your password is encrypted ([hopefully!](https://transparencyreport.google.com/https/overview?hl=en)), sent to the server, and ‘hashed’ — a mathematical operation converting it into a long string of seemingly random letters, numbers, and symbols- from which it is impossible to tell what the original input was. This hash is stored on the server, so each time you log in, the hashes are compared- not your plain password. This way, only you know your password- not even system administrators can see it, and if the server is breached by hackers, they will only see the garbled-looking hash.

The crux of this process is the _hash function_ —the specific mathematical operations that change your password into this gibberish. Hash functions can be quite complex, but the basic idea is something pretty familiar. Let’s say our function is just simple addition, and our input is 2 integers as the ‘password’. You set a ‘password’ of 3 and 4. This is ‘hashed’ to 7 (3 +4 =7). Only this 7 is stored on the server. If a hacker gains access to the server and finds this ‘hash’, they have no way of knowing whether your ‘password’ is 3 and 4, or 1 and 6, or 5 and 2. This is a crucial point: **_you cannot conclusively determine the original input from the output._** Hash functions are **one-way.** (This is different than encryption, where you can easily regain the original input). Now, this example of addition as a hash function is incomplete- if the server just knows your numbers should equal 7, then any 2 numbers that sum to 7 will work to guess your ‘password.’ This is called having many _collisions-_ when two or more inputs result in the same hashed output. So, we need to add some transformation that results in as few collisions as possible, but still avoid any reversible operations. Let’s try concatenating the original digits, and multiplying the resulting number by our sum. So for 3 and 4, we’d have 3 + 4 = 7, then 7 * 34 = 238. For 5 and 2, we’d have 5 + 2 = 7, then 7 * 52 = 364.  
Remember, any guess that we make has to be in the form of 2 numbers, so we’d have to calculate the entire answer for each set of 2 numbers we want to guess. So what two numbers give us the output 1305?

You could probably figure it out eventually with a calculator, or faster by writing a program to guess and check, but it would take some work. This is basically the idea behind modern password hashing. Modern hash functions are highly complex, and take a computer a relatively large amount of energy to calculate. So even when we know what the formula is and what the output hash is, we have to invest such a large amount of computational time to guess that it becomes prohibitive to try. As we’ll explore below, it could take a computer easily thousands of years to guess a password. In fact, it’s been shown that with certain hash functions, the heat-death of the universe would occur before we could calculate all possible hashes with current global computing power.

## Part 2: Hash Cracking: It’s all Guess-and-Check

The only way to “crack” a password is to calculate the hash for a given input, and see if it matches the hash you’re trying to crack- i.e. guess and check. So for example, say the [hash function called MD5](https://en.wikipedia.org/wiki/MD5) takes 3000 CPU cycles to calculate (the actual number varies by formula and computer system), and maybe it takes 10 cycles to compare and see if the hashes are the same… so 3010 cycles to check one hash. If you have a 10 character password, there’s 72¹⁰ possible permutations of lowercase letters, capital letters, digits, and symbols (possibly more depending on what symbols are allowed as input)- about 3.75 quintillion possibilities. So with one core of a typical 3GHz CPU and about 3000 cycles per hash, we have 3 billion cycles per second divided by 3000 cycles per hash = 1 million hashes per second. One quintillion is a thousand billion millions, so 3.75 trillion seconds to calculate all possible combinations…which is about 118,833 years of constant CPU time at 1 million hashes per second. We’ll come back to this in a moment.

![](https://miro.medium.com/v2/resize:fit:875/1*rcd4jtucCbGQuw0Im9cP_w.jpeg)

It might help to understand exactly what happens in a hash formula, and why that takes CPU cycles. The short answer is that it’s just a bunch of math operations. In a modern CPU, you have registers which hold 64 bit binary numbers, and the CPU can perform basic logic operations on those, like adding two numbers together, or comparing them for equality. To do that, enough electricity has to be run through the transistors that make up the CPU to cause the electrons to move a “step forward” through the logic gates- similar to how a certain amount of electricity is required to make an electric motor revolve one time. So, a hash formula typically involves doing enough math to require at the absolute minimum a few thousand of these operations.

Most real hash functions are quite CPU intensive, and guarantee unique outputs for each input, etc. But modern CPUs have many cores, and you can also leverage the cloud….so say we have a bunch of cloud servers that totals 100 cores at 3GHz- using our example above of 118,833 years of single-core CPU, that would get us down to 1188 years….or say we have a giant server farm with ten-thousand cores, we can get it down to 0.1188 years (about 6 weeks). That’s for every possible hash, of course- i.e. we would have cracked every single possible password. If we were just trying to find a single hash, we might get lucky and crack it in perhaps a measly couple decades.

## Part 3: How to Crack a Password

In reality, we don’t need to guess _all_ the possibilities. Most people use combinations of letters and numbers that relate to their lives- e.g. English words and numbers from their birthdate- so we can vastly reduce the amount of guesses we need to take. For example, we could feed a list of every word in the English language into the popular [cracking program Hashcat](https://hashcat.net/hashcat/), and instruct it to calculate hashes for each word followed by the numbers 0 to 999. So rounding up to 200,000 words in English, plus 1000 following numbers for each one is 200,000 *1000 = 200 million possibilities, which would take 200 seconds at 1 million hashes/second. Not too bad.

Of course, most sites have “strength” requirements, like “your password must include at least one number, one capital letter, and one symbol.” Mathematically this is a great idea, but it doesn’t take into account what people actually do, and consequently these “strength” rules play right into hackers’ hands. A rule like this makes it harder for people to make a password they can remember, so we tend to head straight for common patterns and sequences. Most people will just capitalize the first letter of a word, put a common number like 123, 456, or a recent year, on the end, then a symbol that is easy to reach while holding the shift key- typically an exclamation point, at-sign, pound-sign, or asterisk (Yes, the keyboard layout affects how people choose passwords- “asdf” and “qwerty” are some recognizable common patterns). So in practice, these requirements actually make passwords LESS safe- sure, they prevent absolutely terrible passwords like “password”, but overall they make even complex passwords much easier to guess.

![](https://miro.medium.com/v2/resize:fit:875/1*_T4c0H4-wXKzdlCGb5CfAQ.jpeg)

We also know that everyone reuses passwords- not just their own, but we tend to come up with the same passwords as other people. Even when we think we’re coming with a “random” sequence, or something highly personal and original, it has usually been used by other people. We’re just not that different. Even when we create things that are “random,” we tend to pick sequences that are easier to type, or that are pronounceable in our native language. Cybersecurity researchers estimate that only about 7 billion distinct passwords are in use currently. In our earlier example of 1 million hashes/second, calculating 7 billion hashes would take 116 minutes. And modern GPUs and distributed systems can easily do billions per second.

So when trying to crack a password, or a whole stolen database of hashes, we want to take all these things into account and compile a list of possibilities that is most likely to crack the most hashes:

1. Words found in the most-spoken languages

2. Common numbers, such as sequences, birthdates, recent years.

3. Passwords that have been used before- large lists of these, known as “[cracking dictionaries,](http://enzoic.com/rockyou2021)” are publicly available.

4. Symbols and capital letters in common places — first and last characters, easy to reach from the shift key, etc.

5. Small phrases like “iloveyou” or “donthackme”

6. If targeting a specific website, statistically many passwords will contain the name of the site, e.g. “facebook123”

Depending on what other information is available about the target users, it may be possible to further refine the list (e.g. names, nationalities, etc).  
We know that this is actually how threat actors operate. Cybersecurity research has observed “credential stuffing” bots in the wild communicating with command-and-control (C2) servers that provide them with parameters (i.e. guessing rules) to target victims based on heuristics very similar to those described in the list above. Cracking websites and programs like Hashcat have evolved to make developing and applying these rules easier and faster. So how do we fight back?

## Part 4: How to Make Your Password Strong

Well, in theory this is easy- just don’t act like a human. But as we all know, that’s easier said than done. So let a computer do it for you, and use a [strong password generator.](https://www.lastpass.com/features/password-generator) This ensures that your password is not only mathematically robust, but that it is safe from behavior-based guessing. Of course, there is no 100% guarantee that even a random string of characters can’t be guessed (or that you won’t get malware that logs your keystrokes, or steals the passwords saved in your browser), so it’s also a good idea to have different random passwords for every account.

Changing habits is hard, however, and it’s better to improve than do nothing, so if you must continue devising your own passwords, try doing the opposite of what a human would do:

- ==use words to make nonsensical phrases (“parkinglot-bathtub-arboretum”)==
- place capital letters at random or in the middle of a phrase (“parkingLot-bathtub-ARBORetum”)
- use non-sequential numbers and a wide array of symbols (“parkingLot%bath395tub@@&ARBORetum”)
- don’t use any identifying information about you or the site/service.
- make sure your password is not already in a cracking dictionary.

If you’re a sysadmin or software developer, consider using credential screening services (like [Enzoic](https://www.enzoic.com/)) that check all your users against known compromised accounts and passwords, and continuously update their databases as more passwords are cracked or leaked in data exposures.
