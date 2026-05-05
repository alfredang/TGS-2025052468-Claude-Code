# Agentic AI Applications with Claude Code (TGS-2025052468)

## Step-by-Step Learner Activities

---

## Topic 1: Claude Code Fundamentals

### Activity 1.1: Install the Claude Code Extension on VS Code

**Objective:** Get Claude Code working inside VS Code — the easiest way to start.

**Steps:**

1. Open VS Code.
2. Open the Extensions sidebar (`Cmd+Shift+X` on Mac, `Ctrl+Shift+X` on Windows).
3. Search for **Claude Code** (publisher: Anthropic) and click **Install**.
4. Click the Claude Code icon in the activity bar — a sign-in prompt appears.
5. Sign in with your Anthropic account (Claude.ai subscription or API key).
6. Optional: right-click the Claude Code icon → **Move to Secondary Side Bar** so it lives on the right.

**Checkpoint:** The Claude Code panel is open and ready to chat in VS Code.

---

### Activity 1.2: Install Claude Code in the Terminal

**Objective:** Install the Claude Code CLI so you can run `claude` from any terminal.

**Steps:**

1. Make sure Node.js (LTS) is installed. Check with:
   ```bash
   node --version
   ```
   If missing, download from https://nodejs.org.

2. Install Claude Code globally:
   ```bash
   npm install -g @anthropic-ai/claude-code
   ```

3. Verify:
   ```bash
   claude --version
   ```

4. Launch it from a project folder:
   ```bash
   claude
   ```

**Windows note:** if `claude` is not recognized after install, close and reopen PowerShell. If still missing, add `%APPDATA%\npm` to your PATH.

**Checkpoint:** `claude --version` prints a version number.

---

### Activity 1.3: Create the Project Folder and `.claude` Structure

**Objective:** Set up a clean project for the bride-booking app.

**Steps:**

1. Create the project folder and open it in VS Code:
   ```bash
   mkdir bride-booking
   cd bride-booking
   code .
   ```

2. In Claude Code, ask:
   ```
   Create folders .claude/agents, .claude/commands, .claude/hooks, and .claude/skills
   ```

**Checkpoint:** All four folders exist under `.claude/`.

---

### Activity 1.4: Build the Bride-Booking Landing Page

**Objective:** Use Claude Code to build a single-page bridal photography booking website with a booking form.

**Steps:**

1. In Claude Code, paste this prompt:
   ```
   Build a single-page bridal photography booking website in one index.html file
   (HTML + CSS + JS inline). Sections: Hero, About, Packages (3 cards), Gallery,
   Booking Form, Contact. The booking form fields: Full Name, Email, Phone,
   Preferred Date, Preferred Time, Package, Location, Number of People, Message.
   On submit, POST as JSON to https://formsubmit.co/ajax/your-email@example.com
   and show a success message. Use placeholder images from Unsplash.
   Style: elegant, romantic, blush pink + gold accents.
   ```

2. Start a local server and open the page:
   ```bash
   npx serve
   ```
   Visit http://localhost:3000.

3. Test by submitting a booking — you should see a success message.

**Checkpoint:** The landing page loads and the booking form works.

---

### Activity 1.5: Generate `CLAUDE.md` with `/init`

**Objective:** Create a project memory file so Claude understands the project in future sessions.

**Steps:**

1. In Claude Code, run:
   ```
   /init
   ```

2. Review the generated `CLAUDE.md` — it should describe the bride-booking site, its sections, and the form flow.

**Checkpoint:** `CLAUDE.md` exists and accurately describes the project.

---

### Activity 1.6: Memory Management Commands

**Objective:** Learn the everyday memory commands.

Try each one in Claude Code:

| Command | What it does |
|---------|--------------|
| `/clear` | Wipes the current conversation |
| `/compact` | Summarises the conversation to free up context |
| `/new` | Starts a fresh conversation in the same session |
| `/resume` | Reopens your previous conversation |
| `/rewind` | Reverts the conversation (and file edits) to an earlier checkpoint |

**Checkpoint:** You can describe when to use each one.

