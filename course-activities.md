# Agentic AI Applications with Claude Code (TGS-2025052468)

## Step-by-Step Learner Activities

---

## Topic 1: Claude Code Fundamentals

### Activity 1.1: Installing Claude Code

**Objective:** Install Claude Code CLI on your operating system.

**For Mac:**

1. Open Terminal
2. Install Node.js (LTS version recommended):
   - Download from https://nodejs.org and run the installer
   - Or install via Homebrew:
     ```bash
     brew install node
     ```
   - Verify installation:
     ```bash
     node --version
     npm --version
     ```
3. Install Claude Code:
   ```bash
   npm install -g @anthropic-ai/claude-code
   ```
4. Verify installation:
   ```bash
   claude --version
   ```
5. Launch Claude Code for the first time:
   ```bash
   claude
   ```
6. Complete the authentication by logging in with your Anthropic account

**For Windows:**

1. Install Node.js (LTS version recommended):
   - Download the Windows installer from https://nodejs.org
   - Run the installer — ensure **"Add to PATH"** is checked during setup
   - Open PowerShell and verify:
     ```powershell
     node --version
     npm --version
     ```
2. Open PowerShell as Administrator
3. Install Claude Code:
   ```powershell
   npm install -g @anthropic-ai/claude-code
   ```
4. Verify installation:
   ```powershell
   claude --version
   ```

**Checkpoint:** Run `claude --version` and confirm the version number is displayed.

---

### Activity 1.2: Enabling Global Path on Windows

**Objective:** Configure Windows environment variables so `claude` command works from any directory.

**Steps:**

**Method 1 — CLI (Recommended):**

1. Open PowerShell as Administrator
2. Find where npm installs global packages:
   ```powershell
   npm config get prefix
   ```
   This typically returns `C:\Users\<YourName>\AppData\Roaming\npm`

3. Add the npm global path to your user PATH using `setx`:
   ```powershell
   setx PATH "$env:PATH;$(npm config get prefix)" /M
   ```
   Note: `/M` sets it for the system (requires Admin). Remove `/M` to set for current user only.

4. Close and reopen PowerShell for changes to take effect

5. Verify:
   ```powershell
   where.exe claude
   claude --version
   ```

**Method 2 — GUI:**

1. Press `Win + R`, type `sysdm.cpl`, press Enter
2. Go to the **Advanced** tab
3. Click **Environment Variables**
4. Under **System Variables**, find and select **Path**, then click **Edit**
5. Click **New** and add the npm global bin path:
   ```
   %APPDATA%\npm
   ```
6. Click **OK** on all dialogs to save
7. Close and reopen PowerShell
8. Verify:
   ```powershell
   where.exe claude
   claude --version
   ```

**Dependencies to verify:**

9. Check Node.js is installed:
    ```powershell
    node --version
    ```
10. Check npm is installed:
    ```powershell
    npm --version
    ```
11. Check Git is installed (needed later):
    ```powershell
    git --version
    ```
12. If Git is missing, install via CLI or download:
    ```powershell
    winget install --id Git.Git -e --source winget
    ```
    Or download from https://git-scm.com/downloads

**Checkpoint:** Run `claude --version` from a new PowerShell window opened in any directory.

---

### Activity 1.3: Installing Claude Code Extension on VS Code

**Objective:** Set up Claude Code within VS Code and organize the workspace.

**Steps:**

1. Open VS Code
2. Go to Extensions sidebar (`Ctrl+Shift+X` / `Cmd+Shift+X`)
3. Search for **"Claude Code"**
4. Click **Install** on the official Anthropic extension
5. After installation, you should see the Claude Code icon in the primary sidebar

**Moving to Secondary Side Bar:**

6. Right-click the Claude Code icon in the primary sidebar
7. Select **"Move to Secondary Side Bar"**
8. The secondary sidebar now appears on the right side of VS Code
9. You can toggle the secondary sidebar with `Ctrl+Alt+B` / `Cmd+Alt+B`

**Checkpoint:** Claude Code panel is visible in the secondary (right) sidebar of VS Code.

---

### Activity 1.4: Opening Claude Code Terminal in VS Code

**Objective:** Access Claude Code via the integrated terminal.

**Steps:**

1. Open VS Code terminal: `` Ctrl+` `` / `` Cmd+` ``
2. In the terminal, type:
   ```bash
   claude
   ```
