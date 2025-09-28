# Module-2 Modernization Plan

## Overview
This document outlines the step-by-step modernization of Module-2 to match the modern Python development practices implemented in Module-0 and successfully applied to Module-1.

## Current State Analysis

### Legacy Files Present
- `setup.py` - Minimal setup file (contains only `py_modules=[]`)
- `setup.cfg` - Contains tool configurations and version 0.4
- `requirements.txt` - Legacy dependency management
- `requirements.extra.txt` - Additional dependencies
- No modern packaging or CI/CD infrastructure

### Module-2 Specific Considerations
- **Version**: Currently 0.4, should update to 0.6 (Module-0: 0.4, Module-1: 0.5)
- **Tasks**: Only task2_* tests (task2_1, task2_2, task2_3, task2_4, task2_5)
- **Dependencies**: More extensive than Module-1 (includes streamlit, plotly, torch, etc.)
- **Inherited Tasks**: task0_*, task1_* synced from previous modules, not tested in CI

## Modernization Steps Required

### ✅ Step 0: Analysis and Planning (COMPLETED)
- [x] Read Module-1 modernization documentation
- [x] Analyze Module-2 current structure and dependencies
- [x] Create Module2.md assignment summary
- [x] Create this modernization plan

### 📋 Step 1: Create Modern pyproject.toml
**Action**: Migrate from legacy setup.py + requirements.txt to modern pyproject.toml
- **Create**: `Module-2/pyproject.toml`
- **Version**: Update from 0.4 to 0.6
- **Dependencies**: Migrate and update all packages with modern versions
- **Build system**: Use `hatchling` backend (consistent with Module-0/1)
- **Configuration**: Add Ruff, Pyright, and pytest configurations

**Dependency Migration Strategy**:
- **Base requirements.txt**: colorama, hypothesis, mypy, numba, numpy, pre-commit, pytest, pytest-env, pytest-runner, typing_extensions
- **Extra requirements.txt**: datasets, embeddings, networkx, plotly, pydot, python-mnist, streamlit, streamlit-ace, torch, watchdog
- **Version Updates**: Follow Module-1 pattern for common dependencies
- **New Dependencies**: Preserve Module-2 specific packages (streamlit, plotly, etc.)

### 📋 Step 2: Remove Legacy setup.py
**Action**: Remove minimal setup.py file
- **Remove**: `Module-2/setup.py`
- **Reason**: Replaced by pyproject.toml modern packaging

### 📋 Step 3: Remove Legacy Requirements Files
**Action**: Remove both requirements files after verifying all dependencies migrated
- **Remove**: `Module-2/requirements.txt`
- **Remove**: `Module-2/requirements.extra.txt`
- **Verification**: Ensure all dependencies properly migrated to pyproject.toml

### 📋 Step 4: Remove/Modernize setup.cfg
**Action**: Remove setup.cfg after migrating relevant configurations
- **Remove**: `Module-2/setup.cfg`
- **Migration**: Move any necessary configurations to pyproject.toml
- **Note**: Tool configurations (flake8, mypy, black, isort, darglint) will be replaced by modern Ruff/Pyright

### 📋 Step 5: Create Modern Pre-commit Configuration
**Action**: Create modern pre-commit hooks to match Module-0/1
- **Create**: `Module-2/.pre-commit-config.yaml`
- **Content**: Copy exactly from Module-1 (modern toolchain)
- **Tools**: Use Ruff (replaces Black/Flake8/isort) and Pyright (replaces mypy)

### 📋 Step 6: Create GitHub Actions CI/CD
**Action**: Add automated testing and grading infrastructure
- **Create**: `Module-2/.github/workflows/classroom.yaml`
- **Content**: Copy from Module-1 (GitHub Classroom integration)

### 📋 Step 7: Create Module-2 Specific Autograding
**Action**: Create autograding configuration for Module-2 tasks only
- **Create**: `Module-2/.github/classroom/autograding.json`
- **Tests**: Only task2_* tests (task2_1, task2_2, task2_3, task2_4, task2_5) + Style check
- **Reasoning**: Module-2 syncs task0_*, task1_* from previous modules, only tests its own tasks

### 📋 Step 8: Create Documentation Files
**Action**: Create modern documentation matching Module-1
- **Create**: `Module-2/installation.md` (copy from Module-1, generic content)
- **Create**: `Module-2/testing.md` (adapt for Module-2 specific tasks)
- **Update**: `Module-2/README.md` (modernize and improve)

