# Claude Starter Kit

A step-by-step starter pack for getting up and running with Claude - designed for people who aren't developers and have never used a command line before (or don't even know what command line is - that's OK!).

If you haven't already, download the repo from GitHub (green Code button > Download ZIP), unzip it, and open the folder. This file will be inside it.

## Who this is for

You want to get involved more in "AI" and start levelling up your skills. You're paying for Claude (or about to), and you want to get the most out of it. You're not a developer and you've never written code, or not much of it at least. You want to see what all the fuss is about.

With this starter guide, you'll set up two tools, in this order:

1. **Claude Cowork first** - a mode inside the Claude desktop app where custom skills live. This is the fastest way to get real productivity wins. Installing a skill and building your own takes about 30 minutes, no terminal required.
2. **Claude Code next** - a command line tool for doing more powerful work with Claude directly from the command line. Takes about an hour to set up cleanly from scratch, and the guide walks you through it with every step explained in plain English.

You'll do Cowork first so you get a productivity win early and get comfortable with Claude doing real work for you. Then you'll move onto Claude Code, where things get more powerful (you can start writing code, without having to know how to write code!)

## By the end you'll have

- A Claude account with Pro or Max
- The Claude desktop app installed (home of Cowork)
- The `prompt-builder` skill installed in Cowork which makes it easy to create amazing prompts for any purpose (and for any large language model like Claude, ChatGPT, Gemini - any and all of them)
- Your own custom skill, built from scratch in about 15 minutes (Skills are a 'Claude' term at the time of writing - think of them as a saved prompt that you can rerun at any time).
- Claude Code running on your machine (so you can start building things with Claude Code)
- A personalised `CLAUDE.md` file so Claude already knows how you work
- Your first coding project pushed to GitHub

---

## Getting started

1. Download this repo (green Code button > Download ZIP) and unzip it.
2. Open the folder for your operating system:

   - **Mac** - open the `Mac/` folder and start with `README.md`
   - **Windows** - open the `Windows/` folder and start with `README.md`

Each folder contains the full kit for that platform - same structure, same skills, just with the right commands and instructions for your machine.

## What's in each folder

- `README.md` - the main guide that walks you through everything in order
- `build-your-first-skill.md` - the Cowork walkthrough (do this first)
- `claude-code-setup-guide.md` - the Claude Code setup guide (do this second)
- `CLAUDE.md` - a fill-in-the-blanks template used in the Claude Code setup
- `CHEAT-SHEET.md` - a quick reference guide for common commands and shortcuts
- `skills/prompt-builder/` - the pre-built prompt-builder skill

## Next Steps

Download the repo, open your platform folder, and follow the README.md inside it.

Have fun!



## Cheat Sheet (Reference Guide)

---

## Use Claude as your working partner

This is the thing most people don't do enough, especially when they're starting out: just ask Claude.

Get stuck on a command? Screenshot your terminal window or copy-paste the error, drop it into a Claude Cowork chat, and ask "what does this mean and what should I do?" You don't need to understand what went wrong - Claude will explain it in plain English and walk you through fixing it.

Not sure what to build next? Ask. Describe what you do for work and say "suggest three things I could build with Claude Code that would save me real time." Claude will give you ideas tailored to your situation.

Want to work faster? Run Cowork and Claude Code at the same time. Use Cowork for conversation and planning - it's great for thinking things through, writing, and giving Claude context about what you're trying to do. Use Claude Code for the actual building - it works directly in your files and folders. Flick between them freely. They complement each other.

The mindset shift is this: you're not using a tool, you're working with a partner. Talk to it like one. Give it context. Tell it when something's wrong. Ask follow-up questions. The more you treat it like a collaborator, the more useful it becomes.

---

## Quick cheat sheet

Once you're set up, here's what you'll use most. Full platform-specific versions are in `Mac/CHEAT-SHEET.md` and `Windows/CHEAT-SHEET.md`.

### Opening your terminal

**Mac:** press `Cmd + Space`, type `Terminal`, press Enter.

**Windows:** press the `Windows` key, type `PowerShell`, press Enter.

### Navigating folders

| What you want to do | Mac (Terminal) | Windows (PowerShell) |
|---|---|---|
| See where you are | `pwd` | `pwd` |
| List files | `ls` | `ls` or `dir` |
| Go into a folder | `cd foldername` | `cd foldername` |
| Go back up one level | `cd ..` | `cd ..` |
| Go to your home folder | `cd ~` | `cd ~` |
| Open folder in VS Code | `code .` | `code .` |
| Open folder in Finder/Explorer | `open .` | `explorer .` |

**Tip:** press `Tab` to autocomplete folder and file names - works on both platforms.

### Starting and using Claude Code

These commands are the same on Mac and Windows:

| What you want to do | Command |
|---|---|
| Start Claude Code in current folder | `claude` |
| Open a project and start Claude Code | `cd ~/code/myproject` then `claude` |
| Exit Claude Code | `/exit` |
| Switch model | `/model` |
| Clear the conversation context | `/clear` |
| See all available commands | `/help` |

### The basic loop

1. `cd` into your project folder
2. Run `claude`
3. Describe what you want in plain English
4. Review what Claude proposes, approve or decline
5. `/exit` when done

### Getting unstuck

**Command not found:** close your terminal and reopen it - newly installed tools need a fresh window.

**Something looks broken:** copy the error, open claude.ai, paste it in, and ask "what does this mean and what should I do?" Claude will walk you through it.

**Forgot where you are:** run `pwd` - it prints your full current location.

**Cancel a running command:** `Ctrl + C` on both Mac and Windows.