3. Claude Code starts in interactive mode within the terminal
4. To open Claude Code in the secondary sidebar panel instead:
   - Click on the Claude Code icon in the secondary sidebar
   - Or use the Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`) and type **"Claude Code: Focus"**

**Moving Terminal Panel to Secondary Side Bar:**

5. Right-click on the Terminal tab at the bottom
6. Select **"Move Panel to Secondary Side Bar"** if you prefer the terminal alongside Claude Code

**Checkpoint:** Claude Code is running and responding to prompts in VS Code.

---

### Activity 1.5: Creating the .claude Project Structure

**Objective:** Set up the `.claude` folder with standard subfolders for agents, commands, hooks, and skills.

**Steps:**

1. Open your project folder in VS Code
2. Create the project directory:
   ```bash
   mkdir -p TGS-2025052468-Claude-Code
   cd TGS-2025052468-Claude-Code
   ```
3. Create the `.claude` folder structure:
   ```bash
   mkdir -p .claude/agents
   mkdir -p .claude/commands
   mkdir -p .claude/hooks
   mkdir -p .claude/skills
   ```
4. Verify the structure:
   ```bash
   ls -la .claude/
   ```
5. You should see:
   ```
   .claude/
   ├── agents/      # Custom agent definitions
   ├── commands/     # Custom slash commands
   ├── hooks/        # Pre/post action hooks
   └── skills/       # Installed skills
   ```

**Explanation of each folder:**

| Folder | Purpose |
|--------|---------|
| `agents/` | Custom AI agent definitions (e.g., UX reviewer, code reviewer) |
| `commands/` | Custom slash commands you can invoke with `/command-name` |
| `hooks/` | Scripts that run before or after Claude Code actions |
| `skills/` | Installed skill packs that extend Claude Code capabilities |

**Checkpoint:** Run `ls -R .claude/` and confirm all four subfolders exist.

---

### Activity 1.6: Creating the Lead Generation Web App

**Objective:** Build a lead generation web app using HTML/CSS/JavaScript with Apify and Playwright MCP integration.

**Steps:**

1. In your `TGS-2025052468-Claude-Code` folder, start Claude Code:
   ```bash
   claude
   ```

2. Create a `.env` file to store your secrets and tokens:
   ```
   Prompt: "Create a .env file with a placeholder for my Apify token"
   ```
   The `.env` file should contain:
   ```
   APIFY_TOKEN=your-apify-token-here
   ```
   Replace `your-apify-token-here` with your actual Apify API token.

3. Create a `.gitignore` file to prevent secrets from being pushed to GitHub:
   ```
   Prompt: "Create a .gitignore file that excludes .env, .mcp.json, 
   node_modules, and .DS_Store"
   ```
   The `.gitignore` file should contain:
   ```
   .env
   .mcp.json
   node_modules/
   .DS_Store
   ```

4. Configure MCP servers by creating `.mcp.json` (referencing the `.env` token):
   ```
   Prompt: "Add Apify and Playwright MCP servers to this project. My Apify token is [YOUR_TOKEN]"
   ```
   This creates `.mcp.json` with both servers configured.

5. Restart Claude Code to load the MCP servers

6. Ask Claude Code to create the web app:
   ```
   Prompt: "Create a lead generation web tool using HTML/CSS/JavaScript. 
   The tool should let users specify sectors, job titles, target groups 
   in Singapore. Include dark/light theme toggle. Use Apify Google Maps 
   scraper to find real business leads. Include CSV export functionality."
   ```

7. Claude Code will create the following files:
   - `index.html` — Main page with search form and results table
   - `style.css` — Styling with dark/light theme support
   - `data.js` — Singapore sectors, job titles, target groups
   - `app.js` — Application logic and Apify API integration
   - `export.js` — CSV export utility

8. Ask Claude Code to start the server and open it in your browser:
   ```
   Prompt: "Start a local server and open the app in my browser"
   ```
   Claude Code will run `npx serve` and open http://localhost:3000 for you.

9. Test the application:
   - Select a sector (e.g., "Information Technology & Software")
   - Select a job title (e.g., "CEO / Managing Director")
   - Enter keyword (e.g., "AI")
   - Click **Generate Leads**
   - Try the **Export CSV** button
   - Toggle between dark and light themes

**Checkpoint:** The web app loads, theme toggle works, and search form displays correctly.

---

### Activity 1.7: Setting Up CLAUDE.md Using /init

**Objective:** Generate a CLAUDE.md file that documents your project for future Claude Code sessions.

**Steps:**

1. In Claude Code, run the init command:
   ```
   /init
   ```

2. Claude Code will:
   - Analyze your entire codebase
   - Identify the tech stack and architecture
   - Document key patterns and conventions
   - Generate a `CLAUDE.md` file

3. Review the generated `CLAUDE.md` file in VS Code

4. The file should contain:
   - Project overview
   - How to run the app
   - Architecture description
   - Data flow explanation
   - Key patterns and conventions

5. Make any manual adjustments if needed:
   ```
   Prompt: "Update CLAUDE.md to include information about the Apify 
   actor ID we're using and the lead object schema"
   ```

**Checkpoint:** Open `CLAUDE.md` and verify it accurately describes your project.

---

### Activity 1.8: Memory Management Demo

**Objective:** Understand and practise different memory management commands in Claude Code.

**Demo 1 — `/clear` (Clear conversation)**

1. Have a conversation with Claude Code about your project
2. Type `/clear`
3. Notice the conversation history is wiped
4. Claude Code no longer remembers what you discussed
5. But it still reads `CLAUDE.md` for project context

**Demo 2 — `/compact` (Compress context)**

1. Have a long conversation with Claude Code (ask multiple questions, make edits)
2. Type `/compact`
3. Claude Code summarizes the conversation to free up context window space
4. Previous details are compressed but key decisions are retained
5. Useful when you're running low on context in a long session

**Demo 3 — `/new` (Start new conversation)**

1. Have a conversation with Claude Code about your project
2. Type:
   ```
   /new
   ```
3. This starts a completely new conversation without leaving Claude Code
4. All previous conversation context is discarded
5. Claude Code reads `CLAUDE.md` and `.mcp.json` automatically
6. No memory of previous conversations unless saved to memory files
7. Useful when you want to switch to a different task within the same session

**Demo 4 — `/resume` (Resume previous session)**

1. Exit Claude Code with `/quit`
2. Restart and immediately type:
   ```bash
   claude --resume
   ```
3. Or within Claude Code, use `/resume`
4. This restores your previous conversation context
5. Useful when you accidentally closed a session

**Demo 5 — `/rewind` (revert to past conversation)**

1. Ask Claude Code to make a change to a file:
   ```
   Prompt: "Add a new sector called 'Space Technology' to data.js"
   ```
2. After the change is made, type:
   ```
   /rewind
   ```
3. Claude Code shows a list of past conversation checkpoints
4. Select the checkpoint before the change was made
5. Claude Code reverts the conversation and any file changes back to that point
6. Useful when Claude Code goes down the wrong path and you want to undo multiple steps

**Checkpoint:** Successfully demonstrate each memory command and explain when to use each one.

---

### Activity 1.9: Creating a GitHub Account and Pushing Code to GitHub

**Objective:** Set up a GitHub account, install Git and GitHub CLI, authenticate, and push your project to a remote repository.

**Steps:**

**Part A — Create a GitHub Account:**

1. Go to https://github.com in your browser
2. Click **Sign up**
3. Enter your email address, create a password, and choose a username
4. Complete the verification and click **Create account**
5. Choose the **Free** plan
6. Complete the onboarding questions (optional — you can skip)

**Part B — Install Git:**

**For Mac:**

1. Open Terminal
2. Check if Git is already installed:
   ```bash
   git --version
   ```
3. If not installed, you have two options:
   - **Option A — Installer:** Download the Mac installer from https://git-scm.com/downloads/mac, run the `.dmg` file, and follow the on-screen instructions
   - **Option B — Terminal:** macOS will prompt you to install Xcode Command Line Tools when you run `git --version` — click **Install**
4. Verify installation:
   ```bash
   git --version
   ```
6. Configure your Git identity:
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your-email@example.com"
   ```

