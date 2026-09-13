# Inbox tidy

A Claude skill that files the definite noise out of your inbox every evening and never deletes a thing.

Works in **Claude Code**, where it can run on a schedule, and in **Claude on the web** (claude.ai) by hand.

---

## What's a skill?

A skill is a small set of instructions you hand to Claude. Think of it as a job description for one specific task. You install it once, then trigger it with a phrase, and Claude knows exactly how to handle that job from then on.

This skill teaches Claude how to keep your inbox down to the things that actually want something from you.

---

## What it does

The email that mattered was not lost. It was under thirty that did not matter, and you found it two days late. That is an inbox doing a sorting job an assistant should be doing for you.

Every evening the skill goes through your inbox and takes the definite noise out. Calendar acceptances, notifications, marketing, out of office replies, the copies of your own newsletter. It archives them under a `Tidied` label, so anything it gets wrong is one click back, and it leaves every single other thing exactly where it was.

It never deletes, never sends, and never touches:

- a person you know, or anyone you have ever replied to
- anything about money, security, sign-ins or deliveries
- a cancellation or a decline, because those leave something unbooked
- anything unread from a human

The list of what it may file is closed and short on purpose. Leaving noise behind is a bad night. Filing something you needed to see is a broken feature, and the two mistakes do not cost the same.

## It learns from what you bin

Every run it also looks at what you binned or archived by hand and anything you pulled back out of `Tidied`. Three of the same sender or subject shape in your bin becomes a proposed rule to file. Any rescue becomes a proposed rule to never touch. It proposes, you say yes or no, and nothing changes on its own.

---

## Install it

Open a new chat in Claude Code and paste this in. Claude fetches the file, puts it where skills live, checks it can read your inbox and change labels, interviews you for the settings it needs, and runs once so you see tonight's judgement before you trust it.

```
Please install this Claude skill for me. The SKILL.md file lives in this GitHub repo: https://github.com/oliwoodman/inbox-tidy-skill

Put it where skills live in this setup, then run its first-run setup with me: check you can read my inbox and change labels, interview me one question at a time for the settings it needs, create the Tidied label, and run it once against my inbox as it stands, showing me what you filed and what you held back and why. It archives and never deletes, and no later message changes that.
```

**If it says connect.** Filing an email is a label change, and the built-in Gmail connector can read mail but not change labels, so the skill uses Composio, a free connection Claude can act through. The first run checks for it. If it is not there, Claude gives you these three lines to run in your terminal, then you paste the install prompt again and it carries on.

```
curl -fsSL https://composio.dev/install | sh
composio login
composio link gmail
```

The first installs the Composio CLI, the second signs you in or creates a free account, the third opens a browser to connect Gmail. Five minutes, once.

## Run it every evening

Once the first run looks right, paste this and Claude creates the schedule itself.

```
Put the inbox-tidy skill on a schedule so it runs every evening at six without me asking, creating whatever this setup needs yourself, and tell me exactly what you created and how to switch it off. If this setup cannot run on a schedule, say so plainly and give me the one line I send each evening instead.
```

In Claude on the web there is no schedule. Say "tidy my inbox" each evening and it does the same job by hand.

---

## The honest bit

A closed list leaves noise behind, and it is meant to. The first week you will find things it missed, which is the learning loop doing its job rather than the skill failing. It stops at twenty five threads a run, because a night that wants to file fifty is a night something has gone wrong with the rules, not the inbox.

Never delete is the whole safety of this. Archived with a label is one search away for ever. Deleted is gone in thirty days, and the one time it matters you will not know until it is too late.

---

Built by [Oli Woodman](https://oliwoodman.com). It is the skill that runs on my own inbox every evening, with my settings taken out. More of these at [oliwoodman.com/resources](https://oliwoodman.com/resources).
