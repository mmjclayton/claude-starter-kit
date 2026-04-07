# Claude Code Setup Guide (Windows)

Zero to Claude Code running on your Windows PC, start to finish.

**Before you start:** you should already have a Claude Pro or Max subscription and the Claude desktop app installed (per Step 1 of the README), and you should have built at least one custom skill in Cowork via `build-your-first-skill.md`. If not, do those first - they're quicker wins and get you comfortable with Claude before you open PowerShell.

**A note on language:** this guide explains every technical term the first time it shows up. If you see a word in brackets after an acronym, that's the plain-English version. You don't need to memorise any of it - just follow the steps.

**Is anything in this guide risky to my PC?** No. Everything here is safe. You're installing well-known, widely-used tools that millions of developers use every day. None of these commands will damage your computer, delete your files, or change anything you can't undo. PowerShell looks intimidating but it's just a different way of giving your PC instructions - the same instructions you'd give by clicking around in File Explorer, written as text.

Two things to keep in mind:

- **"Run as Administrator" is a way of running something with elevated privileges.** You'll see it in a couple of steps. Only run things as Administrator when this guide explicitly tells you to, and only use Administrator commands from trusted sources (like this guide, or the official documentation of a tool). Never paste a random command from the internet into an Administrator window without knowing what it does.
- **A couple of steps install tools using winget or standard Windows installers.** These are the official install methods for those tools - all are well-known and trusted by the entire developer community. They're safe. The guide points out when this is happening and tells you where the installer comes from.

**Claude is there to help you, every step of the way.** If you ever get nervous about a command, or anything in PowerShell looks confusing, stop and ask Claude. You can:

- Paste any command into Claude (on claude.ai) and ask "what does this command do and is it safe?" - Claude will explain it in plain language.
- Take a screenshot of your PowerShell window (press `Win + Shift + S`, drag to select the area, release - the screenshot saves to your clipboard and you can paste it) and drop it into a Claude conversation. Claude can read what's on screen and tell you what's happening.
- Copy and paste whatever's in your PowerShell (errors, output, anything) into Claude and ask "what does this mean and what should I do next?" Claude will walk you through it.

You don't need to struggle alone with any of this. If anything is unclear, unexpected, or just looks scary - screenshot it, paste it, ask. That's what Claude is for.

---

### Phase 1: PowerShell and winget

