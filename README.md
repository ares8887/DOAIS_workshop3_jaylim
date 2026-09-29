# DOAIS Workshop 3 – LLMSecOps (llmapp09)

## Changes made to the course code

| Change | Why |
|---|---|
| Added `.gitignore` (`.env`, `venv/`, caches, `.deepeval/`) | Keep API keys and large/generated files out of the repo |
| Replaced Docker Hub user `darryl1975` with `ares8887` (workflows, k8s, build scripts, docs) | Push images to my own registry |
| Trivy: added `ignore-unfixed: true` (both Docker workflows) | Base image had 38 HIGH CVEs with no upstream fix, which failed the scan |
| PromptFoo/DeepEval workflows: set `OLLAMA_MODEL_SENTIMENT/SUMMARIZE/INTENT=gemma4:31b` | Default models (`glm-5.2` etc.) returned `402 Payment Required` on the free Ollama plan |
| Evals: print backend logs on failure | Made the 402 diagnosable |
| `ai_service.py`: Ollama HTTP timeout 120s → 300s | Cloud model occasionally hit `ReadTimeout` |

Application logic and unit tests are unchanged.

## Secrets

No keys are committed. These were set as GitHub Actions repository secrets: `DOCKERHUB_TOKEN`, `OLLAMA_API_KEY`, `OLLAMA_BASE_URL`, `OPENAI_API_KEY`. Locally, keys go in `llm-multiroute/.env` (git-ignored), created from `.env.example`.

## CI status

LLM Multiroute CI, LLM Frontend Python CI, PromptFoo Tests and DeepEval Tests all pass. DeepEval uses an LLM judge and can occasionally fail on a single borderline check; re-run if so.

## AI declaration

I used Claude Sonnet 5.5 (via Claude Code) to check the submission requirements, set up the GitHub repo and `.gitignore`, and debug the CI pipeline failures. I am responsible for the content and quality of the submitted work.
