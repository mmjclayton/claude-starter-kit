# Claude Code Cheat Sheet (Mac)

Quick reference for everything you'll use regularly. Keep this open while you work.

---

## Opening Terminal

Press `Cmd + Space`, type `Terminal`, press Enter.

Paste commands with `Cmd + V`. Run them with Enter.

To open a new Terminal tab: `Cmd + T`. To close: `Cmd + W`.

---

## Navigating folders

| What you want to do | Command |
|---|---|
| See where you are | `pwd` |
| List files in current folder | `ls` |
| List files including hidden ones | `ls -a` |
| Go into a folder | `cd foldername` |
| Go back up one level | `cd ..` |
| Go to your home folder | `cd ~` |
| Go to a specific path | `cd ~/code/myproject` |
| Open current folder in VS Code | `code .` |
| Open current folder in Finder | `open .` |
| Create a new folder | `mkdir foldername` |

**Tip:** press `Tab` to autocomplete folder and file names. Type the first few letters and hit Tab - Terminal will fill in the rest. If nothing happens, hit Tab twice to see all the options.

---

## Starting and using Claude Code

| What you want to do | Command |
|---|---|
| Start Claude Code | `claude` |
| Start Claude Code in a specific folder | `cd ~/code/myproject` then `claude` |
| Exit Claude Code | `/exit` |
| Switch model | `/model` |
| Clear the conversation context | `/clear` |
| See all available commands | `/help` |
| See your current plan and usage | `/status` |

**The basic loop:**
1. `cd` into your project folder
2. Run `claude`
3. Describe what you want in plain English
4. Review what Claude proposes, approve or decline
5. `/exit` when done

---

## Common Claude Code commands to try

Once you're inside a `claude` session, you can say things like:

```
read README.md and tell me what this project does
```
```
create a file called notes.md and add a bullet list of the things we've discussed
```
```
look at index.html and add a dark mode toggle
```
```
what files are in this folder?
```

Claude Code can read, create, and edit files in the folder you started it from. It will always ask permission before making changes.

---

## Git basics

You don't need to memorise these - but they're handy once you've pushed your first project.

| What you want to do | Command |
|---|---|
| Check what's changed | `git status` |
| See recent commits | `git log --oneline -10` |
| Stage all changes | `git add .` |
| Save a snapshot (commit) | `git commit -m "describe what you did"` |
| Push to GitHub | `git push` |
| Pull latest from GitHub | `git pull` |

---

## Getting unstuck

**Command not found:**
Close Terminal and reopen it. Newly installed tools sometimes need a fresh window before they're available.

**Claude Code won't start:**
Run `claude --version` to check it's installed. If not, run `npm install -g @anthropic-ai/claude-code`.

**Logged into the wrong Claude account:**
Start `claude`, type `/logout`, then start `claude` again and re-authenticate.

**Something looks broken and you don't know why:**
Copy the error message, open claude.ai in your browser, and paste it in. Ask "what does this mean and what should I do?" Claude will walk you through it.

**Forgot what folder you're in:**
Run `pwd` - it prints your current location in full.

---

## Keyboard shortcuts (Terminal)

| Shortcut | What it does |
|---|---|
| `Ctrl + C` | Cancel the current command (stops anything running) |
| `Ctrl + L` | Clear the screen |
| Up arrow | Scroll back through previous commands |
| `Tab` | Autocomplete a file or folder name |
| `Cmd + T` | New Terminal tab |

## Editing what you type in command line

| Shortcut | What it does |
|---|---|
| `Ctrl + A` | Jump to start of line |
| `Ctrl + E` | Jump to end of line |
| `Ctrl + K` | Delete from cursor to end of line |
| `Ctrl + U` | Delete from cursor to start of line |
| `Ctrl + W` | Delete the word before the cursor |
| `Option + ←/→` | Move word by word |