Get PowerShell open and confirm winget (Windows' built-in package manager) is available.

**Step 1: Open PowerShell**

PowerShell is a Windows app that lets you type commands directly to your computer instead of clicking buttons. Everything in this guide runs inside PowerShell.

Press the `Windows` key (or click the Start menu), type `PowerShell`, and click **Windows PowerShell**. A window with a blinking cursor will open. Paste commands with `Ctrl + V`, run them with Enter.

**Step 2: Check winget is available**

winget is Windows' built-in package manager - a tool that installs other tools for you. Instead of hunting down installers on websites, you type `winget install <thing>` and it handles the rest. It comes pre-installed on Windows 10 (version 1809+) and Windows 11.

```powershell
winget --version
```

You should see a version number like `v1.x.xxxxx`.

Troubleshooting:
- "winget is not recognized" - you may need to update the App Installer from the Microsoft Store. Search for "App Installer" in the Microsoft Store, click Update, then close and reopen PowerShell.

**A note on winget's first run:** the first time you use winget to install something, it will ask you to agree to Microsoft Store source agreements (terms of transaction, geographic region, etc.). Type `Y` and press Enter. This only happens once - after that, winget installs won't ask again.

**A note on installer prompts:** some winget installs will trigger a Windows "Do you want to allow this app to make changes to your device?" popup (called UAC - User Account Control). Click **Yes** to let the installer proceed. This is normal Windows behaviour for any software install.

**Phase checkpoint:** `winget --version` prints a version number.

---

### Phase 2: Git and GitHub

Git is version control - it tracks every change you make to your files, like a super-powered undo history. GitHub is a website that stores Git projects online so you (and others) can access them from anywhere. We'll install Git, connect your GitHub account (or create one if you don't have one), and set up the GitHub CLI (Command Line Interface - GitHub's official tool for working with GitHub from PowerShell).

If you'd like a visual primer on Git and GitHub before jumping in, this YouTube playlist is a gentle, beginner-friendly introduction: https://www.youtube.com/watch?v=r8jQ9hVA2qs&list=PL0lo9MOBetEFcp4SCWinBdpml9B2U25-f. Optional - you can do the steps below without it.

**Step 1: Install Git**

```powershell
winget install Git.Git
```

> **IMPORTANT: Close and reopen PowerShell now.** Windows needs a fresh PowerShell window to recognise newly installed commands. If you skip this, the next step will fail.

Verify:

```powershell
git --version
```

You should see `git version 2.4x.x` or higher.

**Step 2: Configure your Git identity and GitHub account**

Every time you save a snapshot of your work (called a "commit" in Git), it gets tagged with your name and email. Pick the path that matches your situation:

**Path A: I already have a GitHub account**

Use the email address associated with your existing GitHub account:

```powershell
git config --global user.name "Your Name"
git config --global user.email "your-github-email@example.com"
git config --global init.defaultBranch main
```

**Path B: I don't have a GitHub account yet**

Leave PowerShell. Go to https://github.com/signup and create a free account. Pick an email address and verify it when GitHub prompts you. Come back to PowerShell when done, then configure Git with the same email you just signed up with:

```powershell
git config --global user.name "Your Name"
git config --global user.email "your-new-github-email@example.com"
git config --global init.defaultBranch main
```

**Both paths - verify:**

```powershell
git config --global --list
```

You should see `user.name`, `user.email`, and `init.defaultBranch=main`.

**Step 3: Install GitHub CLI**

The GitHub CLI (`gh`) is GitHub's official command line tool. It handles logging in, creating repos, and pushing code all from PowerShell, so you don't need to manage SSH keys or passwords manually.

```powershell
winget install GitHub.cli
```

> **IMPORTANT: Close and reopen PowerShell now.** Same as before - Windows needs a fresh window to pick up the new `gh` command.

Verify:

```powershell
gh --version
```

You should see a version number like `gh version 2.x.x`.

**Step 4: Log into GitHub**

This command walks you through logging in. It opens a browser window, you approve once, and your PC is connected to your GitHub account from then on.

```powershell
gh auth login
```

Answer the prompts with these choices (use arrow keys, press Enter to select):
- What account do you want to log into? - **GitHub.com**
- What is your preferred protocol for Git operations? - **HTTPS**
- Authenticate Git with your GitHub credentials? - **Yes**
- How would you like to authenticate GitHub CLI? - **Login with a web browser**

It will show you a one-time code. Press Enter to open the browser, paste the code when prompted, click Authorise, then return to PowerShell.

Verify:

```powershell
gh auth status
```

You should see `Logged in to github.com as <your-username>`.

Troubleshooting:
- Browser doesn't open automatically - copy the URL it prints (starts with `https://github.com/login/device`) and open it manually.
- "authentication required" errors later when pushing - run `gh auth login` again and pick "Yes" when asked about authenticating Git.

**Phase checkpoint:** `gh auth status` shows you logged in as your GitHub username, with both GitHub.com and Git operations authenticated.

---

### Phase 3: Node.js

Node.js is a program that lets your PC run code written in JavaScript outside of a web browser. Claude Code itself is written in JavaScript and runs on Node.js, so we need to install it.

**Step 1: Install Node.js**

Download the LTS (Long Term Support) installer from the official Node.js website:

1. Go to https://nodejs.org and click **Get Node.js**.
2. You'll land on a download page. Ignore the version number at the top of the page and the preselected options (these default to Docker, which isn't what we want). Instead, click the **Windows Installer** button to download the `.msi` file.
3. Run the downloaded `.msi` installer. Accept all defaults and click through to finish.

> **IMPORTANT: Close and reopen PowerShell now.** Same as before - Windows needs a fresh window to pick up the new `node` and `npm` commands.

**Step 2: Allow PowerShell to run scripts**

Windows blocks scripts by default, which will prevent npm (and Claude Code later) from working. Run this command first to fix it:

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

If it asks you to confirm, type `Y` and press Enter. This tells Windows to allow scripts that were created locally or from trusted sources. It only applies to your user account and is safe - it's the standard fix recommended by Microsoft. You only need to do this once.

**Step 3: Verify Node.js is installed**

