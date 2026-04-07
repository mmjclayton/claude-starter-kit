# Build Your First Skill (Claude Cowork for Windows)

A step-by-step walkthrough for installing the `prompt-builder` skill in Claude Cowork, then using it to build your own custom skill. Everything here happens inside Cowork (the mode in the Claude desktop app) - no command line required.

**Before you start:** make sure you've completed Step 1 of the README - you need a Claude Pro or Max subscription and the Claude desktop app installed and signed in.

## What's a skill and why does this matter

A skill is a set of instructions that teaches Claude a specific workflow - for example, "when I ask you to brainstorm a product idea, do it like a sharp VC asking hard questions." Once installed, Cowork recognises when you need the skill and follows that workflow every time, consistently.

Claude comes with a lot of pre-built skills, but the ones tailored to YOUR work will always be the most valuable. Building your own takes about 15 minutes per skill. This walkthrough shows you how.

## What you'll do

1. Open Claude Cowork and give it access to a folder on your PC.
2. Install the `prompt-builder` skill (Cowork downloads and installs it for you).
3. Trigger `prompt-builder` and let it interview you about the skill you want to build.
4. Have Cowork save the result as a proper SKILL.md file.
5. Test it, then iterate.

Total time: 30 minutes for your first skill. Subsequent skills take 10-15 minutes each.

---

## Step 1: Open Claude Cowork

Launch the Claude desktop app and open a new chat in **Cowork** mode. Cowork is the mode inside the Claude desktop app where skills live and where Claude can access files on your PC. If you don't see Cowork as an option, check you've signed in with your Pro or Max account.

