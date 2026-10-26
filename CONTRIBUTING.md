# Team Workflow

1. **Choose your issue.** Confirm the owner, reviewer and first deliverable. Read the linked block page.
2. **Create a branch.** Start from updated main. Use `schematic/power`, `pcb/control`, `docs/resources`, or another short task name.
3. **Check early.** Show your component choice and rough circuit to the reviewer before finishing the design.
4. **Do the work.** Put progress/questions in the issue. Agree interface changes with the owner on the other end.
5. **Open a PR.** Link the issue, describe the changes, attach a readable schematic PDF and request your reviewer.
6. **Review and merge.** Address comments and merge after approval. Close the issue when its deliverable is complete.

## Branch Commands

From a clean working tree:

```bash
git switch main
git pull --ff-only
git switch -c schematic/power
```

After editing, review `git status`, stage only intended files and commit:

```bash
git add path/to/changed-file
git commit -m "Add power schematic"
git push -u origin schematic/power
```

Replace the example path and branch name with your actual files/task. If Git reports conflicting local work or a rejected update, ask a lead before discarding anything.

## Issues and Reviews

- Assignee = person doing the work. Reviewer = person checking it.
- An issue does not automatically create a branch. Members can create one themselves.
- Put the reviewer username in the issue; request the formal review on the PR.
- Use `Related to #12` for partial work. Use `Closes #12` for the completing PR into main.
- A completed schematic issue does not mean hardware testing is complete.

## Hardware Rules

- Agree which sheet you own before editing. Coordinate top-level sheets, project settings, libraries and annotation with Integration.
- Do not change shared net names, connectors or voltages without agreement from affected owners.
- Include part numbers, checked footprints, relevant calculations and an ERC result or explanation in the PR.
- Keep generated backups and temporary files out of commits. Keep required libraries and project source files in the repository.

[Setup](Docs/SETUP.md) · [Assignments](Docs/Blocks/README.md)
