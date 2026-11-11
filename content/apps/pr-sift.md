---
description: 'PR Sift is my free Chrome extension for reviewing large GitHub pull requests: show only the files you care about, mark what you have read and keep private notes for your AI assistant.'
---

## Overview

::project-shot{src="/apps/pr-sift/review.webp" single alt="A GitHub pull request open in PR Sift: filters by file type and change across the top, a folder tree on the left, a diff with a private note on lines 20 to 22, and a counter that reads 33 left, 6 of 39 done." width="3200" height="2120"}
PR Sift on a pull request with 39 changed files.
::

PR Sift turns a long GitHub pull request into a focused review. Open any pull request, press PR Sift at the bottom right, and the files you don't need step aside. It works in Chrome and in Chromium browsers such as Edge, Brave, Arc and Dia. I started it in November 2026, and it is on its way to the Chrome Web Store.

## What it does

### Show only the files you want

Click a file type or a kind of change to show it. Shift-click to hide it for good.

::project-video{src="/apps/pr-sift/filters.mp4" poster="/apps/pr-sift/filters.jpg" alt="Clicking the file type filters in PR Sift: the list narrows to the chosen files, and a hidden type shows crossed out." width="1600" height="1000"}
Filters by file type and by change.
::

### Never read a file twice

Mark files or whole folders as viewed. A new push brings back only the files that changed.

::project-video{src="/apps/pr-sift/review.mp4" poster="/apps/pr-sift/review.jpg" alt="Marking files and whole folders as viewed in the PR Sift folder tree." width="1600" height="1000"}
Whole folders marked as viewed.
::

### Private notes for your AI

Notes only you see. Copy them for Claude Code, Codex, Cursor or ChatGPT, or post one to GitHub.

::project-video{src="/apps/pr-sift/notes.mp4" poster="/apps/pr-sift/notes.jpg" alt="Writing a private note on selected lines of a diff in PR Sift, then sending the notes to an AI assistant." width="1600" height="1000"}
A private note, ready for an assistant.
::

## Privacy

Your code stays in your browser. PR Sift talks only to GitHub, keeps filters, viewed marks and notes on your computer, and has no server, account or analytics.