---

### Activity 1.7: Push the Project to GitHub

**Objective:** Publish the bride-booking project to your own GitHub repo.

**Steps:**

1. Install Git and GitHub CLI if you haven't:
   - Mac: `brew install git gh`
   - Windows: `winget install Git.Git` and `winget install GitHub.cli`

2. Configure Git once:
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your@email.com"
   ```

3. Sign in to GitHub:
   ```bash
   gh auth login
   ```
   Choose **GitHub.com → HTTPS → Login with a web browser**, then paste the code shown in the terminal into the browser page that opens.

4. Create `.gitignore` to keep secrets out:
   ```
   .env
   .mcp.json
   node_modules/
   .DS_Store
   ```

5. Initialise, commit, and push in one go:
   ```bash
   git init
   git add .
   git commit -m "Initial commit: bride-booking site"
   gh repo create bride-booking --public --source=. --push
   ```

6. Open the new repo in your browser:
   ```bash
   gh repo view --web
   ```

**Checkpoint:** Your repo is live on GitHub and `.env` / `.mcp.json` are excluded.

---

## Topic 2: Tools and Commands

### Activity 2.1: Custom `/github-push` Slash Command

**Objective:** Create a reusable slash command that commits, pushes, and updates GitHub Pages — all in one step.

**Steps:**

1. In Claude Code, ask:
   ```
   Create .claude/commands/github-push.md as a custom slash command that:
   1. Stages all changes and commits with a clear message
   2. Pushes to the main branch
   3. Enables GitHub Pages (workflow source) using gh CLI
   4. Updates the repo description and topics
   5. Prints the live GitHub Pages URL
   ```

2. Run it:
   ```
   /github-push
   ```

3. Open the live URL Claude prints.

**Checkpoint:** The bride-booking site is live on GitHub Pages.

---

### Activity 2.2: Auto-Fill and Submit the Booking Form with Playwright MCP

**Objective:** Use the Playwright MCP server to drive a real browser — open the bride-booking page, fill the booking form, and submit it.

**Steps:**

1. Create `.mcp.json` in the project root:
   ```json
   {
     "mcpServers": {
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest"]
       }
     }
   }
   ```

2. Restart Claude Code so it loads the MCP server.

3. Make sure the site is running:
   ```bash
   npx serve
   ```

4. In Claude Code, ask:
   ```
   Use Playwright MCP to:
   1. Open http://localhost:3000
   2. Scroll to the booking form
   3. Fill in: Full Name "Jane Tan", Email "jane@example.com",
      Phone "98765432", Preferred Date next Saturday, Preferred Time "2pm",
      Package "Premium Pre-Wedding Shoot", Location "Gardens by the Bay",
      Number of People "2", Message "Looking forward to it!"
   4. Click Submit
   5. Take a screenshot of the success message
   ```

5. Watch Claude operate the browser and confirm the success state.

**Checkpoint:** The form was filled and submitted by Playwright, and a confirmation screenshot was captured.

---

## Topic 3: Skills and Agents

### Activity 3.1: Add a Project-Level Frontend-Design Skill (Rustic Retro Ero)

**Objective:** Create a project-scoped skill at `.claude/skills/frontend-design/` that redesigns the bride-booking site in a **rustic retro Ero** style — sepia palette, vintage serif type, aged paper textures, wax-seal buttons.

**Steps:**

1. In Claude Code, ask:
   ```
   Create .claude/skills/frontend-design/SKILL.md as a project-level skill.
   Frontmatter: name "frontend-design", description that triggers on the words
   rustic / retro / Ero / vintage / old-world.
   Body should describe a rustic retro Ero aesthetic:
   - Palette: sepia, cream, weathered ivory, dusty rose, faded gold, walnut
   - Vintage serif headings (Playfair Display) + typewriter body (Special Elite)
   - Aged paper background, subtle grain, vignette
   - Hand-drawn floral flourishes, art-nouveau dividers
   - Sepia/duotone filter on gallery images, slight tilt for Polaroid feel
   - Wax-seal style buttons
   Include implementation steps that use Playwright MCP to screenshot before/after.
   ```

2. Restart Claude Code so it picks up the new skill.

3. Verify it loaded:
   ```
   What skills are available?
   ```
   You should see `frontend-design` in the list.

4. Make sure the site is running (`npx serve`), then invoke the skill:
   ```
   Use the frontend-design skill to redesign the bride-booking site at
   http://localhost:3000 in a rustic retro Ero style.
   ```

5. Review the before/after screenshots Claude produces and the CSS changes applied.

**Checkpoint:** The bride-booking site now has a sepia, vintage, paper-textured look — and the booking form still works.

---

### Activity 3.2: Create a UX/UI Agent — Oriental Chinese Purple Redesign

**Objective:** Build a custom UX/UI agent and use it to redesign the bride-booking site in an oriental Chinese style with a purple palette.

**Steps:**

1. In Claude Code, run:
   ```
   /agents
   ```
   Choose **Create a new agent** and name it `ux-reviewer`.

2. Paste this as the agent's instructions:
   ```
   You are a UX/UI design agent specialising in oriental Chinese aesthetics.
   Use Playwright MCP to view the page, then redesign with:
   - A purple-dominant palette (deep violet, plum, lavender) with gold accents
   - Chinese-inspired motifs: cloud patterns, lattice borders, jade tones
   - Serif display font with a hint of brush-stroke feel for headings
   - Subtle red double-happiness or floral accents on package cards
   - Maintain elegance, romance, and full responsiveness
   Output concrete CSS/HTML edits and apply them.
   ```

3. Make sure the site is running (`npx serve`).

4. Invoke the agent:
   ```
   @ux-reviewer Redesign the bride-booking site at http://localhost:3000
   with an oriental Chinese style and a purple palette.
   ```

5. Review the changes in the browser.

**Checkpoint:** The site shows a purple oriental redesign and still works on mobile.

---

### Activity 3.3: Pre- and Post-Submit Hooks for the Booking Form

**Objective:** Add two project-level hooks under `.claude/hooks/`:

1. **PreToolUse** — validates the booking form data before the browser submits it.
2. **PostToolUse** — when the submission succeeds, plays a sound and uses TTS to announce *"Hurray, your form is submitted"*.

Both hooks are registered in `.claude/settings.json` and matched on Playwright MCP tool calls.

**Steps:**

**Part A — Create the validation pre-hook:**

1. Ask Claude Code:
   ```
   Create .claude/hooks/validate-booking.js that:
   - Reads tool input from stdin as JSON
   - If the input mentions booking-form fields (Full Name, Preferred Date, etc.),
     check: Full Name non-empty, Email matches an email regex, Phone has 8+ digits,
     Preferred Date is today or later, Number of People is a positive integer
   - On failure, print errors to stderr and exit with code 2 to block the tool call
   - Otherwise pass input through unchanged
   ```

**Part B — Create the success-celebration post-hook:**

2. Ask Claude Code:
   ```
   Create .claude/hooks/booking-success-tts.sh that:
   - Reads stdin
   - If the output mentions a successful booking submission
     (e.g. "success", "thank you", "booking confirmed")
   - Play /System/Library/Sounds/Glass.aiff with afplay
   - Use `say -v Samantha "Hurray, your form is submitted"` for TTS
   - Always pass the original output through unchanged
   Make the script executable.
   ```

3. Make the shell script executable:
   ```bash
   chmod +x .claude/hooks/booking-success-tts.sh
   ```

**Part C — Register both hooks:**

4. Ask Claude Code:
   ```
   Create .claude/settings.json that registers:
   - PreToolUse hook on matcher "mcp__playwright" running
     "node $CLAUDE_PROJECT_DIR/.claude/hooks/validate-booking.js"
   - PostToolUse hook on matcher "mcp__playwright" running
     "bash $CLAUDE_PROJECT_DIR/.claude/hooks/booking-success-tts.sh"
   ```

5. Restart Claude Code so both hooks load. Verify:
   ```
   /hooks
   ```
   Both should be listed.

**Part D — Test the full pipeline:**

6. Make sure the site is running (`npx serve`).

7. Test the **pre-hook** with bad data:
   ```
   Use Playwright to fill the booking form with an empty Full Name and submit it.
   ```
   The hook should block the submission and print validation errors.

8. Test the **post-hook** with valid data:
   ```
   Use Playwright to fill the booking form with valid details and submit it.
   ```
   You should hear the Glass sound and Samantha saying *"Hurray, your form is submitted"*.

**Checkpoint:** Invalid bookings are blocked; successful bookings trigger the sound + TTS announcement.

---

### Activity 3.4: Git Worktrees — Three Parallel Improvements

**Objective:** Use Git worktrees to develop three improvements to the bride-booking site in parallel and merge them.

**Steps:**

1. Commit the current state:
   ```bash
   git add . && git commit -m "Base bride-booking site"
   ```

2. Create three worktrees, each on its own branch:
   ```bash
   git worktree add .trees/hero -b hero
   git worktree add .trees/gallery -b gallery
   git worktree add .trees/mobile -b mobile
   ```

3. Open each folder in a new VS Code window (`code .trees/hero`, etc.) and run Claude Code there with its own task:

   - **hero:** "Add a parallax effect and a video background option to the hero section."
   - **gallery:** "Turn the gallery into a lightbox carousel with keyboard navigation."
   - **mobile:** "Make the navigation a smooth-animating hamburger menu and ensure all sections look great at 375px width."

4. Commit in each worktree.

5. Back in the main folder, ask Claude Code:
   ```
   Merge the branches hero, gallery, and mobile into main.
   Resolve any conflicts.
   ```

6. Clean up:
   ```bash
   git worktree remove .trees/hero
   git worktree remove .trees/gallery
   git worktree remove .trees/mobile
   ```

**Checkpoint:** All three improvements are merged into `main`.

---

### Activity 3.5: GitHub Issues → Pull Requests with `@claude`

**Objective:** Install the Claude GitHub App and let Claude fix an issue automatically by tagging `@claude`.

**Steps:**

1. Install the app at https://github.com/apps/claude and grant access to your `bride-booking` repo.

2. In the repo, add a workflow file `.github/workflows/claude.yml` (Claude Code can write this for you):
   ```
   Create .github/workflows/claude.yml that runs the
   anthropics/claude-code-action@v1 on issue comments and PRs that mention @claude.
   ```

3. Set the auth secret on the repo:
   ```bash
   gh secret set CLAUDE_CODE_OAUTH_TOKEN
   ```
   Get the token by running `claude setup-token` locally.

4. Commit and push the workflow.

5. Create an issue:
   ```bash
   gh issue create --title "Add testimonials section" \
     --body "Add a testimonials section with 3 client quotes between Gallery and Booking Form."
   ```

6. On the issue page, comment:
   ```
   @claude please implement this
   ```

7. Wait — Claude will create a branch, push the change, and open a pull request linked to the issue.

8. Review and merge the PR.

**Checkpoint:** The issue is closed by a Claude-authored PR that's merged into `main`.

---

## Summary

| Activity | Topic | Key Skill |
|---|---|---|
| 1.1 | VS Code Extension | Install Claude Code in VS Code |
| 1.2 | Terminal CLI | Install `claude` CLI |
| 1.3 | Project Setup | Create `.claude` folders |
| 1.4 | Build the Site | Bride-booking landing page + form |
| 1.5 | `/init` | Generate `CLAUDE.md` |
| 1.6 | Memory | clear, compact, new, resume, rewind |
| 1.7 | GitHub | Push project to GitHub |
| 2.1 | Custom Command | `/github-push` slash command |
| 2.2 | MCP — Playwright | Auto-fill and submit the booking form |
| 3.1 | Skills | Install a community skill |
| 3.2 | Custom Agent | Oriental purple UX/UI redesign |
| 3.3 | Hooks | Pre-validate booking form data |
| 3.4 | Git Worktrees | Three parallel improvements |
| 3.5 | GitHub Actions | `@claude` issue-to-PR workflow |
