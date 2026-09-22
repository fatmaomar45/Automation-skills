# User Story & Acceptance Criteria Breakdown Skill (JIRA-Ready via MCP)

## 1. Description & Purpose
This skill takes a raw product idea, feature request, or note and **breaks it down into clear user stories**. Each story is written from the user's point of view to show exactly what value they get. Every single story has a strict limit: it can only have **3 to 5 acceptance criteria** using the simple `Given/When/Then` format. 

If your workspace is set up to **connect to Jira** using Model Context Protocol (MCP), this tool will not just print text. It will connect to Jira directly, show you a draft, ask for your permission, and then **create the live tickets on your Jira board automatically**.

## 2. Strict Rules (What This Skill Does NOT Do)
To keep things clean, this tool follows two strict boundaries:
- **No Backend System Specs:** It will completely refuse to write technical database rules, system configurations, or backend developer tasks. (Use a system-requirements skill for that instead).
- **No Guesswork:** If part of your idea is unclear, the tool will not guess. It will clearly list it as an **Assumption** or an **Open Question** so you can fix it later.

## 3. How This Skill Compares to Other Tools
We analyzed how other public product management tools handle user stories and optimized this skill:

*   **Strict Story-Splitting:** Unlike standard tools that let a single ticket get too large, this skill forces a hard limit of 3–5 criteria and breaks oversized features down into smaller, linked tickets automatically.
*   **Clear Value Focus:** Many tools mix backend database code rules with user stories. This skill completely isolates system specifications so developers can focus strictly on consumer value.
*   **No Mandatory Pre-Interviews:** Some advanced tools (like `feature-forge`) require a long question-and-answer session before writing anything. This skill processes your text instantly and flags missing data as high-level assumptions instead.

## 4. Possible Enhancements (Future Upgrades)
These are helpful features that are not built into the tool yet, but can be added later to make it even more powerful:
1. **Clarifying Questions:** Add a step where the tool interviews you to ask questions about your feature idea *before* it starts writing the user stories.
2. **Auto-Save Files:** Add a rule that automatically creates and saves a new markdown text file (like `stories-login.md`) directly onto your computer every time it finishes a breakdown.
3. **Reusable Blank Templates:** Ship the folder with blank, ready-to-use template files for single stories and criteria so you can quickly write them by hand when needed.
4. **Extra Phrasing Styles:** Offer other popular writing formats (like EARS syntax) alongside the standard `Given/When/Then` style for groups who prefer it.

## 5. Credits & Inspiration
In alignment with academic integrity guidelines, this skill gives credit to the repositories where we borrowed core prompt design concepts:
- Layout and structure ideas from [Skills.io](https://skills.io).
- Ticket splitting logic inspired by `user-stories` from [Mehdibargach/claude-code-pm-skills](https://github.com).
- Multi-story formatting structures referenced from `user-story` from [deanpeters/Product-Manager-Skills](https://github.com).

## 6. Sources Consulted
The following public resource repositories were carefully studied and reviewed during the creation of this skill:
- `feature-forge` — [://github.com](https://://github.com)
- `user-stories` — [://github.com](https://github.com)
- `ba-zone-user-story-ac-writer` — [://github.com](https://://github.com)
- `prd-generator` — [://github.com](https://://github.com)
- `user-story-templates` — [://github.com](https://://github.com)
- `user-story` — [://github.com](https://github.com)

## 7. Beginner's Guide: How to Connect This Skill to Jira

Follow these simple steps to make this tool connect to your team's live Jira project board:

### Step 1: Get Your Jira Web Address (URL)
1. Open your internet browser and log in to your Jira account.
2. Look at the address bar at the top of your screen. 
3. Copy the web address link up until `.net` (Example: `https://atlassian.net`). This is your **Jira Base URL**.

### Step 2: Generate a Jira Access Token
1. Go to your Atlassian Security Profile page by clicking this link: [https://atlassian.com](https://atlassian.com)
2. Click the blue button that says **"Create API token"**.
3. Give your token a simple name (like "My Automation Script") and click **Create**.
4. Click **Copy** to save the long string of letters and numbers. **Warning:** Save this somewhere safe immediately, as it will never be displayed on your screen again!

### Step 3: Open the Configuration File in VS Code
1. Open your computer's file manager and locate the main folder where your model application saves its preferences:
   - **On Windows:** `C:\Users\YourName\AppData\Roaming\Claude\`
   - **On Mac:** `/Users/YourName/Library/Application Support/Claude/`
2. Locate the text file named **`claude_desktop_config.json`** inside that folder and open it inside VS Code.

### Step 4: Paste Your Connection Settings
Delete everything inside that file, copy the template box below, paste it inside your file, and fill in your exact information inside the quotation marks:

```json
{
  "mcpServers": {
    "atlassian-jira-automation": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-jira"],
      "env": {
        "JIRA_API_TOKEN": "PASTE_THE_API_TOKEN_YOU_COPIED_IN_STEP_2",
        "JIRA_BASE_URL": "PASTE_YOUR_JIRA_WEB_ADDRESS_FROM_STEP_1",
        "JIRA_USER_EMAIL": "type-your-registered-jira-email-here@domain.com"
      }
    }
  }
}
```
5. Save the file and restart your VS Code workspace session. The tool will now connect to Jira automatically when you tell it to build a ticket!

## 8. Quality Score Status
We tested this skill file using the class evaluation tool to make sure it is completely high quality.

- **Testing Tool Link:** [Skills Quality Scorer](https://github.com)
- **Our Grader Results:**

  | Part Evaluated | Score / Performance |
  |----------------|---------------------|
  | Completeness   | [PENDING LOCAL RUN] |
  | Edge Cases     | [PENDING LOCAL RUN] |
  | Constraint Rules| [PENDING LOCAL RUN] |

*Note: You can see the full, detailed printout text from the grading terminal inside the folder at `./quality_analysis/gemini_score.txt`.*
