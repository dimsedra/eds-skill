# eds-skill

A fork of [mattpocock/skills](https://github.com/mattpocock/skills). This CHANGELOG covers `eds-skill`-specific changes only. The full upstream history lives at [mattpocock/skills/CHANGELOG.md](https://github.com/mattpocock/skills/blob/main/CHANGELOG.md).

## 1.1.0 (2026–08-19)

**Architecture Upgrades:**

- **`/comprehend` Subagent-Driven HTML Generation**: Upgraded `/comprehend` to delegate HTML walkthrough report compilation to a clean-head subagent upon invocation. The subagent inspects code in an isolated context window with zero context pollution and writes standalone HTML modules directly to disk, keeping the main conversation stream light and fast for follow-up Q&A.
- **`/write-skills` Balancing (Invariants vs. Vanity Numbers)**: Refined the meta-skill to distinguish functional quantitative invariants (loop limits, token caps, 0 failing tests) from arbitrary vanity numbers, and deterministic state machines from checklist fixation.

## 1.0.0 (2026–08-03)

Initial fork.

**Curated down** (from upstream):

- Removed `misc/`, `personal/`, `in-progress/`, `deprecated/` skill buckets; only the promoted `engineering/` and `productivity/` buckets remain.
- Removed the `docs/`, `scripts/`, `.claude-plugin/`, `.agents/`, `.changeset/`, `.github/`, `.out-of-scope/` folders.
- Removed `package.json` and `package-lock.json`; distribution is via `npx skills`, not npm.
- Restructured: skills now live at `engineering/<name>/SKILL.md` and `productivity/<name>/SKILL.md` (not under a top-level `skills/` prefix).

**Renamed** (to drop upstream branding):

- `ask-matt` → `ask-skill` (Windows reserved name workaround; folder + slash command).
- `setup-matt-pocock-skills` → `setup-eds-skill` (folder + slash command).

**Added:**

- **`/comprehend`**: a new user-invoked engineering skill (originally `/own-it`). Build a private HTML comprehension journal for the code you ship. A near-twin of `/teach` where the primary source is your own codebase, the workspace is gitignored, and the agent informs rather than tests. The journal is the practice surface; the comprehension still has to be yours. See [engineering/comprehend/SKILL.md](./engineering/comprehend/SKILL.md).

**Attribution:** All wording, structure, and most skill designs are Matt Pocock's. The curation and the new `/comprehend` skill are the fork author's. The upstream `mattpocock/skills` repository remains the canonical source.