### 📋 Step 9: Verification and Testing
**Action**: Ensure modernized setup works correctly
- **Test**: `pip install -e ".[dev,extra]"` installation
- **Test**: `pre-commit run --all-files` functionality
- **Test**: Module-2 specific tasks (pytest -m task2_1, task2_2, etc.)
- **Test**: Import verification (`python -c "import minitorch; print('Success!')"`)

## Module-2 Specific Dependency Analysis

### Core Dependencies (requirements.txt)
```
colorama==0.4.3      → 0.4.6      (update to match Module-1)
hypothesis==6.54     → 6.138.2    (update to match Module-1)
mypy==0.971          → Remove     (replace with Pyright)
numba==0.56          → 0.61.2     (update to match Module-1)
numpy==1.22          → >=1.24,<2.3 (update to match Module-1)
pre-commit==2.20.0   → 4.3.0      (move to [dev] group)
pytest==7.1.2       → 8.4.1      (update to match Module-1)
pytest-env          → Keep       (Module-2 specific)
pytest-runner==5.2  → Remove     (not needed with modern packaging)
typing_extensions    → Keep       (version spec from Module-1)
```

### Extra Dependencies (requirements.extra.txt)
```
datasets==2.4.0      → Keep/Update (Module-2 specific)
embeddings==0.0.8    → Keep       (Module-2 specific)
networkx==2.4        → Keep/Update (Module-2 specific)
plotly==4.14.3       → Keep/Update (Module-2 specific)
pydot==1.4.1         → Keep/Update (Module-2 specific)
python-mnist         → Keep       (Module-2 specific)
streamlit==1.12.0    → Keep/Update (Module-2 specific)
streamlit-ace        → Keep       (Module-2 specific)
torch                → Keep torch==2.8.0 (match Module-1)
watchdog==1.0.2      → Keep/Update (Module-2 specific)
```

## Task Structure Analysis

### Module-2 Test Tasks
- `task2_1`: Tensor data and indexing (test_tensor_data.py)
- `task2_2`: Tensor broadcasting (test_tensor_data.py)
- `task2_3`: Tensor operations (test_tensor.py)
- `task2_4`: Tensor autodifferentiation (test_tensor.py)
- `task2_5`: Training implementation (no specific tests, validation through training)

### Inherited Tasks
- `task0_*`: Synced from Module-0 via sync_previous_module.py
- `task1_*`: Synced from Module-1 via sync_previous_module.py
- **Note**: Not tested in Module-2 CI, only task2_* tests run

## Expected File Structure After Modernization

```
Module-2/
├── pyproject.toml           # ✅ NEW: Modern packaging
├── installation.md          # ✅ NEW: Installation guide
├── testing.md               # ✅ NEW: Testing documentation
├── module2-modernization.md # ✅ NEW: This planning document
├── Module2.md               # ✅ NEW: Assignment summary
├── README.md                # ✅ UPDATED: Modern documentation
├── .pre-commit-config.yaml  # ✅ NEW: Modern tools
├── .github/                 # ✅ NEW: CI/CD infrastructure
│   ├── workflows/
│   │   └── classroom.yaml   # ✅ NEW: GitHub Actions
│   └── classroom/
│       └── autograding.json # ✅ NEW: Module-2 specific tests
├── setup.py                 # ❌ REMOVED: Legacy
├── setup.cfg                # ❌ REMOVED: Legacy
├── requirements.txt         # ❌ REMOVED: Legacy
└── requirements.extra.txt   # ❌ REMOVED: Legacy
```

## Benefits Expected
- **Performance**: Ruff is significantly faster than Black+Flake8+isort
- **Consistency**: Unified toolchain matching Module-0 and Module-1
- **Modern**: Uses current best practices for Python packaging
- **Automated**: CI/CD pipeline for continuous testing
- **Type Safety**: Better type checking with Pyright
- **Maintainability**: Single configuration file (pyproject.toml)
- **Documentation**: Clear installation and testing guides

## Testing Commands (Post-Modernization)
```bash
# Install in development mode
pip install -e ".[dev,extra]"

# Run pre-commit
pre-commit run --all-files

# Test module-specific tasks
pytest -m task2_1
pytest -m task2_2
pytest -m task2_3
pytest -m task2_4

# Verify import
python -c "import minitorch; print('Success!')"

# Run training (Task 2.5)
python project/run_tensor.py
```

## Next Steps
After completing this modernization plan:
1. Execute steps 1-9 in sequence
2. Test all functionality thoroughly
3. Document any Module-2 specific issues encountered
4. Use this as template for future module modernizations (Module-3, Module-4)