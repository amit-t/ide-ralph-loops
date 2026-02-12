# 🚂 Ralph Wiggum for Windsurf

> *"I'm helping!"* — Ralph Wiggum

This repository contains the "Ralph" harness for Windsurf. The Ralph approach transforms Windsurf into an autonomous worker by running it in a feedback loop with a persistent task list.

## � How to Use

See the [Windsurf Guide](./windsurf/README.md) for detailed setup and usage instructions.

## 🏗️ Deep Initialization (Large Projects)

For complex projects where generating a full backlog in a single pass would hit LLM token limits (truncating `prd.json`), use the **Deep Init** workflow.

**The "Architect-Builder" Workflow:**

1. **Phase 1 (The Architect):** Analyzes the request and "locks in" a plan by identifying 6 distinct functional groups (e.g., Auth, API, Database).
2. **Phase 2 (The Builders):** Iteratively expands each group in separate agent loops, writing safe "partial" task files to avoid context overflow.
3. **Phase 3 (The Assembly):** A bash-controlled merge step combines all partial files into a guaranteed valid `prd.json`.

**How to run:** Run the `/ralph-deep-init` workflow in Windsurf Chat.

## 🔄 The Ralph Loop Logic

1. **Analyze** context (read RULES.md, prd.json, and progress log)
2. **Select** highest priority incomplete task from prd.json
3. **Execute** implementation for the selected task
4. **Verify** with tests or typechecks (retry up to 3 times if needed)
5. **Record** success in prd.json (mark task complete) and progress log
6. **Commit** changes to git with descriptive message
7. **Repeat** until all tasks complete or max iterations reached

> [!NOTE]
> I made this for my own use, but I think it's a good idea to share it with the community. PRs are welcome!

## 🤝 Credits

- Inspired by [Matt Pocock's video](https://www.youtube.com/watch?v=_IK18goX4X8)
- Based on the [Ralph workflow by Ghuntley](https://ghuntley.com/ralph/)


