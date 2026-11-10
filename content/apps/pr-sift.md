---
description: 'PR Sift is my free Chrome extension for large GitHub pull requests: filter the files that matter, track what you have viewed, and keep private line notes for your AI coding agent, with no server.'
---

## Overview

::project-shot{src="/apps/pr-sift/review.webp" single alt="PR Sift open on a 39-file pull request on github.com. The top bar shows the title, a file filter, a progress ring reading 33 left and 6 of 39 done, unified and split buttons, and Notes with 3. Below it are chips for file types such as .php 28 and .vue 5, and for changes: added 23, modified 16, deleted 1, renamed 1 and with notes 3. A folder tree with counts sits on the left; on the right, a PHP diff shows a private note on lines 20 to 22 with a Post to GitHub button." width="1760" height="1166"}
A long pull request, filtered by type and change, with a private note on lines 20–22.
::

PR Sift is a browser extension for reviewing large pull requests on github.com. It adds a button to every pull request and opens a focused review on top of it: filters, a folder tree, viewed marks and private notes. I started it in November 2026. It works in Chrome and in Chromium browsers such as Edge, Brave, Arc, Dia, Opera and Vivaldi, and it is on its way to the Chrome Web Store.

## The problem

Large pull requests were slow to review on GitHub.

- **Too many files.** Lock files, translations, migrations and config sat between the changes that needed a careful read.
- **Losing track.** On a long list it was hard to see what was left, and a whole folder couldn't be marked as viewed at once.
- **Notes with nowhere to go.** Questions for myself or for an AI coding agent either became public comments too early or ended up in a text file.
- **Privacy.** I didn't want a review tool that sends private code to a server.

## The solution

::project-shot{src="/apps/pr-sift/smart-filters.webp" single alt="The Smart filters tab in PR Sift's sidebar. Quick chips read Tests 5, Docs 1, Migrations 2, Translations 6, Config 1 and CI / Docker 1. Below them are recurring folders, such as Billing with 16 files, and the files grouped by parent folder: src with Domain 9 and Presentation 5, resources/js 9 and lang 6." width="1760" height="1166"}
Smart filters group the files by kind and by folder, with a count on each.
::

**Show only what matters.** Click a file type or a change, such as `.php` or deleted, to show only those files; shift-click hides them for good. Smart filters pick out tests, migrations, translations, config and CI in one click.

**See what's left.** Mark files or whole folders as viewed, and a progress ring shows how many remain. A new push brings changed files back.

**Notes for your AI agent.** Private notes sit on a line or a range of lines, and only you see them. Copy them as one prompt, with the code they point at, for a coding agent or a chat, or post one to GitHub as a comment.

**Local only.** There is no server, account or analytics. PR Sift talks only to GitHub and keeps settings, viewed marks and notes in the browser.

## What I did

- Defined the product, its features and its privacy rule: no server, and nothing sent anywhere but GitHub.
- Designed the interface in light and dark, inside a shadow root so GitHub's styles and its own never mix.
- Built the extension with coding agents: I set the scope and the design, and reviewed every change.
- Built the website in English and Arabic, with guides, a changelog and screenshots recorded from a demo pull request.
- Published the source on GitHub under the PolyForm Shield licence.

## What it offers

::feature-grid
---
items:
  - icon: lucide:list-filter
    title: Type and change filters
    text: Show or hide files by type, such as .php or .test.ts, and by change, such as added, modified, deleted or renamed.
  - icon: lucide:sparkles
    title: Smart filters
    text: Tests, docs, migrations, translations, config and CI in one click, plus folders that repeat across the tree.
  - icon: lucide:folder-tree
    title: Folder tree
    text: Every changed file in a tree with counts, and search across files and folders.
  - icon: lucide:circle-check
    title: Viewed tracking
    text: Mark files or whole folders as viewed, hide them, and see what's left at a glance.
  - icon: lucide:message-square-lock
    title: Private notes
    text: Notes on a line or a range that only you see, saved for each pull request and resolved when done.
  - icon: lucide:bot
    title: Notes to your AI agent
    text: Copy open notes as one prompt with their code for Claude Code, Codex, Cursor, GitHub Copilot, Claude or ChatGPT.
  - icon: lucide:columns-2
    title: Split or unified
    text: Switch every diff, or just one file, between split and unified views, in a light, dark or system theme.
  - icon: lucide:shield-check
    title: No server, no tracking
    text: Settings, viewed marks and notes stay in the browser, and a GitHub token is optional.
---
::

## System design

PR Sift runs inside the pull request page. A shadow root keeps GitHub's styles and its own apart, and a background worker reads the diff from GitHub with the login you already have. A GitHub token is optional: it is used only to read through the API or to post a note as a comment.

### Logic without a browser

The rules for diffs, the folder tree, smart filters and note prompts live in a package with no browser code, so each one is tested on its own. Only two places touch the browser: storage and the network.

### Private by design

Settings, viewed marks and notes are stored on your machine and are deleted with the extension. It asks for access to three GitHub addresses and nothing else, and it never sends your notes to an assistant: you paste them yourself.

## In the product

::project-shot{src="/apps/pr-sift/notes.webp" single alt="A note being written on lines 16 to 21 of a new PHP file. The selected lines are highlighted, and above the note box are buttons to move the start and the end of the range. The note reads: Filter zero quantities in SQL instead of in PHP, the totals table can be large." width="1760" height="1166"}
A note on a range of lines, with its start and end adjustable.
::

::project-shot{src="/apps/pr-sift/ai-export.webp" single alt="The Private notes dialog over a blurred review: 3 open, 0 resolved, only you can see these. Each note shows its file, its lines and its text. A menu next to the Copy for Claude Code button lists coding agents (Claude Code, Codex, Cursor, GitHub Copilot), chats (Claude, ChatGPT) and Clipboard only." width="1760" height="1166"}
Every open note, copied as one prompt for a coding agent or a chat.
::

::project-shot{src="/apps/pr-sift/dark.webp" single alt="The same 39-file pull request in PR Sift's dark theme: the type and change chips, the folder tree and a PHP diff with a private note on lines 20 to 22." width="1760" height="1166"}
The same review in the dark theme.
::
