# Squad Engineering Rules for Claude Code

This file contains specific rules and guidelines for Claude Code when working with the Squad Engineering framework.

## Core Principles

1. **Role Separation is Sacred**
   - Supervisor (Claude Opus) NEVER writes code
   - Role Agents (Claude Sonnet) ONLY work within their assigned scope
   - No agent reads another agent's plan or modifies their files

2. **Communication Protocol**
   - All inter-agent communication happens through `role-comm-*.md` files
   - Agents update their comm files after EVERY meaningful action
   - Supervisor reads all comm files during sync-up

3. **Task Boundaries**
   - Each agent works ONLY on files specified in their `role-plan-*.md`
   - Agents cannot create new tasks for themselves
   - Agents cannot modify supervisor files or other agents' plans

## Command Execution Rules

### When running `/analyze`:
- Read all existing squad files to understand current state
- Never generate code or make changes
- Output should be analytical and suggestive only

### When running `/define-feature`:
- Create comprehensive PRDs in `.squad/features/`
- Include clear MVP boundaries
- Define testing criteria
- Never include implementation code

### When running `/evaluate`:
- Read ALL role-plan and role-comm files from `.squad/`
- Check task completion against original plans
- Output clear pass/fail verdicts
- Never modify code or files

### When running `/generate-squad-role`:
- Update `.squad/squad-roster.md` with new members
- Create role-definition files in `.squad/`
- Update `.squad/supervisor-rules.md` if needed
- Each definition must include: Stack, Boundaries, Standards

### When running `/start-task`:
- Read ONLY your assigned role-plan-*.md
- Reset your role-comm-*.md for fresh start
- Work strictly within defined boundaries
- Update comm file after each subtask

### When running `/continue-task`:
- Read existing role-comm to understand progress
- Check off completed items in role-plan
- Continue from last checkpoint
- Never reset comm file when continuing

### When running `/sync-up`:
- Read all role-comm files
- Summarize progress and blockers
- Suggest reallocations if needed
- Never execute code changes

## File Conventions

1. **Naming**:
   - Role plans: `.squad/role-plan-<number>.md`
   - Communications: `.squad/role-comm-<number>.md`
   - Features: `.squad/features/feature-<kebab-case-name>.md`
   - Role definitions: `.squad/role-definition-<number>.md`

2. **Status Tracking**:
   - Use markdown checkboxes in task lists
   - Update comm files with timestamps
   - Mark blockers with ⚠️ emoji
   - Mark completions with ✅ emoji

3. **Code Style** (for Role Agents):
   - Follow existing project conventions
   - Commit after each meaningful change
   - Include inline documentation
   - Write tests alongside implementation

## Squad Workflow Enforcement

1. **Feature Loop**:
   ```
   analyze → define-feature → evaluate → generate-squad-role → start-task → sync-up
   ```

2. **Validation Gates**:
   - Features require PRD before squad generation
   - Agents require role-plan before starting
   - Sync-up required before major reallocations

3. **Token Optimization**:
   - Agents read minimal context (own plan + comm)
   - Supervisor batches reads during evaluation
   - Use templates to reduce repeated content

## Error Handling

- If an agent encounters a blocker: Document in comm file, continue other tasks
- If scope is unclear: Ask for clarification in comm file, await sync-up
- If files conflict: Never modify, document issue for supervisor

## Remember

Squad Engineering is about structured, scalable LLM development. Every action should reinforce:
- Clear boundaries
- Explicit communication
- Deterministic outcomes
- Human-like team dynamics