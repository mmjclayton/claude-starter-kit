# Claude Code Setup Guide (macOS)

Zero to Claude Code running on your Mac, start to finish.

**Before you start:** you should already have a Claude Pro or Max subscription and the Claude desktop app installed (per Step 1 of the README), and you should have built at least one custom skill in Cowork via `build-your-first-skill.md`. If not, do those first - they're quicker wins and get you comfortable with Claude before you open Terminal.

**A note on language:** this guide explains every technical term the first time it shows up. If you see a word in brackets after an acronym, that's the plain-English version. You don't need to memorise any of it - just follow the steps.

**Is anything in this guide risky to my Mac?** No. Everything here is safe. You're installing well-known, widely-used tools that millions of developers use every day. None of these commands will damage your computer, delete your files, or change anything you can't undo. Terminal looks intimidating but it's just a different way of giving your Mac instructions - the same instructions you'd give by clicking around in Finder, written as text.

Two things to keep in mind:

- **`sudo` is a command that runs something with administrator privileges.** You'll see it in a couple of troubleshooting steps. Only run `sudo` commands when this guide explicitly tells you to, and only paste `sudo` commands from trusted sources (like this guide, or the official documentation of a tool). Never paste a random `sudo` command from the internet without knowing what it does.
- **A couple of steps run install scripts from the internet** (Homebrew and nvm). These are the standard, official install methods for those tools - both are open source and trusted by the entire developer community. They're safe. The guide points out when this is happening and tells you where the script comes from.

**Claude is there to help you, every step of the way.** If you ever get nervous about a command, or anything in Terminal looks confusing, stop and ask Claude. You can:

- Paste any command into Claude (on claude.ai) and ask "what does this command do and is it safe?" - Claude will explain it in plain language.
- Take a screenshot of your Terminal window (press `Cmd + Shift + 4`, drag to select the area, release - the screenshot saves to your Desktop) and drop it into a Claude conversation. Claude can read what's on screen and tell you what's happening.
- Copy and paste whatever's in your Terminal (errors, output, anything) into Claude and ask "what does this mean and what should I do next?" Claude will walk you through it.

You don't need to struggle alone with any of this. If anything is unclear, unexpected, or just looks scary - screenshot it, paste it, ask. That's what Claude is for.

---

### Phase 1: Terminal and Xcode Command Line Tools

Get the Terminal app open and install Apple's base developer toolkit (a bundle of tools that Git, Homebrew, and other things we'll install depend on).

**Step 1: Open Terminal**

Terminal is a macOS app that lets you type commands directly to your computer instead of clicking buttons. Everything in this guide runs inside Terminal.

Press `Cmd + Space` (opens Spotlight, Mac's search bar), type `Terminal`, press Enter. A window with a blinking cursor will open. Paste commands with `Cmd + V`, run them with Enter.

**Step 2: Check your chip architecture**

Macs made since late 2020 use Apple's own chips ("Apple Silicon", called M1, M2, M3 or M4). Older Macs use Intel chips. A couple of commands later in this guide differ depending on which chip you have, so check now.

```bash
uname -m
```

Verify: `arm64` means Apple Silicon (newer Mac). `x86_64` means Intel (older Mac). Remember which one you are.

**Step 3: Install Xcode Command Line Tools**

Xcode Command Line Tools is Apple's free bundle of developer basics (a version of Git, compilers, and build tools). Homebrew needs these to work.

```bash
xcode-select --install
```

A small window will pop up on your screen (a GUI - Graphical User Interface - which just means a clickable window rather than something in Terminal). Click Install and accept the licence. Wait for it to finish (5-15 minutes depending on your internet speed).

Verify:

```bash
xcode-select -p
```

You should see `/Library/Developer/CommandLineTools`.

Troubleshooting:
- "command line tools are already installed" - you're fine, continue.
- Popup doesn't appear - run `sudo xcode-select --reset` then retry.

**Phase checkpoint:** Run `git --version`. You should see a version number like `git version 2.x.x`.

---

### Phase 2: Homebrew

Homebrew is macOS's package manager - a tool that installs other tools for you. Instead of hunting down installers on websites, you type `brew install <thing>` and it handles the rest.

**Step 1: Install Homebrew**

This command downloads the official Homebrew installer script from brew.sh (the real Homebrew project) and runs it. It's safe - it's the standard install method used by millions of developers.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

You'll be prompted for your Mac password (the one you use to log into your computer). Type it (nothing visible will appear as you type, that's normal for security) and press Enter.