**For Windows:**

1. You have two options to install Git:
   - **Option A — Installer (Recommended):** Download the Windows installer from https://git-scm.com/downloads/win, run the `.exe` file, and follow the setup wizard
   - **Option B — CLI:** Open PowerShell as Administrator and run:
     ```powershell
     winget install --id Git.Git -e --source winget
     ```
2. During installation, accept the default settings:
   - Select **"Use Git from the Windows Command Line and also from 3rd-party software"**
   - Select **"Use the OpenSSL library"**
   - Select **"Checkout Windows-style, commit Unix-style line endings"**
3. Close and reopen PowerShell
5. Verify installation:
   ```powershell
   git --version
   ```
6. Configure your Git identity:
   ```powershell
   git config --global user.name "Your Name"
   git config --global user.email "your-email@example.com"
   ```

**Part C — Install GitHub CLI (gh):**

**For Mac:**

1. You have two options:
   - **Option A — Installer:** Download the `.pkg` installer from https://cli.github.com and run it
   - **Option B — Homebrew:**
     ```bash
     brew install gh
     ```
2. Verify:
   ```bash
   gh --version
   ```

**For Windows:**

1. You have two options:
   - **Option A — Installer (Recommended):** Download the `.msi` installer from https://cli.github.com and run it
   - **Option B — CLI:**
     ```powershell
     winget install --id GitHub.cli -e --source winget
     ```
2. Close and reopen PowerShell
3. Verify:
   ```powershell
   gh --version
   ```

**Part D — Authenticate GitHub CLI:**

1. Run the authentication command:
   ```bash
   gh auth login
   ```
2. You will be prompted with a series of questions:
   - **Where do you use GitHub?** → Select `GitHub.com`
   - **What is your preferred protocol for Git operations?** → Select `HTTPS`
   - **Authenticate Git with your GitHub credentials?** → Select `Yes`
   - **How would you like to authenticate GitHub CLI?** → Select `Login with a web browser`
