---
name: okf-folder
description: Organise a folder of documents so people and agents can both find things fast. Writes a README.md (for people) and an index.md (for agents) in each folder, adds owners and review dates, and never requires reading the whole folder. Use when asked to set up, tidy, audit or maintain a knowledge folder.
license: MIT
---

# OKF Folder

Turn any folder of documents into a knowledge base that people and agents can both use, without anyone having to read everything first.

**How to use:** the user says "load the okf-folder skill and start with `<folder>`". Work only inside that folder.

## The one rule

- `README.md` is for people. It says what the folder is for, who owns it, and what to read first.
- `index.md` is for agents. It lists every file and child folder with one line each and a trust signal, so an agent can choose without opening them.
- Neither file may require reading the rest of the folder to learn what is in it or linked below it. Each folder's index describes its children; each child's index describes its own.

## Step 1: Look, then ask

1. List the folder (two levels deep at most). Do not read every file. Open only what you need to describe it.
2. Ask the user, in one short message, only what you cannot find out: who owns the folder, and what it is for. Use `[Owner Name]` and `[Date]` placeholders if they do not know yet. Never invent an owner or a date.

## Step 2: Write the two files for each folder

**README.md** (people): purpose in one or two sentences, owner, what to read first, how to add something, last review date. Plain language. No agent instructions.

**index.md** (agents): begin with frontmatter and a one-line statement that the file is for agents.

```
---
type: Index
title: "<Folder name>"
description: "<One line: what this folder holds>"
status: active
audience: agents
owner: "<Owner>"
updated: "<YYYY-MM-DD>"
stale_after: "<YYYY-MM-DD>"
---
```

Then include:
- **Rules for agents:** prefer `status: active` and in-date entries; say when an answer comes from an overdue entry; cite the file used; if nothing answers the question, say so and do not guess; update the index row whenever a file is added, changed or retired.
- **Files in this folder:** a table of Path, What it holds, Status, Owner, Review due.
- **Child folders:** a table of Path, Index, What it holds, File count, Last reviewed.
- **Parent:** link to the parent folder's `index.md`.

## Step 3: Add frontmatter to documents

Every knowledge document gets frontmatter:

```
---
title: "<Title>"
type: <SOP | Guide | Decision | Reference | Inventory | Note>
status: <draft | active | archived>
owner: "<Owner>"
review_due: "<YYYY-MM-DD>"
tags: [<a few words>]
---
```

Add only what you can verify. Do not guess owners or dates. If a document has no known owner, set `owner: "[Owner Name]"` and list it in your final report.

## Step 4: The 90-second test for procedures

A procedure is good when a newcomer can get through it in 90 seconds. It has five parts: **Question** (what someone is actually asking), **Answer** (two or three sentences), **Next step** (one action and who does it), **Owner**, **Review date**. Offer to rewrite long procedures into this shape, but do not rewrite without being asked.

## Rules

1. Search first: before creating a document, check the index for an existing one.
2. Archive, do not delete: set `status: archived` and move to an `archive/` folder. Update the index.
3. One owner and one review date per document.
4. Secrets never go in the folder: passwords, keys, tokens, personal data. If you find one, stop and tell the user, and do not copy it into any file.
5. Never overwrite a user's existing README.md or index.md without showing what would change and getting a yes. Prefer adding.
6. Keep indexes honest: counts and dates must match what is on disk.

## Maintaining

When asked to "check" or "audit" the folder:
1. Walk the indexes top-down (not the whole tree).
2. Report: files missing from an index, index rows with no file, documents without frontmatter, owners missing, review dates past due, folders without README.md or index.md.
3. Fix only what the user approves.

## Final report

Finish with a short list: folders given a README.md and index.md, documents given frontmatter, open questions (missing owners, past-due reviews), and the next suggested step.
