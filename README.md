# MiniTorch Module 2

<img src="https://minitorch.github.io/minitorch.svg" width="50%">

**Tensors** - Extending Autodifferentiation to Multidimensional Arrays

* Docs: https://minitorch.github.io/
* Overview: https://minitorch.github.io/module2/module2/

## Overview

Module 2 introduces **Tensors** - multidimensional arrays that extend the scalar autodifferentiation system from Module 1. While the scalar system is correct, it's inefficient due to Python overhead. Tensors solve this by grouping operations together and enabling faster implementations.

## Installation

See [installation.md](installation.md) for detailed setup instructions.

## Quick Start

```bash
# Install dependencies
pip install -e ".[dev,extra]"

# Sync files from Module 1
python sync_previous_module.py ../Module-1 .

# Verify installation
python -c "import minitorch; print('Success!')"

# Run tests
pytest -m task2_1  # Tensor data and indexing
pytest -m task2_2  # Tensor broadcasting
pytest -m task2_3  # Tensor operations
pytest -m task2_4  # Tensor autodifferentiation

# Train tensor-based model
python project/run_tensor.py
```

## Tasks

- **Task 2.1**: Implement tensor data structures with indexing and strides
- **Task 2.2**: Implement tensor broadcasting for operations between different shapes
- **Task 2.3**: Implement tensor operations (map, zip, reduce) and mathematical functions
- **Task 2.4**: Extend autodifferentiation to work with tensors and broadcasting
- **Task 2.5**: Create tensor-based neural network training

## Testing

See [testing.md](testing.md) for detailed testing instructions.

## Files

This assignment requires the following files from Module 1. You can get these by running:

```bash
python sync_previous_module.py ../Module-1 .
```

The files that will be synced are:

- `minitorch/operators.py`
- `minitorch/module.py`
- `minitorch/autodiff.py`
- `minitorch/scalar.py`
- `project/run_manual.py`
- `project/run_scalar.py`