3. Copy the one-time code displayed in the terminal
4. Press **Enter** — your browser will open to https://github.com/login/device
5. Paste the one-time code in the browser
6. Click **Authorize github** 
7. Return to the terminal — you should see `✓ Authentication complete`
8. Verify authentication:
   ```bash
   gh auth status
   ```
   You should see: `✓ Logged in to github.com as YourUsername`

**Part E — Push Your Project to GitHub:**

1. Navigate to your project folder:
   ```bash
   cd /path/to/TGS-2025052468-Claude-Code
   ```
2. Initialize a Git repository:
   ```bash
   git init
   ```
3. Verify `.gitignore` exists (created in Activity 1.6) to ensure `.env` and `.mcp.json` are excluded:
   ```bash
   cat .gitignore
   ```
   You should see `.env`, `.mcp.json`, `node_modules/`, and `.DS_Store` listed.
4. Stage all files:
   ```bash
   git add .
   ```
5. Create the first commit:
   ```bash
   git commit -m "Initial commit: Lead Generator SG web app"
   ```
6. Create a GitHub repository and push in one command:
   ```bash
   gh repo create TGS-2025052468-Claude-Code --public --source=. --push
   ```
7. Verify the push was successful:
   ```bash
   gh repo view --web
   ```
   This opens your new GitHub repository in the browser.

**Checkpoint:** Your GitHub repository is live, shows all project files, and the `.env` and `.mcp.json` files are NOT included (excluded by `.gitignore`).

---

## Topic 2: Tools and Commands

### Activity 2.1: Creating a Custom GitHub Push Command

**Objective:** Create a custom slash command that pushes code to GitHub, generates a README, sets up GitHub Pages via GitHub Actions, and updates the repo about section.

**Understanding custom commands:**
- Custom commands are markdown files stored in `.claude/commands/`
- Each `.md` file becomes a slash command (e.g., `github-push.md` → `/github-push`)
- The markdown content is the instruction Claude Code follows when the command is invoked

**Steps:**

1. In Claude Code, ask it to create the command:
   ```
   Prompt: "Create a custom slash command called 'github-push' in 
   .claude/commands/github-push.md that does the following in sequence:
   1. Generate or update a professional README.md with project description,
      features list, tech stack, setup instructions, and screenshots section
   2. Create a GitHub Actions workflow file at .github/workflows/deploy.yml 
      for GitHub Pages deployment (static HTML site)
   3. Stage all changes and commit with a descriptive message
   4. Push to GitHub
   5. Enable GitHub Pages in the repo settings using gh CLI 
      (gh api to set pages source to GitHub Actions)
   6. Update the repo description and topics using gh CLI 
      (gh repo edit --description and --add-topic)
   Print the live GitHub Pages URL at the end."
   ```

2. Review the generated command file:
   ```
   Prompt: "Show me the contents of .claude/commands/github-push.md"
   ```

3. The command file should look similar to this:
   ```markdown
   Push all changes to GitHub with full project setup:
   
   1. Generate or update README.md:
      - Add project title, description, and features
      - Add tech stack badges
      - Add setup and usage instructions
      - Add a screenshots section
   
   2. Create GitHub Pages deployment workflow:
      - Create .github/workflows/deploy.yml
      - Use actions/upload-pages-artifact and actions/deploy-pages
      - Trigger on push to main branch
   
   3. Stage and commit all changes:
      - git add .
      - git commit with a descriptive message
   
   4. Push to GitHub:
      - git push origin main
   
   5. Enable GitHub Pages:
      - Use gh api to configure Pages with GitHub Actions as source
   
   6. Update repo about section:
      - Set repo description using gh repo edit --description
      - Add relevant topics using gh repo edit --add-topic
      - Set homepage URL to the GitHub Pages URL
   
   7. Print the live GitHub Pages URL
   ```

4. Test the command:
   ```
   /github-push
   ```

5. Claude Code will execute each step and show progress

6. Verify each step completed:
   - Check README.md was created: open `README.md` in VS Code
   - Check GitHub Actions workflow: open `.github/workflows/deploy.yml`
   - Check GitHub repo: `gh repo view`
   - Check GitHub Pages deployment: `gh api repos/{owner}/{repo}/pages`

7. Visit your GitHub Pages URL (typically `https://yourusername.github.io/TGS-2025052468-Claude-Code/`)

8. Check the repo about section on GitHub — it should now show:
   - A description of the project
   - Topics like `html`, `css`, `javascript`, `lead-generation`, `singapore`
   - The live GitHub Pages URL as the homepage

**Checkpoint:** Run `/github-push` successfully — website is live on GitHub Pages, README is visible, and repo about section is updated.

---

### Activity 2.3: Adding MCP Tools — Apify and Playwright

