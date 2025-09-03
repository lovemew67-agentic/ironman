# LLM Instructions

You are an AI engineering assistant specialized in software development and automation. Follow the instructions below to complete the task and produce the required deliverables.

## 1. Task Context
- **Project Name:** `PayrollPlus`
- **Task Goal:** `Implement a “Supplementary Health Insurance Fee” calculator with CLI and tests`
- **Background & Constraints:**
  - Target users and use case: `HR staff in Taiwanese SMEs`
  - Tech stack & versions: `Node.js 20, TypeScript, Vitest`
  - Coding style & linting rules: `ESLint + Prettier, strict TypeScript`
  - Testing requirements: `Unit tests must cover core calculation functions and boundary conditions`
  - Performance or security considerations: `Calculation must complete within 100ms; input validation required`
  - Non-functional requirements: `CLI must support "--input" and "--output" flags`
- **References:**
  - Existing modules or APIs: `src/salary/core.ts`, `src/utils/validation.ts`
  - Related documentation: `docs/specs/health-insurance-supplement.md`

## 2) IO Settings
- **Input Directory:** `/workspace/tasks/inputs/hi-supplement-2025-09`
  - Example files: `case-001.json`, `case-002.json` (include fields such as employee bonuses and wages)
- **Output Directory:** `/workspace/tasks/outputs/hi-supplement-2025-09`
  - All new code, tests, and the final report should be placed here
- **Working Directory:** `/workspace/PayrollPlus`
- **Filename Conventions:**
  - Code: `src/hi-supplement/*.ts`
  - Tests: `tests/hi-supplement/*.test.ts`
  - Report: `TASK_REPORT.md`
- **Output Format:**
  - CLI executable:
    ```bash
    node dist/cli/hi-supplement.js --input input.json --output result.json
    ```

## 3) Tools
- **fs**: list `src` and `tests`, read the spec document
- **editor**: create `src/hi-supplement/calc.ts`, `cli/hi-supplement.ts`, `tests/hi-supplement/calc.test.ts`
- **shell**: run `npm i`, `npm run build`, `npm run test`, `npm run lint`
- **git**: run `init`, `add`, `commit -m "feat(hi): add supplement calculator with CLI and tests"`
- **Other tools:** None

## 4) Deliverables
- New code: `src/hi-supplement/calc.ts`, `cli/hi-supplement.ts`
- Tests: `tests/hi-supplement/calc.test.ts`
- Report: `/workspace/tasks/outputs/hi-supplement-2025-09/TASK_REPORT.md`

## 5) Process
1. Use `fs` to check existing directories and read the spec file
2. Design the calculation interface and input validation logic
3. Implement code with `editor`
4. Write tests and run them with `shell`
5. Fix issues until tests pass
6. Write `TASK_REPORT.md` and place all outputs in the output directory

## 6) Quality Gates
- Test coverage ≥ 80%
- Pass ESLint and Prettier checks
- CLI must return proper error codes and messages for invalid inputs

## 7) Constraints
- No external network calls
- Do not modify files in the input directory
- All results must be stored in the output directory

## 8) Action Log
- 14:02 → Used `fs` to list `src` and `tests`
- 14:06 → Used `editor` to create `calc.ts` and implement core logic
- 14:25 → Used `editor` to create `calc.test.ts`
- 14:33 → Used `shell` to run tests and fix errors
- 14:50 → Wrote `TASK_REPORT.md` and finalized outputs

## 9) Success Criteria
- `npm run build && npm run test` passes
- CLI can read `/workspace/tasks/inputs/hi-supplement-2025-09/case-001.json` and correctly output results to the output directory
- `TASK_REPORT.md` is complete and allows a reviewer to reproduce the task successfully
