# Phase 1: Foundation - YOLO Service
**Status**: PLANNED  
**Difficulty**: EASY  
**Started**: 2025-12-19

## Requirements
- YOLOv8n classification model (small, fast)
- Classification only (no bounding boxes)
- Console output only (no image visualization)
- Confidence threshold filtering (default: 0.25)
- Modern CLI using Typer (type-safe, clean API)
- Pydantic for data validation and settings management

## Files to Create
- `src/yolo_poetry/config.py` - Settings and configuration management
- `src/yolo_poetry/models.py` - Pydantic data models
- `src/yolo_poetry/yolo_service.py` - Core YOLO classification service
- `src/yolo_poetry/main.py` - Typer-based CLI entry point
- `tests/test_yolo_service.py` - Unit tests

## Implementation Steps

### 1. Add Dependencies
```bash
poetry add typer pydantic pydantic-settings
poetry add --group dev pytest
poetry lock
poetry install
```

### 2. Create Configuration (config.py)
```python
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    model_name: str = "yolov8n-cls.pt"
    default_confidence: float = 0.25
    device: str = "cpu"
    
    class Config:
        env_prefix = "YOLO_"
```

### 3. Create Data Models (models.py)
```python
from pydantic import BaseModel

class ClassificationResult(BaseModel):
    class_name: str
    confidence: float

class ClassificationResponse(BaseModel):
    image_path: str
    results: list[ClassificationResult]
    confidence_threshold: float
```

### 4. Create YoloService (yolo_service.py)
```python
from ultralytics import YOLO
from .config import Settings
from .models import ClassificationResponse, ClassificationResult

class YoloService:
    def __init__(self, model_name: str | None = None):
        self.settings = Settings()
        self.model_name = model_name or self.settings.model_name
        self.model = YOLO(self.model_name)
    
    def classify(self, image_path: str, confidence: float | None = None) -> ClassificationResponse:
        # Implementation details
        pass
```

### 5. Create CLI (main.py)
```python
import typer
from pathlib import Path
from .yolo_service import YoloService

app = typer.Typer()

@app.command()
def classify(
    image: Path = typer.Argument(..., exists=True),
    confidence: float = typer.Option(0.25, "--confidence", "-c")
):
    service = YoloService()
    results = service.classify(str(image), confidence)
    # Display results
    
if __name__ == "__main__":
    app()
```

### 6. Write Tests (tests/test_yolo_service.py)
```python
import pytest
from yolo_poetry.yolo_service import YoloService

def test_model_loads():
    service = YoloService()
    assert service.model is not None

def test_classify_with_invalid_path():
    service = YoloService()
    with pytest.raises(FileNotFoundError):
        service.classify("nonexistent.jpg")
```

## Completion Checklist
- [ ] Dependencies installed
- [ ] config.py implemented
- [ ] models.py implemented
- [ ] yolo_service.py implemented
- [ ] main.py CLI working
- [ ] Tests written and passing
- [ ] Manual testing with sample image

## Deletion Trigger
Delete this file once ALL items are checked and Phase 1 is complete.
