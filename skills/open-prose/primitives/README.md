# OpenProse Primitives

This directory contains foundational documents that are loaded into subagent sessions to ensure consistent behavior across the OpenProse VM.

## Files

| File | Purpose | When Loaded |
|------|---------|-------------|
| `session.md` | Context management, state handling, compaction guidelines | All subagent sessions |
| `memory.md` | In-context state management (narration protocol) | VM initialization |
| `disk.md` | File-system state management (.prose/ directory) | VM initialization |

## Design Philosophy

These primitives solve a fundamental problem: subagents spawned via the Task tool are stateless by default. They don't inherently know:
- Where they are in a larger workflow
- How to read persistent state from prior sessions
- How to write state that future sessions can use effectively

The primitives teach subagents these skills, enabling patterns like persistent agents and the captain's chair.

## Usage

The OpenProse VM automatically includes relevant primitives when spawning sessions. Program authors don't need to reference them explicitly.

For persistent agents, the VM:
1. Loads `session.md` into the session context
2. Loads the agent's memory file
3. Provides the task context
4. At session end, prompts for memory compaction per the guidelines

## Adding New Primitives

Primitives should be:
- **Self-contained**: Understandable without external references
- **Actionable**: Clear instructions, not just concepts
- **Tested**: Verified to produce consistent subagent behavior
- **Minimal**: Only what's needed—don't bloat session context
