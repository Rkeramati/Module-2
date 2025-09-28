# Module-2 Assignment Summary

## Overview
Module-2 introduces **Tensors** - multidimensional arrays that extend and optimize the scalar autodifferentiation system from Module-1. While Module-1's scalar system is correct, it's inefficient due to Python overhead from individual scalar objects and operations. Tensors solve this by grouping operations together and enabling faster implementations.

## Learning Objectives
- Build efficient tensor data structures with proper indexing and memory layout
- Implement tensor operations (map, zip, reduce) for element-wise and reduction operations
- Extend autodifferentiation to work with tensors and broadcasting
- Create tensor-based neural networks that outperform scalar implementations
- Understand memory optimization through strides, views, and broadcasting

## Problem Statement
The scalar system from Module-1 has performance issues:
- Every scalar requires building an object
- Each operation stores a complete computation graph
- Training requires repeated operations with Python overhead
- Models like linear regression need inefficient for loops

**Solution**: Tensors group repeated operations to save Python overhead and delegate to faster implementations.

## Core Architecture

### Key Files
- **tensor.py** - User-facing Tensor interface (similar to scalar.py)
- **tensor_data.py** - Core indexing, strides, storage management
- **tensor_ops.py** - Higher-order tensor operations (map, zip, reduce)
- **tensor_functions.py** - Autodifferentiation-ready tensor functions

### Supporting Files
- **operators.py** - Mathematical operators (inherited from Module-1)
- **autodiff.py** - Autodifferentiation framework (inherited from Module-1)

## Detailed Task Breakdown

### Task 2.1: Tensor Data - Indexing
**File**: `minitorch/tensor_data.py`
**Objective**: Implement core tensor backend (`TensorData`) for indexing and storage

**Functions to Implement**:
1. **`index_to_position(index: Index, strides: Strides) -> int`**
   - Converts multidimensional tensor index to single storage position
   - Uses strides to calculate memory position

2. **`to_index(ordinal: int, shape: Shape, out_index: OutIndex) -> None`**
   - Converts ordinal position (0...size-1) to multidimensional index
   - Ensures enumeration produces every index exactly once
   - May not be inverse of `index_to_position`

3. **`TensorData.permute(*order: int) -> TensorData`**
   - Permutes tensor dimensions 
   - Returns new TensorData with same storage, new dimension order

**Key Concepts**:
- **Storage**: Flat 1D array containing tensor data
- **Shape**: Dimensions of tensor (e.g., (3, 4, 5))
- **Strides**: Memory navigation pattern (how many positions to skip per dimension)

### Task 2.2: Tensor Broadcasting
**File**: `minitorch/tensor_data.py`
**Objective**: Implement broadcasting for operations between differently-shaped tensors

**Functions to Implement**:
1. **`shape_broadcast(shape1: UserShape, shape2: UserShape) -> UserShape`**
   - Creates union shape from two shapes following broadcasting rules
   - Raises `IndexingError` if shapes cannot broadcast

2. **`broadcast_index(big_index, big_shape, shape, out_index) -> None`**
   - Converts index from larger tensor to smaller tensor
   - Handles dimension mapping (may map to 0 or remove dimensions)

**Broadcasting Rules**:
- Tensors aligned from rightmost dimension
- Dimensions of size 1 can broadcast to any size
- Missing dimensions treated as size 1
- Example: (3, 1) + (3, 4) → (3, 4)

### Task 2.3: Tensor Operations
**File**: `minitorch/tensor_ops.py`, `minitorch/tensor_functions.py`, `minitorch/tensor.py`
**Objective**: Implement high-level tensor operations and user interface

**Core Operations in `tensor_ops.py`**:
1. **`tensor_map(fn) -> Callable`**
   - Applies function element-wise to tensor
   - Handles broadcasting between different shapes

2. **`tensor_zip(fn) -> Callable`**
   - Applies binary function element-wise to two tensors
   - Supports broadcasting

3. **`tensor_reduce(fn) -> Callable`**
   - Reduces tensor along specified dimension
   - Output shape same as input except reduced dimension becomes size 1

**Forward Functions in `tensor_functions.py`**:
- **Unary**: Mul, Sigmoid, ReLU, Log, Exp
- **Binary**: LT, EQ, IsClose
- **Reductions**: Sum (with dim argument)
- **Shape Operations**: Permute

**User Interface in `tensor.py`**:
- **Properties**: size, dims
- **Operators**: add, sub, mul, lt, eq, gt, neg, radd, rmul
- **Functions**: all, is_close, sigmoid, relu, log, exp
- **Reductions**: sum, mean (with optional dim)
- **Shape Operations**: permute, view
- **Utilities**: zero_grad_

### Task 2.4: Gradients and Autograd
**File**: `minitorch/tensor_functions.py`
**Objective**: Implement backward functions for tensor autodifferentiation

**Key Challenges**:
- Gradient computation through broadcasting operations
- Proper gradient aggregation when tensors are broadcast
- Maintaining computation graph for complex tensor operations

**Similar to Module-1**: Tensors are `Variable` objects supporting autodifferentiation, but now handle multidimensional arrays efficiently.

### Task 2.5: Training
**File**: `project/run_tensor.py`
**Objective**: Implement tensor-based neural network training

**Requirements**:
- Three-layer neural network: 2 → Hidden (ReLU) → Hidden (ReLU) → Output (Sigmoid)
- Same functionality as `project/run_scalar.py` but using tensor operations
- Train on all datasets and record results
- Measure and report time per epoch

## Key Technical Concepts

### Memory Layout and Strides
- **Contiguous**: Data stored in row-major (C-style) order
- **Strides**: Define memory access pattern for each dimension
- **Views**: Different tensor shapes sharing same underlying storage

### Tensor Operations Hierarchy
1. **Low-level**: `tensor_ops.py` (map, zip, reduce)
2. **Mid-level**: `tensor_functions.py` (mathematical functions)
3. **High-level**: `tensor.py` (user-friendly interface)

### Performance Benefits
- **Reduced Python Overhead**: Group operations instead of individual scalars
- **Vectorized Operations**: Delegate to optimized implementations
- **Memory Efficiency**: Shared storage through views and broadcasting
- **Graph Optimization**: Fewer nodes in computation graph

## Testing Structure
- **task2_1**: `test_tensor_data.py` - Indexing and layout tests
- **task2_2**: `test_tensor_data.py` - Broadcasting tests  
- **task2_3**: `test_tensor.py` - Function and operation tests
- **task2_4**: `test_tensor.py` - Autodifferentiation tests

## Expected Performance Improvement
Moving from scalar to tensor implementation should provide:
- Significant speedup in training time per epoch
- Reduced memory usage through efficient storage
- Better scalability for larger models and datasets

## Integration with Previous Modules
**Synced Files from Module-1**:
- `minitorch/operators.py` - Mathematical operators
- `minitorch/module.py` - Neural network module framework  
- `minitorch/autodiff.py` - Core autodifferentiation system
- `minitorch/scalar.py` - Scalar implementation
- `project/run_manual.py` - Manual gradient checking
- `project/run_scalar.py` - Scalar-based training

## Debugging Tools
- **Expression Visualization**: `streamlit run project/app.py -- 2`
- **Graph Builder**: View computation graphs for tensor operations
- **Tensor Debugging**: Interactive tools for understanding tensor operations