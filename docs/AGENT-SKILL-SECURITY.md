# Agent skill security checks

The SkillSpector workflow scans tracked SKILL.md directories (including bundled files) and standalone AGENTS.md, CLAUDE.md, and GEMINI.md instructions on pull requests, pushes to main, and manual runs.

It installs NVIDIA SkillSpector 2.12.0 from commit c7958a3268d9498644b22edb75d0f051bbc8cbfc. GitHub Actions are pinned to commit hashes. Python dependencies are resolved by pip and are not fully locked.

Scans use --no-llm, --fail-on-findings, and --fail-on-incomplete. Any active finding, incomplete scan, or scanner error fails the check. No LLM credentials are needed and no repository content is sent to an LLM. Dependency vulnerability checks may query OSV.

If no matching files exist, the check explicitly reports that no scan was performed. At setup time this repository had no matching agent skills or instructions. Skills installed outside the repository and remote references are outside this workflow's scope.

After merging, require the **SkillSpector agent skill scan** status check in the main branch's ruleset or branch protection settings to block merges on failure. The workflow itself does not change branch protection.

Review findings before changing policy; this setup does not automatically suppress or accept findings. Static scanning cannot guarantee that a skill is safe and does not replace application security, secret scanning, or dependency auditing.