```powershell
node --version
npm --version
```

You should see versions like `v22.x.x` (node) and `10.x.x` (npm - Node Package Manager, a tool for installing JavaScript programs that came along for free with Node).

You may see a notice saying "new minor version of npm available" with a link to update. Ignore this - the version you have is fine for everything in this guide.

Troubleshooting:
- "node is not recognized" - the installer didn't add Node to your PATH. **Close and reopen PowerShell.** If it still doesn't work, rerun the installer and make sure "Add to PATH" is ticked.

**Phase checkpoint:** Both `node --version` and `npm --version` print version numbers.

---

### Phase 4: Code Editor (VS Code)

A code editor is like a souped-up Word document for writing code - it has syntax highlighting, file browsing, and a built-in terminal. VS Code (Visual Studio Code, made by Microsoft) is the most popular one and works well with Claude Code.

VS Code is also what you'll use to open and edit Markdown files (`.md`) - plain text files with simple formatting that Claude uses for instructions, templates, and skills. Inside VS Code, pressing `Ctrl + Shift + V` opens a formatted preview of any Markdown file. If you don't already have a dedicated tool for viewing text files, VS Code is all you need.

**Step 1: Install VS Code**

```powershell
winget install Microsoft.VisualStudioCode
```

> **IMPORTANT: Close and reopen PowerShell now.** You know the drill by now.

**Step 2: Verify the `code` command works**

