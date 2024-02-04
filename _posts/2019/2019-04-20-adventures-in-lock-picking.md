---
title: Adventures in Lock Picking
date: 2019-04-20
categories: other
excerpt: A retelling of my adventures in lock picking during the school year. Of course, I made sure I didn't do anything illegal.
header:
  teaser: /assets/img/2019/lockpicking.jpg
---

<sub>Written 8-23-19</sub>

Note: I make no guarantee that any of this actually happened in real life. Any resemblance to reality is a coincidence. I have a very vivid imagination. Additionally, pictures may be staged.

One of the skills I picked up during the school year because everyone kept locking themselves out was lock picking. It all started when I locked myself out of my room one day and couldn’t get my roommate to come soon enough. I got the pick set from my friend and immediately got started. Within 10 minutes, I was in. Not a bad first try.

{% include figure image_path="/assets/img/2019/lockpicking.jpg" %}

During spring break I attempted to pick my friend’s door, with his permission of course. Unfortunately for me, I was caught by the RA and got written up. I had to meet with the residential director of Foothill for a hearing. At first I was prepared to be really rebellious and argue back with solid facts, but upon finding out that the director was acting as judge, jury, and executioner, I made sure to play nice. What the director did not need to know was that I’ve successfully lock picked like 10 times before. Funnily enough, most people get sent to the residential director for alcohol, not lock picking. After the hearing, I was emailed my conviction of tampering along with my punishment. They like to call it a “sanction” because it sounds less mean.

My “sanction” was to write a 500+ word essay about university policy on tampering, how it applied to my case, and what would happen if it didn’t exist, all without justifying my actions. Here’s what I sent in [Tampering Policy.pdf](/assets/pdf/Tampering-Policy.pdf)

I had way too much fun writing this essay. Ever since my SciOly days, I’ve loved picking rules apart. It took me two hours but it was well worth the laugh. I even made sure to employ the slippery slope fallacy at the end to really nail my point home. Surprisingly, my essay actually got accepted. I never lock picked ever again.

One line I didn’t have room to put in was about B5. Keys. It states, “Possession, duplication, misuse of University issued keys and key cards, including loaning keys to any other person, or leaving a key unattended in the lock, is prohibited.” Weird grammar aside, according to the policy, possession of university issued keys and key cards is prohibited. Thus we can’t have the keys to our own rooms. Even reading the policy differently, where possession, duplication, misuse are considered one act to solve the issue of possession individually being prohibited, issues still arise. Now I can duplicate a key without issue as long as I don’t misuse it.

Funnily enough, keys stamped with “Do Not Duplicate,” are not legally binding and are a very poor security measure. According to [this](https://blog.key.me/do-not-duplicate-keys/), these keys tend to be the least secure, which explains my ease with picking dorm locks. So much for excellent dorm security.

Later in the year I found out that Blackwell, our newest dorm, used RFID keycards for their doors. This was particularly intriguing. I found out that they used MIFARE Classic cards, whose security has been broken for over a decade. Trying to crack one using MFOC, it turned out that the card was actually a MIFARE Plus, which solved the security vulnerability of the past. After hours of research and emailing a dude on the internet for files, I was able to perform the newer hardnested attack on the card. 15 hours later, I was in. I copied the info over to a MIFARE Classic card.

{% include figure image_path="/assets/img/2019/lockpicking-rfid.jpg" %}

The copy only ended up working on the ground floor stairs and elevator, but that was still pretty cool. The rooms and lounges I believe use a reader that rejects MIFARE Classic, which is awesome. If the university wants to further improve security, they should upgrade the ground floor readers. However, I do believe the better readers can be circumvented if I got access to blank MIFARE Plus cards.

Of course, I should reiterate what I said above about making no guarantee that any of this actually happened. I just love security and I have a very vivid imagination. Perfect combination to tell a story.
