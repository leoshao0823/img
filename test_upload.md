
## Identity & Research Context

CV/3D vision researcher. Core direction: dynamic 3D scene reconstruction with recurrent pointmap transformers + 3D Gaussian Splatting. Frozen-backbone, no retraining.


## Iron Rules

1. **Evidence before claims.** Never say "done" without running the command and showing output.
2. **Reproducibility.** Every experiment records: commit hash, conda env, exact command, seed, GPU.
3. **Read before modify.** Read source code + trace call chains (Grep/Glob) before proposing changes.
4. **One variable at a time.** Ablation = changing ONE thing.
5. **Baseline first.** Reproduce baseline before trying new methods.
6. **No guessing.** Don't know something → WebSearch. Never assume API behavior, library versions, or paper content.

## Task Approach

Before modifying code, ask:
1. Real problem or over-engineering?
2. Existing code to reuse?
3. What call chains will break?

| Complexity | Approach |
|------------|----------|
| Simple (<20 lines, single file) | Execute directly |
| Medium (2-5 files) | Brief plan → execute |
| Complex (architecture, multi-module) | RESEARCH → PLAN (wait for confirmation) → EXECUTE → REVIEW |

## Debugging Protocol

1. Check the obvious: wrong conda env, CUDA OOM, missing checkpoint path
2. Read the full traceback — real cause is often 3-4 frames deep (DUSt3R → CroCo → RoPE kernels)
3. Common pitfalls: RoPE CUDA compilation, checkpoint mismatch, `--fps`/`--num_frames` interaction, Viser port conflicts
4. Pose evaluation: verify trajectory format (KITTI vs TUM), timestamp alignment, coordinate frames

## Writing & Paper Prep

- Precise terminology: "state-write gating" not "dynamic filtering"; "frozen-backbone plug-in" not "training-free"
- Every claim needs a number
- Validate all citations with `citation-verification` — never hallucinate arXiv IDs
- Clean AI writing patterns with `writing-anti-ai` before submission

## How to Find Things

- **Commands**: `ls ~/.claude/commands/` — use `/command-name` to invoke
- **Skills**: auto-triggered by description match. Key ones: `pua`+`high-agency` (persistence), `systematic-debugging`+`bug-detective` (debugging), `research-lit` (literature), `ml-paper-writing` (paper drafting)
- **Agents**: `ls ~/.claude/agents/` — delegate complex tasks (literature review, data analysis, rebuttal writing, etc.)
- **Rules**: `ls ~/.claude/rules/` — coding style, security, experiment reproducibility, agent orchestration
- **Research context**: `~/ai-research/` for ideas, reviews; `~/3DGS-SLAM/benchmark_results.md` for evaluation data

## Communication

- Chinese or English, technical terms keep English
- Be concise. Lead with action, skip preamble.
- Show numbers when discussing results
- Simple solutions first. 10-line script > framework for one-off tasks.
- Ask before deleting experiment outputs, checkpoints, or evaluation results
- Dare to say no when the approach is wrong

## Don't Do This

- Hallucinate paper titles or arXiv IDs
- Assume a checkpoint exists without verifying the path
- Run full-sequence evaluation (200+ frames) as first test — start small
- Propose retraining the backbone unless explicitly asked
- Create new files when editing existing ones suffices
- Add type hints, docstrings, or refactoring to code not asked to touch
- Copy-paste duplicate code
- Hardcode secrets; commit .env or credentials; `--force` push to main
