# GitHub Copilot Instructions — Generative AI Project Template

This project is a production-ready Python template for building scalable Generative AI applications. It emphasizes modularity, performance, and clarity. All Copilot suggestions must align with this structure and these principles.

---

## 📦 Folder Conventions

- `config/`: YAML files for model, logging, and prompt configurations  
- `src/`: Core application logic, organized by function or concern  
  - `llm/`: LLM wrapper clients (e.g. GPT, Claude) and utilities  
  - `prompt_engineering/`: Templates and few-shot logic  
  - `utils/`: Shared utilities like token counters or caching  
  - `handlers/`: Error handlers and exception logic  
- `data/`: Runtime data directories (cache, prompts, outputs, embeddings)  
- `examples/`: Simple scripts showing use of the core modules  
- `notebooks/`: Interactive prototyping and analysis notebooks  

---

## ✅ Rules for Code Suggestions

- Use **modular structure**: one function/class per purpose
- All logic must live inside `src/`, never in notebooks or top-level scripts
- Use `config/*.yaml` to manage parameters (never hardcode them)
- Validate any parsed config file with `pydantic.BaseModel` schemas
- Do not import one module from another across unrelated folders (e.g., `utils/` should not import from `llm/`)
- Use type hints everywhere (`def count_tokens(text: str) -> int:`)
- Include a docstring for every public function/class using **Google style**
- Use `pathlib.Path` for all file operations
- Use `logging` configured from `logging_config.yaml`, not `print()`
- Avoid hardcoding rate limits or API keys; load from config or environment variables
- Tests (if created) should use `pytest` and mock external calls

---

## 🧠 Prompt Engineering Guidelines

- Store reusable prompt templates in `config/prompt_templates.yaml`
- Few-shot or chain-of-thought logic should go in `prompt_engineering/`
- If generating prompts dynamically, provide examples using `src/prompt_engineering/templates.py`
- Include testable prompt injection logic (e.g., `format_prompt(name, context) -> str`)

---

## 📊 Data & Outputs

- Store all runtime outputs in `data/outputs/`, and inputs in `data/prompts/`
- Use `data/cache/` for cached responses (e.g., API calls)
- Use `data/embeddings/` to persist vectorized representations (if any)

---

## 🧪 Example Flow (Copilot Should Support)

When writing a new model client:
1. Place logic inside `src/llm/gpt_client.py` or equivalent
2. Define interface methods like `generate_response(prompt: str) -> str`
3. Use `src/utils/rate_limiter.py` to throttle requests
4. Log all requests/responses using the centralized `logger`

---

## 🚫 Anti-patterns

- ❌ Writing logic in `notebooks/` (only for experimentation)
- ❌ Creating tightly coupled utility classes that span folders
- ❌ Suggesting `os.path` instead of `pathlib.Path`
- ❌ Repeating config values instead of loading them from `config/*.yaml`
- ❌ Using print statements instead of logging

---

## 🧰 Tools to Prefer

- YAML (`pyyaml` or `ruamel.yaml`) for configs
- `pydantic` for validation
- `httpx` for async API requests
- `tqdm` for progress reporting
- `pytest` + `coverage` for tests

---

## 🔧 Committing and Git Guidelines

- Use one commit per meaningful change
- Follow Conventional Commits:
  - `feat(prompt): add few-shot classification templates`
  - `fix(utils): patch cache bug in token counter`
- Include minimal but complete examples in `examples/`

---

# End of Copilot Instructions