The VS Code Windows installer adds the `code` command to your PATH automatically, so you can type `code .` in PowerShell to open the current folder in VS Code (a shortcut you'll use constantly).

Verify:

```powershell
code --version
```

You should see a version number.

Troubleshooting:
- "code is not recognized" - **close and reopen PowerShell.** If it still doesn't work, rerun the VS Code installer and make sure "Add to PATH" is ticked during setup.

**Phase checkpoint:** `code --version` prints a version number.

---

### Phase 5: Install Claude Code

Install Claude Code and connect it to your Claude account (the one you set up in Step 1 of the README).

**Step 1: Install Claude Code**

```powershell
npm install -g @anthropic-ai/claude-code
```

Verify:

```powershell
claude --version
```

You should see a version number.

Troubleshooting:
- Permission errors - close PowerShell, right-click it in the Start menu, choose **Run as Administrator**, then retry the install command. Close the Administrator window afterwards and open a normal PowerShell for the rest of the guide.
- "claude is not recognized" - **close and reopen PowerShell**, then retry the verify command.

**Step 2: Log Claude Code into your Claude plan**

Start Claude Code:

```powershell
claude
```

On first run, Claude Code will ask you to choose a text style (dark mode, light mode, etc.) - pick whichever you prefer, it's purely cosmetic. It will then ask how you want to log in. Select "Claude account" (the option that uses your Claude.ai subscription). Do NOT pick the API key or Anthropic Console option - that's a separate pay-per-use billing method we're not using.

A web browser window will open. Log into claude.ai with the same account you subscribed with, and click Authorise. Once authorised, close the browser tab and go back to PowerShell. It will show you some security notes - read them if you like, then press Enter to continue.

Claude Code will then show your working directory (something like `C:\Users\YourName`) and ask if you trust this folder. Select **Yes** - this is your user folder and it's safe. Claude Code needs to trust a folder before it can read and write files in it.

Verify: After that, you should see a "Welcome Back" screen in PowerShell - this is the Claude Code prompt where you type instructions. Don't exit yet - we'll pick a model first.

Troubleshooting:
- Browser doesn't open - copy the URL Claude Code prints in PowerShell and paste it into your browser manually.
- "You need an active subscription" - your Pro/Max plan isn't active yet. Check https://claude.ai/settings/billing.
- Logged into the wrong Claude account - run `claude` to start a session, type `/logout` inside it, then start `claude` again to re-auth.

**Step 3: Check your model**

While you're still in the Claude Code prompt, type:

```
/model
```

You'll see a list. Claude Code defaults to **Opus 4.6** - the most capable model. Stick with it. If you ever find Opus is too slow for a quick task or you're burning through your usage quota, you can switch down to **Sonnet 4.6** (faster, lighter) or **Haiku 4.5** (fastest, simplest). You can change model any time mid-session with `/model`.

If you skipped it, the "Which model should you use?" section in the README explains the trade-offs.

Now type `/exit` to leave Claude Code and return to PowerShell.

**Phase checkpoint:** You've logged in, trusted your folder, picked a model, and seen the Claude Code prompt. Full connection verified.

---

### Phase 6: Clone the Starter Kit

Get Matt's starter kit onto your PC. This is your first real Git clone (downloading a repo from GitHub). It gives you a local copy of the starter kit files, including the CLAUDE.md template you'll install in this phase.

**Step 1: Clone the kit**

First, create a folder for your projects and move into it. Run these two lines:

```powershell
mkdir ~\code
cd ~\code
```

**How to type `~`:** on most keyboards, press `Shift` + the backtick key (`` ` ``), which is usually to the left of `1` on the number row, below `Esc`. On some keyboards (especially laptops) you may need a different combination like `Shift + Fn + Esc`. If you can't find it, type `tilde symbol` into a search engine for your specific keyboard layout, or just type the full path instead (e.g. `C:\Users\YourName\code` instead of `~\code`). In PowerShell, `~` is just shorthand for your user folder.

Now clone the repo. Run this command and **wait for it to finish** before running the next one:

```powershell
git clone https://github.com/mmjclayton/claude-starter-kit.git
```

Once the clone completes (you'll see "done" and get your prompt back), move into the Windows folder:

```powershell
cd claude-starter-kit\Windows
```

(`code` is just a suggested name for where you'll keep your projects - you can call it whatever you like, just use the same name in the later phases. `git clone` downloads a copy of the repo into a new folder. We then navigate into the `Windows` subfolder since that's where the Windows-specific files live.)

Verify:

```powershell
dir
```

You should see `README.md`, `claude-code-setup-guide.md`, `CLAUDE.md`, `build-your-first-skill.md`, and a `skills/` folder.

Troubleshooting:
- "Repository not found" - double-check the GitHub username in the URL.
- "Permission denied (publickey)" - the URL uses HTTPS, not SSH, so this shouldn't happen. If it does, check you've copied the URL exactly.

**Step 2: Install your CLAUDE.md file**

CLAUDE.md is a file that teaches Claude how you like to work. It's loaded automatically at the start of every Claude Code session, so you only have to explain yourself once.

```powershell
mkdir ~\.claude -Force
copy CLAUDE.md ~\.claude\CLAUDE.md
notepad $HOME\.claude\CLAUDE.md
```

Notepad will open the file. Fill in every `[BRACKETED PLACEHOLDER]` with your own details (name, role, preferences, tools). Save with `Ctrl + S` and close the window.

(`$HOME` is another way to write `~` in PowerShell - we use it here because Notepad doesn't understand `~` on its own.)

Verify: open PowerShell and run:

```powershell
cat ~\.claude\CLAUDE.md
```

(`cat` prints a file's contents to the screen.) You should see your filled-in file.

**Step 3: Test that CLAUDE.md is working**

```powershell
claude
```

At the Claude Code prompt, type:

```
what do you know about how I like to work?
```

Claude should echo back the key points from your CLAUDE.md (your name, role, tone preferences). If it doesn't, your file isn't in the right place - check it's at `~\.claude\CLAUDE.md` exactly. Type `/exit` when done.

(The starter kit also contains the `prompt-builder` skill files. You already installed that skill directly in Cowork during `build-your-first-skill.md` - you don't need to install it again from here.)

**Phase checkpoint:** You have a cloned starter kit and a personalised CLAUDE.md that Claude reads automatically.

---

### Phase 7: End-to-End Validation

Create a project, push it to GitHub, and run Claude Code against it.

**Step 1: Create a project directory**

```powershell
mkdir ~\code\hello-claude
cd ~\code\hello-claude
```

Quick translation of what just happened: `mkdir` means "make directory" (create a folder), `cd` means "change directory" (move into that folder), and `~` is shorthand for your user folder (the one with your name on it in File Explorer). So you just made a folder called `hello-claude` inside your `code` folder (created back in Phase 6) and stepped into it.

**Step 2: Create a Git repo and add a file**

A "repo" (repository) is just a folder that Git is tracking. `git init` turns this folder into one.

```powershell
git init
echo "# hello-claude" > README.md
echo "console.log('hello from claude code');" > index.js
```

Verify:

```powershell
dir
```

You should see `README.md` and `index.js`.

**Step 3: Make your first commit**

A commit is a saved snapshot of your work. `git add .` stages all your changes (adds them to the list of things to be saved), and `git commit` saves them with a message describing what you did.

```powershell
git add .
git commit -m "initial commit"
```

Verify:

```powershell
git log
```

You should see one commit with your name and email. Press `q` to exit the log.

**Step 4: Create a GitHub repo and push to it**

"Pushing" means uploading your local commits to GitHub so the code lives online as well as on your PC. The `gh` CLI you installed in Phase 2 does all of this in one command - it creates the repo on GitHub, connects it to your local folder, and pushes your code up:

```powershell
gh repo create hello-claude --public --source=. --remote=origin --push
```

What this command does, piece by piece: creates a new public repo on GitHub called `hello-claude`, connects it to your current folder (the `--source=.` bit means "this folder"), names the connection `origin` (a standard convention), and pushes all your commits up.

Verify: Run `gh repo view --web`. This opens the repo in your browser. You should see `README.md` and `index.js` listed.

Troubleshooting:
- "authentication required" - Phase 2 didn't complete properly. Run `gh auth login` again, making sure to pick "Yes" when asked about authenticating Git.
- "repository already exists" - you've already got a repo by that name on your GitHub account. Either delete it on github.com or pick a different name.

**Step 5: Run Claude Code against the project**

```powershell
claude
```

At the Claude Code prompt, type:

```
read README.md and index.js, then tell me what this project does
```

Verify: Claude Code reads both files and gives you a summary mentioning `hello-claude` and the console.log line. This proves Claude Code can see your project files and respond in context.

Type `/exit` to leave.

**Final checkpoint:** You have a GitHub repo, committed code, and a working Claude Code session that reads your project. Full toolchain verified.

---

### Phase 8: Your First Real Project (Build Snake in 5 Minutes)

Prove the whole thing works by having Claude Code build a working game from a single prompt.

**Step 1: Create a new project folder**

```powershell
mkdir ~\code\snake -Force; cd ~\code\snake
claude
```

**Step 2: Give Claude Code the prompt**

At the Claude Code prompt, paste this exactly:

```
Build a single-file HTML Snake game in a file called index.html. Requirements: drawn on a canvas element, arrow keys to move, score display, game over screen with restart on spacebar, snake grows when it eats food, food spawns in random positions, dark background with a bright green snake. Display the controls underneath the game screen. Keep all CSS and JavaScript inline in the same HTML file. No external libraries.
```

Claude Code will ask permission to create the file. Approve it. It will write the whole game in one go (30-60 seconds).

**Step 3: Run it**

Exit Claude Code with `/exit`, then open the file in your browser:

```powershell
start index.html
```

Verify: A browser tab opens with a working Snake game. Use arrow keys to move, spacebar to restart.

**Step 4: Iterate with Claude Code**

If you need to remember how to get to Claude Code - open PowerShell and put in:

```powershell
cd ~\code\snake
claude
```

Run `claude` again in the same folder and try:

```
Add a high score that saves between sessions (using the browser's built-in storage), and make the snake speed up every 5 points.
```

Claude Code will edit the file for you. Refresh your browser tab to see the changes. This is the core Claude Code loop: describe what you want, review the changes it proposes, approve them, and run it.

**Phase checkpoint:** You've built, run, and modified a working app using only natural language. You're set up.

---

### Recommended next action

Push the Snake project to GitHub (`git init; git add .; git commit -m "snake game"; gh repo create snake --public --source=. --remote=origin --push`), then pick a real problem you want to solve and tell Claude Code to build it. You've now got both Claude Cowork (for everyday work and custom skills) and Claude Code (for coding and command line workflows) set up. Use Cowork when you'd usually open a chat; use Claude Code when you want Claude working directly in your files and PowerShell.

If you're stuck for what to do, remember, Claude Cowork is your friend. You could use /prompt-builder to write a prompt to review everything you've just set up, or help you brainstorm what to do next. You should give it the entire claude-starter-kit folder you started this journey with and tell it to analyse it for you, then ask it to suggest what you might do next!

The best thing you can do is keep playing around. Try things. Have fun.

Be good!
