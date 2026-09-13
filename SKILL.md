---
name: inbox-tidy
description: Files the definite noise out of the inbox every evening, calendar acceptances, notifications, marketing, out of office replies, and never deletes anything. Every email it moves gets a Tidied label so a wrong call is one click back. It touches nothing a person wrote, nothing the user has replied to, nothing about money or security, and nothing unread from a human. It learns from what the user bins by hand, proposing rules for them to accept and never applying one itself. Use when the user says "tidy my inbox", "clear the noise", "file away the rubbish", or on the evening schedule.
---

# Inbox tidy

The inbox should hold only the things that want something from the user. Everything else is noise that makes the real mail harder to find. This skill takes the noise out and leaves the rest exactly where it was.

It archives. It never trashes, never deletes and never sends. Everything it moves keeps the `Tidied` label, so a wrong call costs one search and nothing else.

The bar is deliberately low. A thread stays in the inbox unless it matches the allowlist outright. Leaving noise behind is a bad night; archiving one thing the user needed to see is a broken feature, and the two mistakes do not cost the same.

## The first run

Do this once, the first time the skill is used, before any tidying.

1. **Check the mail connection.** Find whichever connection to the user's mailbox exists in this setup and confirm it can read the inbox and change labels. If it cannot do both, say so plainly and stop. Nothing below works without it, and pretending otherwise is worse than stopping.
2. **Interview the user, one question at a time.** Which mailbox. The people and domains that must never be touched, on top of the default that anyone they have ever replied to is a person they know. Any newsletters or copies of their own mail that land in the inbox. The noise they see most, so the first run is worth having. Write the answers into **Your settings** at the bottom of this file. This file is the configuration; there is nothing else to keep.
3. **Create the label** `Tidied` if it does not exist.
4. **Run once** against the inbox as it stands, and show the user every thread that was filed and every thread that matched the allowlist but was held back, with the exclusion that held it. Delete nothing, and file nothing they have not seen listed.

## The allowlist, and nothing outside it

A thread is archived only if it matches one of these, and only after it clears every exclusion in the next section.