When you start a Cowork chat, Claude will ask for access to a folder on your PC. Select your user folder (the one with your name on it, usually something like `C:\Users\yourname`). This lets Cowork read and write files when you ask it to - including where skills live (`%USERPROFILE%\.claude\skills\`).

**Check your model:** at the bottom of the chat input box, you'll see the model name (e.g. "Sonnet 4.6"). Click it to switch. Stick with **Sonnet** for this walkthrough - it's fast and plenty capable for building skills. Switch to **Opus** later when you're tackling heavier work like strategy, analysis, or long documents. See the "Which model should you use?" section in the README if you skipped it.

## Step 2: Install the prompt-builder skill (pre-read)

You're going to install `prompt-builder` using the Claude desktop app's built-in skills manager. This is the cleanest way to add a skill - no file paths, no command line.

### A note on permissions (important, read this first)

Cowork is cautious by design. Every time it wants to do something on your PC for the first time - access a folder, download a file, run a command - it will pop up a permission prompt asking you to **Allow** or **Deny**. You'll see these throughout your Cowork chats, not just on day one.

**What you'll see in this step:**

1. First, Cowork will try to download the file from GitHub. It may ask permission to access the web or a specific domain - click **Allow**.
2. Then Cowork will ask to access your Desktop folder to save the file there - click **Allow**.

If something fails (e.g. "Failed to fetch..."), it's usually because a permission hasn't been granted yet. Read the popup, allow what it's asking for, and tell Cowork to try again.

General rule: if Cowork is asking for access to a folder or domain that matches what you just asked it to do, allow it. If a popup appears out of nowhere asking for something unrelated, say Deny and check what's happening.

As you may have already guessed, you actually already have the prompt builder skill.md file on your machine if you downloaded the whole folder from Github earlier. That's OK. It's good to get used to asking Claude to do things for you, even if it is technically a double up this one time.

### 2a. Get the SKILL.md file onto your PC

Paste this into your Cowork chat:

```
Download https://raw.githubusercontent.com/mmjclayton/claude-starter-kit/main/skills/prompt-builder/SKILL.md and save it to my Desktop as prompt-builder-SKILL.md. Confirm when it's done.
```

Approve the permission prompts as they appear (web access, then Desktop folder access). Cowork will then fetch the file and save it to your Desktop.

If the download fails, tell Cowork: `Try again.` It usually works on the second attempt once permissions are sorted.

### 2b. Install it via the Customise menu

1. In the Claude desktop app, click **Customise** in the bottom-left of the sidebar.
2. Click **Skills**.
3. Click the **+** button, then choose **Add a new skill**.
4. Select `prompt-builder-SKILL.md` from your Desktop.

Claude imports the file and installs it in the right place for you. This is how you'll install every skill going forward - remember this flow.

Remember, you do have the prompt builder file in the ZIP folder you downloaded earlier, if you get really stuck.

### 2c. Start a new Cowork chat

Start a new Cowork chat so the skill gets loaded. You can delete the file from your Desktop now if you want, Claude has its own copy.

## Step 3: Decide what skill you want to build

Pick something specific you do regularly where the quality would improve if Claude followed a consistent approach. Good first skills:

- A brainstorming skill that asks hard questions about your product ideas
- A pitch deck reviewer that critiques your slides against startup best practices
- An email triager that flags what needs action from a summary of your inbox
- A meeting prep assistant that turns a calendar invite into a one-page brief
- A writing reviewer that cuts fluff from your drafts in your specific voice

For this walkthrough, we'll use **"a product brainstorming sparring partner"** as the example. Replace it with whatever you actually want.

## Step 4: Trigger the prompt-builder skill

In your new Cowork chat, type `/` and you'll see a list of available skills - `/prompt-builder` should be in there. You can invoke any skill directly with slash syntax like this. Paste this into your chat (replace the bit in `[SQUARE BRACKETS]` with your own skill idea):

```
/prompt-builder I want to build a Claude skill that [WHAT THE SKILL SHOULD DO, e.g. "acts as a sharp product brainstorming sparring partner, asking hard questions and pushing back on assumptions the way a VC would"]. Interview me about what I need, then produce the skill instructions as the final output.
```

The slash command is the cleanest way to trigger a skill. You can also just describe what you want in plain English and Cowork will usually pick the right skill based on the description in its frontmatter - but `/skill-name` is more reliable.

Cowork will invoke prompt-builder and start interviewing you. It asks about:

- The role Claude should play
- The specific outcome you want
- Background context it should know
- Hard rules (what it must always/never do)
- Output format
- Examples of good vs bad responses

Answer each question with whatever specificity you can. Short answers are fine - prompt-builder is good at making them work.

**When the interview finishes**, prompt-builder will assemble and show you a structured prompt. This is the "brain" of your skill.

## Step 5: Turn the prompt into a skill file

First, get Cowork to wrap the prompt with proper frontmatter. In the same chat, say:

```
Wrap that prompt as a Claude skill file. Add frontmatter with name, description, and trigger phrases that should activate this skill, then show me the full file contents.
```

The result will look something like this:

```markdown
---
name: product-brainstormer
description: Acts as a sharp product brainstorming sparring partner. Use when the user wants to think through a new product idea, stress-test an assumption, or needs pushback on their thinking. Trigger phrases include "brainstorm", "think through", "push back on this idea".
---

# Product Brainstormer

You are a [role]...
```

Now you need to actually save it. There are three ways - the first is the easiest:

### Option A (recommended): Add it via the Customise menu

1. In the Claude desktop app, click **Customise** (bottom-left of the sidebar), then **Skills**.
2. Click the **+** button and choose **Add a new skill**.
3. Select the SKILL.md file from your computer.

Claude imports the file and installs it in the right place for you. No file paths to remember, no command line. This is how you should add every skill you build going forward.

If you need a file on your computer first, ask Cowork: `Save that skill file to my Desktop as SKILL.md so I can import it via Customise.` Then do the three steps above.

### Option B: Let Cowork offer to save it

When you show Cowork a skill file in chat, it will often offer to save it to your skills folder automatically. If it does, just say yes.

### Option C: Ask Cowork to save it directly

You can also just say:

```
Save that as %USERPROFILE%\.claude\skills\[skill-name]\SKILL.md. Use all-lowercase with hyphens for the folder name, no spaces. Create the folder if it doesn't exist.
```

Cowork will write the file straight to the right location. Good for quick iteration once you're comfortable.

## Step 6: Verify the skill is in place

In the same Cowork chat, ask:

```
List the skills in %USERPROFILE%\.claude\skills\ and show me the contents of the SKILL.md you just created.
```

Cowork will list the folder and print the file. You should see `prompt-builder` and your new skill folder side by side, and the SKILL.md should have the frontmatter and prompt instructions you agreed on.

## Step 7: Test it

Start a **new** Cowork chat (so it picks up the newly installed skill). Test it two ways:

1. **Slash command (most reliable):** type `/` and pick your skill from the list, or type `/your-skill-name` directly.
2. **Natural language:** say something that matches one of the trigger phrases in your skill's description, e.g. "Brainstorm with me on a new product idea - a subscription box for home cocktail kits."

If the skill is loaded correctly, Cowork will follow the workflow you designed (asking hard questions, pushing back, etc.) instead of giving a generic response.

**If natural language doesn't trigger the skill:** the description in the frontmatter isn't catching your phrase. Go back to Cowork and say: `Update %USERPROFILE%\.claude\skills\<your-skill>\SKILL.md - add more trigger phrases to the description so it catches phrases like "<your phrase>".` Then start a new Cowork chat and try again. (The slash command will still work even if the trigger phrases are weak.)

## Step 8: Iterate

Your first skill won't be perfect. After using it a few times, notice what's missing or wrong. Ask Cowork to edit the SKILL.md for you (e.g. "Update %USERPROFILE%\.claude\skills\product-brainstormer\SKILL.md to add a hard rule about always asking for unit economics"). Start a new Cowork chat to pick up the changes.

Common tweaks:

- Add examples of what good/bad output looks like
- Add hard rules ("never suggest we build the MVP before validating demand", "always ask about unit economics")
- Tighten the output format

---

## What to build next

Some ideas, in rough order of effort-to-value:

1. **An email response drafter** trained in your exact tone.
2. **A meeting prep skill** that structures your calendar invites into briefs.
3. **A decision framework skill** that forces you to consider cost, time, risk, and reversibility for any call.
4. **A weekly review skill** that asks you questions to pull together what happened and what's next.

Each one takes 15-30 minutes to build and saves hours across a year.

**For ideas on what else to try:** open Claude Cowork and check the Ideas tab - it has prompts across work, creative, and personal use cases you can draw from.

---

## Recommended next action

Pick one skill that would make your week noticeably easier and build it right now. Once you've got two or three skills working comfortably, open `claude-code-setup-guide.md` - that's the next step in the kit, where you set up Claude Code and unlock the more powerful command line workflows.