**Objective:** Set up Apify and Playwright MCP servers from scratch.

**Steps:**

**Part A — Setting up Apify MCP:**

1. Open or create `.mcp.json` in your project root

2. Add the Apify MCP server configuration:
   ```json
   {
     "mcpServers": {
       "apify": {
         "command": "npx",
         "args": ["@apify/actors-mcp-server"],
         "env": {
           "APIFY_TOKEN": "your-token-here"
         }
       }
     }
   }
   ```

3. Restart Claude Code to load the server

4. Verify Apify tools are available:
   ```
   Prompt: "What Apify tools do you have access to?"
   ```

**Part B — Setting up Playwright MCP:**

5. Add Playwright to the same `.mcp.json`:
   ```json
   {
     "mcpServers": {
       "apify": { ... },
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest"]
       }
     }
   }
   ```

6. Restart Claude Code again

7. Verify Playwright tools are available:
   ```
   Prompt: "Navigate to http://localhost:3000 and take a screenshot"
   ```

**Checkpoint:** Both MCP servers are running and Claude Code can use their tools.

---

### Activity 2.4: Setting Up an Apify Account and Getting the Token

**Objective:** Create an Apify account and obtain an API token for integration.

**Steps:**

1. Go to https://console.apify.com in your browser

2. Click **Sign Up** (or log in if you already have an account)

3. Complete the registration process

4. After logging in, navigate to **Settings** in the left sidebar

5. Click on **API & Integrations**

6. Your **Personal API Token** is displayed here

7. Click **Copy** to copy the token

8. Update your `.mcp.json` with the real token:
   ```
   Prompt: "Update the Apify token in .mcp.json to [paste-your-token]"
   ```

9. Verify the token works by restarting Claude Code and running a test:
   ```
   Prompt: "Use Apify to search for 'coffee shops in Singapore' 
   and return the first 3 results"
   ```

**Important notes:**
- Free tier includes $5/month of platform credits
- The Google Maps Scraper actor charges per result
- Keep your token secure — don't commit it to public repos
- Add `.mcp.json` to `.gitignore` if it contains your token

**Checkpoint:** Apify returns real search results when tested through Claude Code.

---

## Topic 3: Skills and Agents

### Activity 3.1: Adding Skills from skills.sh

**Objective:** Install community skills to extend Claude Code capabilities.

**Steps:**

**Installing the GitHub README skill:**

1. In Claude Code, install the readme skill using the full URL:
   ```
   /install-skill https://skills.sh/skills/readme
   ```
   This downloads and installs the skill into your project.

2. Verify the skill was installed:
   ```bash
   ls .claude/skills/
   ```
   You should see the readme skill file.

**Installing the Frontend Design skill:**

3. Install the frontend design skill using the full URL:
   ```
   /install-skill https://skills.sh/skills/frontend-design
   ```

4. You can browse more community skills at https://skills.sh to find additional skills.

5. Verify skills are loaded:
   ```
   Prompt: "What skills do you have available?"
   ```

6. The skills should now appear in the available skills list when you start a new session

**Checkpoint:** Skills are installed and listed as available in Claude Code.

---

### Activity 3.2: Using Frontend Design Skill to Improve UI

**Objective:** Use the frontend design skill to enhance the Lead Generator app's visual design.

**Steps:**

1. Start the local server:
   ```bash
   npx serve
   ```

2. Invoke the frontend design skill:
   ```
   Prompt: "Use the frontend-design skill to review and improve the UI 
   of my Lead Generator SG app at http://localhost:3000. 
   Make it look more professional and polished."
   ```

3. Claude Code will:
   - Take screenshots of the current UI
   - Analyze the design
   - Suggest and implement improvements

4. Review the changes Claude Code proposes, such as:
   - Improved typography and spacing
   - Better color palette
   - Enhanced card shadows and borders
   - Improved button styles
   - Better table formatting
   - Loading animation improvements

5. Compare before and after by reviewing the CSS changes

6. Test the updated UI in your browser:
   - Check dark mode
   - Check light mode
   - Check mobile responsiveness (resize browser window)

**Checkpoint:** The UI looks noticeably more polished after the skill-driven improvements.

---

### Activity 3.3: Adding Custom Agents

**Objective:** Create UX/UI reviewer and code reviewer agents using the `/agents` command, then use them to improve the project.

**Understanding agents:**
- Agents are markdown files stored in `.claude/agents/`
- Each `.md` file defines an agent with a specific role, instructions, and tools it can use
- You invoke an agent with `@agent-name` followed by your prompt
- The `/agents` command provides an interactive way to create and manage agents

**Steps:**

**Creating the UX/UI Agent:**

1. In Claude Code terminal, type:
   ```
   /agents
   ```

2. Select **"Create a new agent"**

3. When prompted for the agent name, enter:
   ```
   ux-reviewer
   ```

