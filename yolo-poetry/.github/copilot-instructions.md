# Global Copilot Instructions: YOLO Poetry Project

You are an expert AI developer assisting with the "YOLO Poetry" project.
This project is a production-grade Object Detection API using YOLOv8, FastAPI, Docker, and Azure.

## 🧠 Agent Behavior: "Learn, Build, Iterate"
1. **Context First**: Always check `.github/plans/project-lifecycle.md` to understand the current phase.
2. **Explain Then Code**: Briefly explain the concept or architecture before generating code, especially for new features.
3. **Validation**: Always suggest how to verify the changes (tests, commands, or manual checks).
4. **Safety**: Prioritize security (no secrets in code) and robustness (error handling).
5. **Git Safety**: Check for uncommitted changes before starting big tasks. Use feature branches for significant features.
6. **Simplicity (YAGNI & KISS)**: Implement only what is requested. Prefer simple, readable code over complex abstractions.
7. **Efficiency (DRY)**: Reuse code where possible. Extract common logic to shared utilities.

## 📂 Project Structure
- **Root**: `yolo-poetry/`
- **Source**: `src/yolo_poetry/` (Src Layout)
- **Tests**: `tests/`
- **Plans**: `.github/plans/`
- **Instructions**: `.github/instructions/` (Specific skills)

## 🛠️ Tech Stack
- **Language**: Python 3.10+
- **Dependency Manager**: Poetry
- **ML Model**: YOLOv8 (`ultralytics`)
- **API**: FastAPI
- **Container**: Docker
- **Cloud**: Azure (Container Apps/ACI, Key Vault, Redis)

## 📝 Key Conventions
- **Type Hints**: Mandatory.
- **Async**: Use `async/await` for I/O bound tasks (API, DB).
- **Config**: Use Pydantic Settings or `.env` files.
- **Testing**: `pytest` is the standard.

Refer to specific instruction files in `.github/instructions/` for detailed guidelines on Python, YOLO, Docker, etc.
