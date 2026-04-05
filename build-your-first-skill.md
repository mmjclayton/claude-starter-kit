# Build Your First Skill

A step-by-step walkthrough for creating a custom Claude skill using the `prompt-builder` skill you just installed. This is where the real power kicks in.

## What's a skill and why does this matter

A skill is a set of instructions that teaches Claude a specific workflow - for example, "when I ask you to brainstorm a product idea, do it like a sharp VC asking hard questions." Once installed, you trigger the skill with a short phrase and Claude follows that workflow every time, consistently.

Claude comes with a lot of pre-built skills, but the ones tailored to YOUR work will always be the most valuable. Building your own takes about 15 minutes per skill. This walkthrough shows you how.

## What you'll do

1. Create a dedicated "Claude Config" project folder where all your Claude customisation lives.
2. Use the `prompt-builder` skill to design the instructions for a new skill.
3. Save the result as a proper skill file.
4. Install it so Claude loads it automatically.
5. Test it.

Total time: 15-20 minutes for your first one.

---

## Step 1: Create your Claude Config project

This is where you'll keep all your skill files, templates, and Claude-related experiments. Having one dedicated folder means nothing gets lost.

In Terminal:

```bash
mkdir -p ~/dev/claude-config
cd ~/dev/claude-config
```

(You can put it anywhere you like - `~/Documents/claude-config` works just as well. We're using `~/dev/` to keep it alongside your other projects.)

Optional: turn it into a Git repo so you can track changes to your skills over time.

```bash
git init
```

## Step 2: Decide what skill you want to build

Pick something specific you do regularly where the quality would improve if Claude followed a consistent approach. Good first skills:

- A brainstorming skill that asks hard questions about your product ideas
- A pitch deck reviewer that critiques your slides against startup best practices
- An email triager that reads your inbox summaries and flags what needs action
- A meeting prep assistant that turns a calendar invite into a one-page brief
- A writing reviewer that cuts fluff from your drafts in your specific voice

For this walkthrough, we'll use **"a product brainstorming sparring partner"** as the example. Replace it with whatever you actually want.

## Step 3: Start Claude Code in your project folder

```bash
claude
```

You should see the Claude Code prompt. It will pick up your `CLAUDE.md` automatically so it already knows how you work.

## Step 4: Ask prompt-builder to design your skill instructions

Paste this into Claude Code (replace the bit in `[SQUARE BRACKETS]` with your own skill idea):

```
Use the prompt-builder skill. I want to build a Claude skill that [WHAT THE SKILL SHOULD DO, e.g. "acts as a sharp product brainstorming sparring partner, asking hard questions and pushing back on assumptions the way a VC would"]. Interview me about what I need, then produce the skill instructions as the final output.
```

Prompt-builder will now interview you. It asks about:
- The role Claude should play
- The specific outcome you want
- Background context it should know
- Hard rules (what it must always/never do)
- Output format
- Examples of good vs bad responses

Answer each question with whatever specificity you can. Short answers are fine - prompt-builder is good at making them work.

**When the interview finishes**, prompt-builder will assemble and show you a structured prompt. This is the "brain" of your skill.

## Step 5: Turn the prompt into a skill file

A skill file is just a markdown file (`SKILL.md`) with a small header block (called frontmatter) at the top that tells Claude when to trigger the skill.

In the same Claude Code session, say:

```
Now wrap that prompt as a Claude skill file. Add frontmatter with name, description, and a list of trigger phrases that should activate this skill. Save it to my current directory as SKILL.md. Put the frontmatter between --- markers at the very top of the file.
```

Claude will write a SKILL.md file in your `claude-config` folder. It'll look something like this:

```markdown
---
name: product-brainstormer
description: Acts as a sharp product brainstorming sparring partner. Use when the user wants to think through a new product idea, stress-test an assumption, or needs pushback on their thinking. Trigger phrases include "brainstorm", "think through", "push back on this idea".
---

# Product Brainstormer

You are a [role]...
```

## Step 6: Install the skill so Claude loads it

Skills live in `~/.claude/skills/<skill-name>/SKILL.md`. Create a folder for your new skill and move the file into place:

```bash
mkdir -p ~/.claude/skills/product-brainstormer
cp SKILL.md ~/.claude/skills/product-brainstormer/SKILL.md
```

(Replace `product-brainstormer` with whatever name your skill has. Use all-lowercase with hyphens, no spaces.)

Verify:

```bash
ls ~/.claude/skills/
```

You should see your new skill folder in the list.

## Step 7: Test it

Exit Claude Code with `/exit`, then start a fresh session:

```bash
claude
```

Trigger your skill by asking Claude to do the thing it was built for. For the brainstorming example:

```
Brainstorm with me on a new product idea - a subscription box for home cocktail kits.
```

If the skill is loaded correctly, Claude will follow the workflow you designed (asking hard questions, pushing back, etc.) instead of a generic response.

**If the skill doesn't trigger:** the description in the frontmatter isn't catching your phrase. Edit `~/.claude/skills/<your-skill>/SKILL.md` and add more trigger phrases to the description.

## Step 8: Iterate

Your first skill won't be perfect. After using it a few times, notice what's missing or wrong. Go back into the SKILL.md file, edit the instructions, save. No reinstall needed - Claude picks up changes next session.

Common tweaks:
- Add examples of what good/bad output looks like
- Add hard rules ("never suggest we build the MVP", "always ask about unit economics")
- Tighten the output format

---

## What to build next

Some ideas, in rough order of effort-to-value:

1. **An email response drafter** trained in your exact tone.
2. **A meeting prep skill** that structures your calendar invites into briefs.
3. **A decision framework skill** that forces you to consider cost, time, risk, and reversibility for any call.
4. **A weekly review skill** that asks you questions to pull together what happened and what's next.

Each one takes 15-30 minutes to build and saves hours across a year.

**For ideas on what else to try:** open the Claude desktop app or claude.ai and check the Ideas tab - it has prompts across work, creative, and personal use cases you can draw from.

---

## Recommended next action

Pick one skill that would make your week noticeably easier and build it right now. The first one is the slowest. By the third, you'll be building them in 10 minutes.