4. When prompted for the agent description/instructions, enter:
   ```
   You are a UX/UI reviewer agent. Review web interfaces for:
   - Visual hierarchy and layout
   - Color contrast and accessibility (WCAG AA)
   - Responsive design
   - User flow and interaction patterns
   - Consistency in spacing, typography, and components
   
   Use Playwright to navigate to the app and take screenshots.
   Provide actionable improvement suggestions with specific CSS/HTML changes.
   ```

5. The agent file is created at `.claude/agents/ux-reviewer.md`

6. Verify the file was created:
   ```bash
   cat .claude/agents/ux-reviewer.md
   ```

**Creating the Code Reviewer Agent:**

7. Run the agents command again:
   ```
   /agents
   ```

8. Select **"Create a new agent"**

9. Enter the agent name:
   ```
   code-reviewer
   ```

10. Enter the agent description/instructions:
    ```
    You are a code reviewer agent. Review JavaScript code for:
    - Code quality and readability
    - Security vulnerabilities (XSS, injection)
    - Performance issues
    - Error handling
    - Best practices
    
    Provide specific line-by-line feedback with file paths and line numbers.
    Suggest concrete code fixes for each issue found.
    ```

11. The agent file is created at `.claude/agents/code-reviewer.md`

**Using the UX/UI Agent:**

12. Start the local server first:
    ```
    Prompt: "Start a local server for the app"
    ```

13. Invoke the UX agent using `@` syntax:
    ```
    @ux-reviewer Review the Lead Generator SG app at 
    http://localhost:3000 and suggest improvements
    ```

14. The agent will:
    - Navigate to the app using Playwright
    - Take screenshots
    - Analyze the UI
    - Provide specific improvement suggestions

15. Review and apply the suggested UI improvements

**Using the Code Reviewer Agent:**

16. Invoke the code reviewer agent:
    ```
    @code-reviewer Review app.js for security issues, 
    performance problems, and code quality
    ```

17. The agent will:
    - Read through the code files
    - Identify issues and improvements
    - Provide line-by-line feedback with fixes

18. Review and apply the suggested code improvements

**Managing Agents:**

19. To view all available agents, run:
    ```
    /agents
    ```
    This lists all agents in `.claude/agents/` with their descriptions.

**Checkpoint:** Both agents provide actionable feedback, and at least 3 improvements from each are applied.

---

### Activity 3.4: Working with Git Worktrees

**Objective:** Use Git worktrees to develop 3 features in parallel and merge them.

**Understanding worktrees:**
- A worktree creates a separate folder with its own copy of the project files on its own branch
- You can work on multiple features simultaneously without switching branches
- Each folder = its own branch, so you just `cd` into the folder to work on that feature
- Changes in one folder don't affect the others

**Steps:**

**Part A — Create the .trees folder and 3 worktrees:**

1. Ensure your current code is committed:
   ```bash
   git add .
   git commit -m "Base version before feature branches"
   ```

2. Create the `.trees` parent folder:
   ```bash
   mkdir .trees
   ```

3. Create 3 worktree subfolders — each command creates a folder AND a new branch (`-b`) automatically:
   ```bash
   git worktree add .trees/feature1 -b feature1
   git worktree add .trees/feature2 -b feature2
   git worktree add .trees/feature3 -b feature3
   ```

4. Verify the 3 worktrees are created:
   ```bash
   git worktree list
   ```
   You should see:
   ```
   /path/to/TGS-2025052468-Claude-Code                 abc1234 [main]
   /path/to/TGS-2025052468-Claude-Code/.trees/feature1  abc1234 [feature1]
   /path/to/TGS-2025052468-Claude-Code/.trees/feature2  abc1234 [feature2]
   /path/to/TGS-2025052468-Claude-Code/.trees/feature3  abc1234 [feature3]
   ```

5. Check the folder structure:
   ```bash
   ls .trees/
   ```
   You should see `feature1/`, `feature2/`, `feature3/` — each containing a full copy of your project files.

**Part B — Feature 1: Dark/Light Toggle Enhancement:**

6. Open the `feature1` folder in a new VS Code window:
   - File → Open Folder → navigate to `.trees/feature1`
   - Or from terminal: `code .trees/feature1`

7. Open the Claude Code terminal in this VS Code window

8. Give Claude Code the feature prompt:
   ```
   Prompt: "Improve the dark/light theme toggle:
   - Add a smooth transition animation when switching themes
   - Add an auto-detect system preference option
   - Store preference in localStorage
   - Add a sun/moon icon animation on toggle"
   ```

9. Once the changes are done, commit from the Claude Code terminal:
   ```
   Prompt: "Commit these changes with message: feat: enhanced dark/light 
   toggle with animations and system preference"
   ```

**Part C — Feature 2: Modify Search Fields:**

