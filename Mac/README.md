# Claude Starter Kit - Mac

This is the Mac version of the Claude Starter Kit - a step-by-step guide for getting up and running with Claude, designed for people who aren't developers and have never used Terminal before (or don't even know what Terminal means for now - that's OK).

If you haven't already, download the repo from GitHub (green Code button > Download ZIP), unzip it, and open the `Mac/` folder. This file should be inside it.

## Who this is for

You want to get involved more in "AI" and start levelling up your skills. You have a Mac, you're paying for Claude (or about to), and you want to get the most out of it. You're not a developer and you've never written code, or not much of it at least. You want to see what all the fuss is about.  

With this starter guide, you'll set up two tools, in this order:

1. **Claude Cowork first** - a mode inside the Claude desktop app where custom skills live. This is the fastest way to get real productivity wins. Installing a skill and building your own takes about 30 minutes, no terminal required.
2. **Claude Code next** - a command line tool for doing more powerful work with Claude directly from your Mac's terminal. Takes about an hour to set up cleanly from scratch, and the guide walks you through it with every step explained in plain English.

You'll do Cowork first so you get a productivity win early and get comfortable with Claude doing real work for you. Then you'll move onto Claude Code, where things get more powerful (you can start writing code, without having to know how to write code!)

## By the end you'll have

- A Claude account with Pro or Max
- The Claude desktop app installed (home of Cowork)
- The `prompt-builder` skill installed in Cowork which makes it easy to create amazing prompts for any purpose (and for any large language model like Claude, ChatGPT, Gemini - any and all of them)
- Your own custom skill, built from scratch in about 15 minutes (Skills are a 'Claude' term at the time of writing - think of them as a saved prompt that you can rerun at any time).
- Claude Code running in your terminal (so you can start building things with Claude Code)
- A personalised `CLAUDE.md` file so Claude already knows how you work
- Your first coding project pushed to GitHub

---

## Step 1: Get Claude

If you already have Claude installed on your Mac you can skip to Step 2.

Get your Claude account and the desktop app.

1. Go to https://claude.ai/signup and create an account (or sign in at https://claude.ai/login if you already have one).
2. Subscribe to **Claude Pro or Max** at https://claude.ai/settings/billing. Pro is enough to start.
3. Install the **Claude desktop app** from https://claude.ai/download. Drag it into Applications, launch it, and sign in with the account you just created.

That's the prerequisite for everything else.

### Which model should you use?

Claude has a few models. For this kit:

- **Claude Sonnet 4.6** - your default. Fast, smart, handles most work brilliantly. Use it for 90% of what you do.
- **Claude Opus 4.6** - the heavyweight. Slower and uses more of your usage quota, but better at complex reasoning, strategy, long documents, and hard analysis. Switch to this when Sonnet's answer feels shallow or when the task really matters (a pitch deck review, a tricky business case, a gnarly bit of code).
- **Claude Haiku 4.5** - the fastest and cheapest. Good for quick lookups and simple tasks. You generally won't need it for the workflows in this kit.

**How to switch models in Claude Cowork:** in the desktop app, look for the model name at the bottom of the chat input box (it'll say something like "Sonnet 4.6"). Click it and pick a different model from the dropdown. You can switch any time, even mid-chat.

**How to switch models in Claude Code:** type `/model` in the terminal and pick from the list. Same idea - switch any time.

Default to Sonnet. Reach for Opus when you need more horsepower.

### A note on permissions

Cowork will ask your permission every time it wants to do something on your Mac for the first time - access a folder, download a file, run a command. You'll see Allow/Deny prompts throughout your chats. This is normal and intentional. The walkthrough flags when to expect them. General rule: if the ask matches what you just requested, allow it.

### Triggering skills (quick reference)

Once you've installed a skill, you can trigger it two ways in Cowork:

- **Slash command (most reliable):** type `/` to see installed skills, or type the name directly, e.g. `/prompt-builder`.
- **Natural language:** describe what you want and Cowork will match it to a skill based on the skill's description. Less reliable but more conversational.

Same works in Claude Code with `/skill-name`.

## Step 2: Build your first skill in Claude Cowork

Open `build-your-first-skill.md`. It walks you through:

- Opening Claude Cowork and granting folder access
- Installing the `prompt-builder` skill via the **Customise > Skills > +** menu in the desktop app (the cleanest way to add any skill)
- Handling permission prompts as they come up
- Using `/prompt-builder` to design your own custom skill through a guided interview
- Saving your skill, testing it (via slash command and natural language), and iterating on it

Plan 30 minutes for your first one. By your third skill, you'll be building them in 10.

## Step 3: Set up Claude Code

Open `claude-code-setup-guide.md`. This is your next move after you've built at least one custom skill in Cowork.

Claude Code is the command line version of Claude. It runs in your Mac's Terminal app and can do things Cowork can't - like kicking off longer-running tasks, writing and editing real code, and working inside projects you track with Git. Don't worry about any of those words yet - the setup guide explains every one of them in plain English, every command shown exactly as you'll type it.

This is the longer path - about 90 minutes - and it's the first time you'll touch Terminal. There's a safety section at the top that explains exactly what is and isn't risky, and Claude is there with you the whole time to help if you get stuck.

The guide covers: Terminal basics, Xcode Command Line Tools, Homebrew, Git and GitHub, Node.js, VS Code, Claude Code itself, picking your model with `/model`, a personalised `CLAUDE.md`, and a working Snake game as the celebration project.

## What's in this folder

- **`README.md`** (this file) - the orchestrator
- **`build-your-first-skill.md`** - the Cowork walkthrough. Do this first.
- **`claude-code-setup-guide.md`** - the Claude Code setup guide. Do this second.
- **`CLAUDE.md`** - a fill-in-the-blanks template used in the Claude Code setup
- **`skills/prompt-builder/`** - the pre-built prompt-builder skill (installed via the Customise menu in the walkthrough)

## Recommended next action

Complete Step 1 (get your Claude account and install the desktop app), then open `build-your-first-skill.md` and work through it.
