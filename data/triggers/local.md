# Local Triggers

Install-specific triggers for this project. These do not travel with the Cortex DNA.
Format: same as cortex.md triggers (#### ::code, Purpose, Prompt to self).

---

#### ::release [version]
**Purpose:** Create a versioned release of Cortex. Bumps version, generates release notes, updates GitHub, refreshes vision/elevator pitch, and drafts an X post.
**Prompt to self:** This is a multi-step release workflow. Execute each step in order:

1. **Version bump.** If a version is provided (e.g., `::release 1.1.0`), use it. If no version is provided, determine the next version by reading the current version from cortex.md line 1 (`# Cortex vX.Y.Z`) and applying semver:
   - If only bug fixes and minor tweaks since last release → patch bump (X.Y.Z+1)
   - If new features or triggers added → minor bump (X.Y+1.0)
   - If breaking changes to DNA format → major bump (X+1.0.0)
   - Ask user to confirm the version before proceeding.

2. **Changelog scan.** Review the diary entries since the last release. Review data/projects/ for recently completed projects. Review git log if available. Compile a list of changes grouped by: Added, Changed, Fixed, Removed.

3. **Update cortex.md version.** Change the `# Cortex vX.Y.Z` header on line 1 to the new version.

4. **Generate release notes.** Create `data/releases/vX.Y.Z.md` with:
   - Version and date
   - Summary (2-3 sentences: what this release is about)
   - Changes grouped by category (Added/Changed/Fixed/Removed)
   - Migration notes if any DNA format changes affect existing installs
   Create the `data/releases/` directory if it doesn't exist.

5. **Update compatibility matrix.** If any platform test results changed since the last release (new T1-T6 scores, new platforms tested, verdict changes), update the compatibility matrix in both `README.md` (the "Platform Compatibility" section) and `docs/prd-agentic-platform-landscape.md` (the "Results Matrix" table). Update the "Last updated" timestamp in both locations. If no test results changed, skip and note "Compatibility matrix: unchanged."

6. **Update vision document.** Read `data/vision.md`. If the changes in this release meaningfully affect the project's purpose, scope, or elevator pitch, update it. If not, skip and note "Vision unchanged."

7. **Draft X post.** Create a draft post in the CMS announcing the release. Use the API: `POST /api/posts` with body `{ "content": "[post text]", "status": "draft", "type": "single" }`. Keep content under 280 characters. Tone: clear, factual, slightly excited. Include the version number. Set status to "draft" so the user can review before posting. If the CMS API is unavailable (e.g., server not running), skip and note "X post: skipped (CMS unavailable)."

8. **GitHub update.** Push `cortex.md` and `README.md` to GitHub per Behavioral Rule 10 — those are the only two files that ever exist in the repo. Use the GitHub integration (Octokit) to create a commit containing exactly those two files, with message "Release Cortex vX.Y.Z", and update the branch. Then create a GitHub Release object for the tag with the release notes in the description — a commit alone does not create a visible Release on GitHub. The release notes file (`data/releases/vX.Y.Z.md`) stays local only.

9. **Report.** Respond with:
   ```
   Released Cortex vX.Y.Z
   Release notes: data/releases/vX.Y.Z.md
   Changes: [N] added, [N] changed, [N] fixed, [N] removed
   Compatibility matrix: [updated / unchanged]
   Vision: [updated / unchanged]
   X post: [drafted / skipped]
   GitHub: [pushed / manual push needed]
   ```

#### ::releases
**Purpose:** List all releases.
**Prompt to self:** List all files in `data/releases/` sorted by version. Show version, date, and summary line for each. If no releases directory exists, respond: "No releases yet. Use `::release` to create one."