10. Open the `feature2` folder in another VS Code window:
    - File → Open Folder → navigate to `.trees/feature2`
    - Or from terminal: `code .trees/feature2`

11. Open the Claude Code terminal in this VS Code window

12. Give Claude Code the feature prompt:
    ```
    Prompt: "Add these new fields to the search form:
    - Company Size dropdown (1-10, 11-50, 51-200, 201-500, 500+)
    - Revenue Range dropdown (Under $1M, $1M-$10M, $10M-$100M, $100M+)
    - Year Established range (slider or dropdown)
    Update the search query builder and results table accordingly."
    ```

13. Commit the changes:
    ```
    Prompt: "Commit these changes with message: feat: added company size, 
    revenue range, and year established fields"
    ```

**Part D — Feature 3: Mobile Responsive:**

14. Open the `feature3` folder in another VS Code window:
    - File → Open Folder → navigate to `.trees/feature3`
    - Or from terminal: `code .trees/feature3`

15. Open the Claude Code terminal in this VS Code window

16. Give Claude Code the feature prompt:
    ```
    Prompt: "Make the website fully mobile-friendly:
    - Add a hamburger menu for mobile
    - Make the search form stack vertically on small screens
    - Make the results table horizontally scrollable on mobile
    - Add touch-friendly button sizes (min 44px)
    - Test at 375px, 768px, and 1024px widths"
    ```

17. Commit the changes:
    ```
    Prompt: "Commit these changes with message: feat: mobile responsive 
    design with hamburger menu"
    ```

**Part E — Merge all features back to main:**

18. Go back to the main project folder in VS Code:
    - File → Open Folder → navigate to your original `TGS-2025052468-Claude-Code` folder

19. Open the Claude Code terminal and merge all 3 branches:
    ```
    Prompt: "Merge the following 3 feature branches into main:
    - feature1
    - feature2
    - feature3
    If there are merge conflicts, resolve them."
    ```

20. Verify all features are working:
    ```
    Prompt: "Start the local server and open the app in the browser"
    ```

21. Clean up the worktrees:
    ```bash
    git worktree remove .trees/feature1
    git worktree remove .trees/feature2
    git worktree remove .trees/feature3
    ```

**Checkpoint:** All 3 features are merged into main and the app works with all enhancements.

---

### Activity 3.5: GitHub Actions App and Issue-to-PR Workflow

**Objective:** Install the GitHub Actions app for Claude Code, create issues, and use Claude to fix them via pull requests.

**Steps:**

**Installing GitHub Actions App:**

1. Go to https://github.com/apps/claude and click **Install**

2. Select the repository `TGS-2025052468-Claude-Code` (or all repositories)

3. Authorize the app

4. Verify installation:
   ```bash
   gh api repos/{owner}/TGS-2025052468-Claude-Code/installation
   ```

**Creating an Issue:**

5. Create a GitHub issue:
   ```bash
   gh issue create --title "Bug: Search results don't show total count in page title" \
     --body "When leads are generated, the browser tab title stays as 'Lead Generator SG'. 
   It should update to show the count, e.g., 'Lead Generator SG (25 leads)'.
   
   Steps to reproduce:
   1. Select any sector
   2. Click Generate Leads
   3. Look at the browser tab title
   
   Expected: Tab title shows lead count
   Actual: Tab title remains unchanged"
   ```

