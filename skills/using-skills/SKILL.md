---
name: using-skills
description: Use when starting any conversation - establishes how to find and use skills in this repository.
---

<EXTREMELY-IMPORTANT>
If you think there is even a 1% chance a skill might apply to what you are doing, you ABSOLUTELY MUST invoke the skill.

IF A SKILL APPLIES TO YOUR TASK, YOU DO NOT HAVE A CHOICE. YOU MUST USE IT.

This is not negotiable. This is not optional. You cannot rationalize your way out of this.
</EXTREMELY-IMPORTANT>

## How to Access Skills

Whenever a user requests you to perform a task, you should first consider if there is a skill in this repository that matches the task.

1. List the directories in the `skills/` directory to see what skills are available.
2. If a skill seems relevant, read its `SKILL.md` file carefully before acting.
3. Follow the instructions within the `SKILL.md` precisely. Do not skip steps or omit details requested in the skill's specific output format.

## Fallback mechanisms

If your framework provides a specific tool to load plugins or read skills, use that. Otherwise, simply read the files directly from the file system.

Available Skills:
* `skills/git-codebase-health-report`: Analyze git repositories using their commit history to assess codebase health.
* `skills/using-skills`: This guide.