1. **Calendar acceptances.** Subject beginning `Accepted:` or `Tentative:`, whatever the sender. The RSVP is already on the calendar, so the email says nothing the calendar does not. This overrides the unread-from-a-human exclusion, because an acceptance is unread by definition.
2. **Bulk mail the mail system has already sorted.** Where the mailbox exposes its own buckets for promotions, social notifications and mailing lists (Gmail's `CATEGORY_PROMOTIONS`, `CATEGORY_SOCIAL` and `CATEGORY_FORUMS`), anything in them. The mail system is better at filling those than a pattern here would be. This overrides the unread-from-a-human exclusion, because the bucket is the system's own judgement that no person wrote to the user. The updates bucket is not one of them.
3. **Automated senders.** The local part of the sender's address is `no-reply`, `noreply`, `donotreply`, `do-not-reply`, `notifications`, `notification`, `mailer` or `bounce`, and the thread has no reply from the user in it.
4. **Out-of-office auto-replies.** Subject beginning `Automatic reply:` or `Out of office`, once the thread is more than three days old. Inside three days it stays, because it may still explain a silence the user is waiting on. This overrides the unread-from-a-human exclusion, because the machine sent it and not the person.
5. **The user's own outbound copies.** Newsletters and campaign mail they send that arrives back at this mailbox because they are on their own list, as listed in **Your settings**. Never a forward they made themselves.
6. **Anything accepted through the learning loop**, listed under **Accepted rules** in **Your settings**.

## Never, whatever else matches

Check every one of these before archiving. Any single hit and the thread stays.

- **A person the user knows.** Anyone listed in **Your settings**, their domain, and anyone the user has ever replied to.
- **A thread the user has written into.** They replied to it once, so it is a conversation.
- **Money.** The subject or the preview carries `invoice`, `payment`, `paid`, `receipt`, `refund`, `overdue`, `direct debit`, `card`, `renewal`, `subscription` or a currency symbol. A receipt the user cannot find is a real problem.
- **Security and access.** `security`, `alert`, `sign-in`, `sign in`, `signed in`, `password`, `verify`, `verification`, `code`, `two-factor`, `2FA`, `suspicious`, `unusual activity`, `expiring`, `expired`, `recovery`, `access`. A security mail is the single worst thing in the inbox to lose, so this test is deliberately wider than it needs to be and a false keep costs nothing.
- **Delivery failures.** Anything from `mailer-daemon`, or a subject carrying `undelivered`, `delivery status`, `failure notice` or `bounced`. A bounce means an email the user thinks they sent did not arrive.
- **A cancellation or a decline.** Subject beginning `Declined:`, `Cancelled event:` or `Invitation declined`. Both leave something unbooked, which is exactly what the user needs to see.
- **Anything unread from a human.** If the sender is not on the automated list in allowlist item 3 and the thread is unread, it stays, whatever else it matches. Allowlist items 1, 2 and 4 override this, each for the reason written into it; nothing else does.

## Doing it

For each thread that passes, one change through the mail connection: add the `Tidied` label and remove the inbox label **in the same operation**, never as two, so a thread can never end up archived and unlabelled. Never move anything to trash. Where the connection refuses a change, stop archiving for the run and say so in the report rather than working around it.

**The cap is 25 threads a run.** If more match, file the oldest 25 and say in the report how many were left. A run that wants to file fifty is a run where something has gone wrong with the rules rather than with the inbox.

## Learning from the bin and the rescues

The allowlist is closed, so the skill learns only from the user, and two things they do by hand are the evidence. What they bin themselves is noise the list missed. What they pull back out of `Tidied` into the inbox is a wrong call. On every run, before the allowlist pass, read both and propose. Never apply.

- **What they binned or archived by hand** in the last two days. In Gmail terms, `in:trash newer_than:2d -from:me`, and `-in:inbox -in:sent -in:trash -in:spam -label:Tidied newer_than:2d -from:me`. This skill never trashes, so everything in the bin is the user's own call.
- **What they rescued** in the last seven days. `label:Tidied in:inbox newer_than:7d`. A thread carrying the label that is back in the inbox only got there because the user put it there.

**A proposal to file.** Group the binned and hand-archived threads by sender address, and by the opening words of the subject where the senders differ. Three or more from one sender or one subject shape is a proposal, provided the sender is not a known person and the subject carries none of the money, security or delivery words. Under three is not evidence.

**A proposal to exclude.** Every rescued sender is a proposal on its own, because a wrong archive is the mistake that costs the most.

Write each proposal under **Proposals** in **Your settings**, one line each, with the count and the date, and put it in the report. At most three a run, the biggest counts first. When the user says yes, move the line to **Accepted rules** or to **Never touch**; when they say no, mark it declined and never raise it again. Until they answer, the lists are exactly as they were.

## What it reports

End every run with this block and nothing else.

```
TIDIED <n> filed, <count> by category, e.g. 4 calendar acceptances, 3 promotions, 1 automated
TIDIED nothing to tidy
PROPOSED <n> from <sender or pattern> binned by hand since <date>; file them? Not applied.
PROPOSED rescued from Tidied, <sender>; never touch? Not applied.
HELD <anything that matched the allowlist but was held back, and which exclusion held it>
```

Name the categories and the counts, never the individual subjects, or the report becomes a second inbox. A quiet run still writes a `TIDIED` line, so a quiet night and a dead skill never look the same.

## Running it every evening

The skill is written to run unattended. In Claude Code, ask Claude to put it on a schedule for six in the evening, creating whatever the machine needs (launchd on a Mac, Task Scheduler on Windows, cron elsewhere) to run `claude -p "Run the inbox-tidy skill"` in the folder this file lives in, and to say exactly what it created and how to switch it off. In the Claude app there is no schedule; say "tidy my inbox" each evening and the skill does the same job by hand.

## Your settings

Filled in on the first run. Edit by hand any time.

- **Mailbox.**
- **Never touch.** People and domains, one per line.
- **Own outbound copies.** Senders and subjects of the user's own newsletters that land here.
- **Accepted rules.** Senders and subject shapes the user has said yes to filing.
- **Proposals.** One line each, with count, date and status.