**Step 2: Add Homebrew to your PATH**

PATH is a list your computer keeps of where to look for commands you type. We need to tell it where Homebrew lives, otherwise when you type `brew` later, your Mac won't find it. This is a once-off setup.

At the end of the install, Homebrew prints two "Next steps" commands. Apple Silicon and Intel Macs need different commands here - use the one that matches your chip from Phase 1.

Apple Silicon (arm64):

```bash
echo >> ~/.zprofile
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Intel (x86_64):

```bash
echo >> ~/.zprofile
echo 'eval "$(/usr/local/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/usr/local/bin/brew shellenv)"
```

Verify:

```bash
brew --version
```

You should see `Homebrew 4.x.x`.

Troubleshooting:
- "command not found: brew" - you skipped Step 2. Run the PATH commands above for your chip.
- Permission errors - run `sudo chown -R $(whoami) $(brew --prefix)/*`.

**Phase checkpoint:** Run `brew doctor`. "Your system is ready to brew" means you're done. Fix any warnings before continuing.

---

### Phase 3: Git and GitHub

Git is version control - it tracks every change you make to your files, like a super-powered undo history. GitHub is a website that stores Git projects online so you (and others) can access them from anywhere. We'll install Git, create a GitHub account, and connect them using the GitHub CLI (Command Line Interface - GitHub's official tool for working with GitHub from Terminal).

This phase sets up all three.

If you'd like a visual primer on Git and GitHub before jumping in, this YouTube playlist is a gentle, beginner-friendly introduction: https://www.youtube.com/watch?v=r8jQ9hVA2qs&list=PL0lo9MOBetEFcp4SCWinBdpml9B2U25-f. Optional - you can do the steps below without it.

**Step 1: Install the latest Git via Homebrew**

macOS ships an old Git. Replace it.

```bash
brew install git
```

Verify:

```bash
git --version
```

You should see `git version 2.4x.x` or higher (Homebrew's version, not Apple's).

**Step 2: Configure your Git identity**

Every time you save a snapshot of your work (called a "commit" in Git), it gets tagged with your name and email. Use the email you'll use for GitHub.

Replace `Your Name` and `you@example.com` with your actual details:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
```

Verify:

```bash
git config --global --list
```

You should see `user.name`, `user.email`, and `init.defaultBranch=main`.

**Step 3: Create a GitHub account (browser)**

Leave the terminal. Go to https://github.com/signup and create a free account. Use the same email you just configured in Git. Verify your email when GitHub prompts you. Come back to the terminal when done.

**Step 4: Install GitHub CLI**

The GitHub CLI (`gh`) is GitHub's official command line tool. It handles logging in, creating repos, and pushing code all from Terminal, so you don't need to manage SSH keys or passwords manually.

```bash
brew install gh
```

Verify:

```bash
gh --version
```

You should see a version number like `gh version 2.x.x`.

**Step 5: Log into GitHub**

This command walks you through logging in. It opens a browser window, you approve once, and your Mac is connected to your GitHub account from then on.

```bash
gh auth login
```

Answer the prompts with these choices (use arrow keys, press Enter to select):
- What account do you want to log into? → **GitHub.com**
- What is your preferred protocol for Git operations? → **HTTPS**
- Authenticate Git with your GitHub credentials? → **Yes**
- How would you like to authenticate GitHub CLI? → **Login with a web browser**

It will show you a one-time code. Press Enter to open the browser, paste the code when prompted, click Authorise, then return to Terminal.

Verify:

```bash
gh auth status
```

You should see `Logged in to github.com as <your-username>`.

Troubleshooting:
- Browser doesn't open automatically - copy the URL it prints (starts with `https://github.com/login/device`) and open it manually.
- "authentication required" errors later when pushing - run `gh auth login` again and pick "Yes" when asked about authenticating Git.

**Phase checkpoint:** `gh auth status` shows you logged in as your GitHub username, with both GitHub.com and Git operations authenticated.

---

### Phase 4: Node.js (via nvm)

Node.js is a program that lets your Mac run code written in JavaScript outside of a web browser. Claude Code itself is written in JavaScript and runs on Node.js, so we need to install it.

We'll install Node through `nvm` (Node Version Manager), a tool that lets you install different Node versions side by side and switch between them. This is the standard way developers manage Node and it'll save you headaches down the road if you ever work on projects that need different versions.

**Step 1: Install nvm**

This command downloads nvm's official installer from the nvm-sh GitHub project (the official home of nvm) and runs it. Safe - this is the standard way to install nvm. Run it exactly as-is:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

The installer adds a few lines to your shell config file (a hidden settings file that Terminal reads when it starts) so nvm loads automatically in future Terminal windows.

**Step 2: Load nvm in your current Terminal session**

Close and reopen Terminal, then verify nvm loaded:

```bash
nvm --version
```

You should see a version number like `0.40.1`.

Troubleshooting:
- "command not found: nvm" after reopening Terminal - run `source ~/.zshrc` to manually reload your shell config, then try again. If it still doesn't work, open `~/.zshrc` in VS Code (`code ~/.zshrc`) and check that there are lines starting with `export NVM_DIR` near the bottom.

**Step 3: Install the latest long-term support (LTS) version of Node**

LTS means "Long Term Support" - the most stable, production-ready version. Install it and tell nvm to use it by default:

```bash
nvm install --lts
nvm use --lts
nvm alias default 'lts/*'
```

Verify:

```bash
node --version
npm --version
```

You should see versions like `v22.x.x` (node) and `10.x.x` (npm - Node Package Manager, a tool for installing JavaScript programs that came along for free with Node).

**Phase checkpoint:** Both `node --version` and `npm --version` print version numbers, and `nvm current` shows the LTS version you just installed.

---

### Phase 5: Code Editor (VS Code)

A code editor is like a souped-up Word document for writing code - it has syntax highlighting, file browsing, and a built-in terminal. VS Code (Visual Studio Code, made by Microsoft) is the most popular one and works well with Claude Code.

VS Code is also what you'll use to open and edit Markdown files (`.md`) - plain text files with simple formatting that Claude uses for instructions, templates, and skills. Inside VS Code, pressing `Cmd + Shift + V` opens a formatted preview of any Markdown file. If you don't already have a dedicated tool for viewing text files, VS Code is all you need.

**Step 1: Install VS Code**

```bash
brew install --cask visual-studio-code
```

**Step 2: Add the `code` command to your shell**

This lets you type `code .` in Terminal to open the current folder in VS Code (a shortcut you'll use constantly).

Open VS Code from Spotlight (`Cmd + Space`, type `Visual Studio Code`, press Enter). Inside VS Code, press `Cmd + Shift + P` (this opens the Command Palette, a search bar for VS Code commands). Type `Shell Command: Install 'code' command in PATH` and press Enter.

Verify (back in terminal, close and reopen first):

```bash
code --version
```

You should see a version number.

Troubleshooting:
- "command not found: code" - the shell command didn't install. Re-run Step 2 from inside VS Code.

**Phase checkpoint:** `code --version` prints a version number.

---

### Phase 6: Install Claude Code

Install Claude Code and connect it to your Claude account (the one you set up in Step 1 of the README).

**Step 1: Install Claude Code**

```bash
npm install -g @anthropic-ai/claude-code
```

Verify:

```bash
claude --version
```

You should see a version number.

Troubleshooting:
- Permission errors - run `sudo chown -R $(whoami) $(brew --prefix)/*` then retry. Do not use `sudo npm install`.
- "command not found: claude" - close and reopen Terminal, then retry the verify command.

**Step 2: Log Claude Code into your Claude plan**

Start Claude Code:

```bash
claude
```

On first run, Claude Code will ask how you want to log in. Select "Claude account" (the option that uses your Claude.ai subscription). Do NOT pick the API key or Anthropic Console option - that's a separate pay-per-use billing method we're not using.

A web browser window will open. Log into claude.ai with the same account you subscribed with, click Authorise, and return to Terminal. It should confirm you're signed in.

Verify: After auth, Claude Code drops you into an interactive prompt showing your working directory. Type `/exit` to leave.

Troubleshooting:
- Browser doesn't open - copy the URL Claude Code prints in the terminal and paste it into your browser manually.
- "You need an active subscription" - your Pro/Max plan isn't active yet. Check https://claude.ai/settings/billing.
- Logged into the wrong Claude account - run `claude` to start a session, type `/logout` inside it, then start `claude` again to re-auth.

**Step 3: Pick your model**

Claude Code lets you switch between models the same way Cowork does. Inside a `claude` session, type:

```
/model
```

You'll see a list. For day-to-day work, pick **Sonnet 4.6** - it's fast and handles most tasks well. Switch to **Opus 4.6** when you're doing heavy reasoning, complex refactors, or long analysis tasks. Haiku is for quick, simple stuff. You can change model any time mid-session with `/model`.

If you skipped it, the "Which model should you use?" section in the README explains the trade-offs.

**Phase checkpoint:** Run `claude` from the terminal. You should see the Claude Code interactive prompt. Type `/model` to confirm you can see the model list, then `/exit`.

---

### Phase 7: Clone the Starter Kit

Get Matt's starter kit onto your Mac. This is your first real Git clone (downloading a repo from GitHub). It gives you a local copy of the starter kit files, including the CLAUDE.md template you'll install in this phase.

**Step 1: Clone the kit**

First, create a folder for your projects and move into it:

```bash
mkdir -p ~/code
cd ~/code
```

Now clone the repo. Run this command and **wait for it to finish** before running the next one:

```bash
git clone https://github.com/mmjclayton/claude-starter-kit.git
```

Once the clone completes (you'll see "done" and get your prompt back), move into the Mac folder:

```bash
cd claude-starter-kit/Mac
```

(`code` is just a suggested name for where you'll keep your projects - you can call it whatever you like, just use the same name in the later phases. `git clone` downloads a copy of the repo into a new folder. We then navigate into the `Mac` subfolder since that's where the Mac-specific files live.)

Verify:

```bash
ls
```

You should see `README.md`, `claude-code-setup-guide.md`, `CLAUDE.md`, `build-your-first-skill.md`, and a `skills/` folder.

Troubleshooting:
- "Repository not found" - double-check the GitHub username in the URL.
- "Permission denied (publickey)" - the URL uses HTTPS, not SSH, so this shouldn't happen. If it does, check you've copied the URL exactly.

**Step 2: Install your CLAUDE.md file**

CLAUDE.md is a file that teaches Claude how you like to work. It's loaded automatically at the start of every Claude Code session, so you only have to explain yourself once.

```bash
mkdir -p ~/.claude
cp CLAUDE.md ~/.claude/CLAUDE.md
code ~/.claude/CLAUDE.md
```

VS Code will open the file. Fill in every `[BRACKETED PLACEHOLDER]` with your own details (name, role, preferences, tools). Save with `Cmd + S` and close the window.

Verify: open Terminal and run:

```bash
cat ~/.claude/CLAUDE.md
```

(`cat` prints a file's contents to the screen.) You should see your filled-in file.

**Step 3: Test that CLAUDE.md is working**

```bash
claude
```

At the Claude Code prompt, type:

```
what do you know about how I like to work?
```

Claude should echo back the key points from your CLAUDE.md (your name, role, tone preferences). If it doesn't, your file isn't in the right place - check it's at `~/.claude/CLAUDE.md` exactly. Type `/exit` when done.

(The starter kit also contains the `prompt-builder` skill files. You already installed that skill directly in Cowork during `build-your-first-skill.md` - you don't need to install it again from here.)

**Phase checkpoint:** You have a cloned starter kit and a personalised CLAUDE.md that Claude reads automatically.

---

### Phase 8: End-to-End Validation

Create a project, push it to GitHub, and run Claude Code against it.

**Step 1: Create a project directory**

```bash
mkdir -p ~/code/hello-claude
cd ~/code/hello-claude
```

Quick translation of what just happened: `mkdir` means "make directory" (create a folder), `cd` means "change directory" (move into that folder), and `~` is shorthand for your home folder (the one with your name on it in Finder). So you just made a folder called `hello-claude` inside your `code` folder (created back in Phase 7) and stepped into it.

**Step 2: Create a Git repo and add a file**

A "repo" (repository) is just a folder that Git is tracking. `git init` turns this folder into one.

```bash
git init
echo "# hello-claude" > README.md
echo "console.log('hello from claude code');" > index.js
```

Verify:

```bash
ls
```

You should see `README.md` and `index.js`.

**Step 3: Make your first commit**

A commit is a saved snapshot of your work. `git add .` stages all your changes (adds them to the list of things to be saved), and `git commit` saves them with a message describing what you did.

```bash
git add .
git commit -m "initial commit"
```

Verify:

```bash
git log
```

You should see one commit with your name and email. Press `q` to exit the log.

**Step 4: Create a GitHub repo and push to it**

"Pushing" means uploading your local commits to GitHub so the code lives online as well as on your Mac. The `gh` CLI you installed in Phase 3 does all of this in one command - it creates the repo on GitHub, connects it to your local folder, and pushes your code up:

```bash
gh repo create hello-claude --public --source=. --remote=origin --push
```

What this command does, piece by piece: creates a new public repo on GitHub called `hello-claude`, connects it to your current folder (the `--source=.` bit means "this folder"), names the connection `origin` (a standard convention), and pushes all your commits up.

Verify: Run `gh repo view --web`. This opens the repo in your browser. You should see `README.md` and `index.js` listed.

Troubleshooting:
- "authentication required" - Phase 3 didn't complete properly. Run `gh auth login` again, making sure to pick "Yes" when asked about authenticating Git.
- "repository already exists" - you've already got a repo by that name on your GitHub account. Either delete it on github.com or pick a different name.

**Step 5: Run Claude Code against the project**

```bash
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

### Phase 9: Your First Real Project (Build Snake in 5 Minutes)

Prove the whole thing works by having Claude Code build a working game from a single prompt.

**Step 1: Create a new project folder**

```bash
mkdir -p ~/code/snake && cd ~/code/snake
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

```bash
open index.html
```

Verify: A browser tab opens with a working Snake game. Use arrow keys to move, spacebar to restart.

**Step 4: Iterate with Claude Code**

if you need to remember how to get to Claude code - open a Terminal and put in:

```bash
mkdir -p ~/code/snake && cd ~/code/snake
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

Push the Snake project to GitHub (`git init && git add . && git commit -m "snake game" && gh repo create snake --public --source=. --remote=origin --push`), then pick a real problem you want to solve and tell Claude Code to build it. You've now got both Claude Cowork (for everyday work and custom skills) and Claude Code (for coding and terminal-based workflows) set up. Use Cowork when you'd usually open a chat; use Claude Code when you want Claude working directly in your files and Terminal.

If you're stuck for what to do, remember, Claude Cowork is your friend. You could use /prompt-builder to write a prompt to review everything you've just set up, or help you brainstorm what to do next. You should give it the entire claude-starter-kit folder you started this journey with and tell it to analyse it for you, then ask it to suggest what you might do next!

The best thing you can do is keep playing around. Try things. Have fun.

BTW - you can play my version of the Snake game here: https://mmjclayton.github.io/snake/

Be good!