6. Note the issue number (e.g., #1)

**Triggering Claude via @claude in the GitHub Issue:**

7. Go to the GitHub issue you just created in your browser

8. In the issue comments, type:
   ```
   @claude Fix this issue. Update the browser tab title to show the lead 
   count when results are generated, e.g., "Lead Generator SG (25 leads)".
   ```

9. Claude will automatically:
   - Read the issue details
   - Create a new branch (e.g., `fix/tab-title-count`)
   - Implement the fix in `app.js`
   - Commit and push the changes
   - Create a pull request linking back to the issue

10. Wait a moment — you will see Claude respond in the issue comments with a link to the pull request

**Reviewing and Merging the Pull Request:**

11. Click the pull request link that Claude posted, or find it in the **Pull Requests** tab

12. Review the changes Claude made in the **Files changed** tab

13. If the changes look good, merge the pull request:
    - Click **Merge pull request** → **Confirm merge** in the GitHub UI
    - Or use the CLI:
      ```bash
      gh pr merge --squash
      ```

14. The issue will be automatically closed when the PR is merged

**Checkpoint:** The issue shows as closed, the PR is merged, and the fix is live on the main branch.

---

### Activity 3.6: Adding Hooks for Input Filtering and Output Formatting

**Objective:** Create hooks that pre-process search input and post-process Apify output.

**Steps:**

**Understanding Hooks:**

Hooks in Claude Code run scripts before or after specific tool calls. They are configured using the `/hooks` command in the Claude Code terminal.

- **PreToolUse** hooks run before a tool is called — useful for filtering or modifying input
- **PostToolUse** hooks run after a tool completes — useful for formatting or enriching output

**Part A — Pre-processing Hook (Filter Input):**

1. In the Claude Code terminal, type:
   ```
   /hooks
   ```

2. Select **"Create a new hook"**

3. When prompted for the hook type, select:
   ```
   PreToolUse
   ```

4. When prompted for the matcher (which tool to hook into), enter:
   ```
   mcp__apify
   ```
   This matches any Apify MCP tool call.

5. When prompted for the hook command, enter:
   ```
   node .claude/hooks/filter-input.js
   ```

6. The hook is now registered. Next, create the filter script:
   ```
   Prompt: "Create the hook script at .claude/hooks/filter-input.js that:
   - Reads the tool input from stdin (JSON format)
   - Extracts search query strings
   - Removes punctuation characters (!@#$%^&*()_+-={}[]|:;<>?,./)
   - Removes common stop words (the, a, an, is, are, was, were, in, on, at, to, for, of, with, and, or, but, not)
   - Trims extra whitespace
   - Outputs the cleaned input as JSON to stdout
   - Logs 'Input cleaned: [original] → [cleaned]' to stderr"
   ```

7. Test the hook by running a search with noisy input:
   ```
   Prompt: "Search for 'the!!! best AI and software companies... 
   in, the Singapore!!!' using Apify"
   ```

8. Verify the input was cleaned before being sent to Apify

**Part B — Post-processing Hook (Format Output):**

9. In the Claude Code terminal, type:
    ```
    /hooks
    ```

10. Select **"Create a new hook"**

11. When prompted for the hook type, select:
    ```
    PostToolUse
    ```

12. When prompted for the matcher, enter:
    ```
    mcp__apify
    ```

13. When prompted for the hook command, enter:
    ```
    node .claude/hooks/format-output.js
    ```

14. Create the formatting script:
    ```
    Prompt: "Create the hook script at .claude/hooks/format-output.js that:
    - Reads the tool output from stdin (JSON format)
    - Categorizes each lead:
      - 'high' quality (has email AND phone) — mark green
      - 'medium' quality (has email OR phone) — mark yellow  
      - 'low' quality (no contact info) — mark red
    - Adds a 'qualityScore' field to each lead object
    - Adds a 'qualityColor' field (#22c55e, #eab308, #ef4444)
    - Outputs the enhanced data as JSON to stdout
    - Logs the quality summary to stderr"
    ```

**Part C — Test the complete pipeline:**

15. Run a search to test both hooks together:
    ```
    Prompt: "Search for IT companies in Singapore using Apify"
    ```

16. Verify:
    - Input was cleaned (check stderr logs for "Input cleaned: ...")
    - Output has quality scores and color fields
    - Summary log shows "Results: X high quality, Y medium, Z low"

**Part D — Update the UI to show quality colors:**

17. Ask Claude Code to update the results table:
    ```
    Prompt: "Update the results table in the app to show a colored dot 
    next to each company name based on their qualityColor field. 
    Green dot = high quality lead, Yellow = medium, Red = low. 
    Add a legend above the table explaining the colors."
    ```

**Managing Hooks:**

18. To view all registered hooks, run:
    ```
    /hooks
    ```
    This lists all hooks with their type, matcher, and command.

**Checkpoint:** Input filtering removes noise, output formatting adds quality scores with colors, and the UI displays the color-coded quality indicators.

---

## Summary of All Activities

| Activity | Topic | Key Skill Learned |
|----------|-------|-------------------|
| 1.1 | Install Claude Code | CLI installation on Mac/Windows |
| 1.2 | Windows Path Setup | Environment variables and dependencies |
| 1.3 | VS Code Extension | Extension installation and sidebar layout |
| 1.4 | VS Code Terminal | Running Claude Code in VS Code |
| 1.5 | .claude Folder Setup | Project structure for agents, commands, hooks, skills |
| 1.6 | Lead Gen Web App | Building an app with HTML/CSS/JS + MCP tools |
| 1.7 | CLAUDE.md with /init | Project documentation for AI context |
| 1.8 | Memory Management | clear, compact, new, resume, rewind |
| 2.1 | Custom Commands | Creating and using slash commands |
| 2.2 | GitHub Push Command | Automated deployment workflow |
| 2.3 | MCP Tools Setup | Apify and Playwright configuration |
| 2.4 | Apify Account | API token setup and testing |
| 3.1 | Installing Skills | Adding community skills |
| 3.2 | Frontend Design Skill | AI-powered UI improvement |
| 3.3 | Custom Agents | UX/UI and code review agents |
| 3.4 | Git Worktrees | Parallel feature development and merging |
| 3.5 | GitHub Actions + Issues | Issue-to-PR workflow with Claude |
| 3.6 | Hooks | Input filtering and output formatting |
