Here’s a **NumPy cheatsheet** that covers the essential and most commonly used features of the NumPy library. NumPy is a powerful library for numerical computations and provides support for large, multi-dimensional arrays and matrices.

---

### **NumPy Cheatsheet**

#### **1. Basics of NumPy**

- **Importing NumPy**:
    ```python
    import numpy as np
    ```

- **Creating Arrays**:
    ```python
    np.array([1, 2, 3])  # 1D array
    np.array([[1, 2], [3, 4]])  # 2D array
    ```

- **Creating Arrays with Zeros, Ones, and Other Functions**:
    ```python
    np.zeros((3, 3))  # 3x3 array of zeros
    np.ones((2, 2))  # 2x2 array of ones
    np.empty((2, 3))  # Empty array with uninitialized values
    np.arange(0, 10, 2)  # Array with values from 0 to 10 with a step of 2
    np.linspace(0, 1, 5)  # 5 evenly spaced values between 0 and 1
    ```

- **Array Dimensions**:
    ```python
    arr = np.array([[1, 2], [3, 4]])
    arr.shape  # (2, 2)
    arr.ndim  # 2 (number of dimensions)
    arr.size  # 4 (total number of elements)
    arr.dtype  # dtype('int64')
    ```

#### **2. Array Indexing and Slicing**

- **Accessing Elements**:
    ```python
    arr[0, 1]  # Access element in first row, second column
    arr[1]  # Access second row (full)
    arr[:, 1]  # Access all rows in the second column
    ```

- **Slicing**:
    ```python
    arr[:2, 1:]  # First two rows, columns from index 1 onwards
    ```

- **Boolean Indexing**:
    ```python
    arr[arr > 2]  # Return elements where value is greater than 2
    ```

#### **3. Array Operations**

- **Element-wise Operations**:
    ```python
    arr + 10  # Add 10 to each element
    arr * 2  # Multiply each element by 2
    np.sqrt(arr)  # Square root of each element
    np.sin(arr)  # Sine of each element
    ```

- **Mathematical Functions**:
    ```python
    np.mean(arr)  # Mean of the array
    np.median(arr)  # Median of the array
    np.std(arr)  # Standard deviation
    np.sum(arr)  # Sum of all elements
    np.prod(arr)  # Product of all elements
    np.min(arr)  # Minimum value
    np.max(arr)  # Maximum value
    ```

- **Aggregating Functions**:
    ```python
    arr.sum()  # Sum of elements
    arr.mean()  # Mean of elements
    arr.cumsum()  # Cumulative sum
    arr.cumprod()  # Cumulative product
    ```

- **Reshaping Arrays**:
    ```python
    arr.reshape(2, 3)  # Reshape array to 2 rows, 3 columns
    arr.flatten()  # Flatten the array to 1D
    ```

#### **4. Array Broadcasting**

- **Broadcasting**:
    ```python
    arr = np.array([[1, 2], [3, 4]])
    scalar = 2
    arr + scalar  # Broadcasting scalar to add to each element of arr
    ```

#### **5. Stacking and Splitting**

- **Concatenating Arrays**:
    ```python
    np.concatenate([arr1, arr2], axis=0)  # Stack arrays vertically (rows)
    np.concatenate([arr1, arr2], axis=1)  # Stack arrays horizontally (columns)
    ```

- **Splitting Arrays**:
    ```python
    np.split(arr, 2, axis=0)  # Split array into 2 parts along rows
    np.hsplit(arr, 2)  # Split array into 2 parts along columns
    ```

#### **6. Linear Algebra**

- **Matrix Multiplication**:
    ```python
    np.dot(arr1, arr2)  # Dot product of two arrays
    np.matmul(arr1, arr2)  # Matrix multiplication (same as dot for 2D arrays)
    ```

- **Matrix Inversion**:
    ```python
    np.linalg.inv(arr)  # Inverse of a matrix
    ```

- **Eigenvalues and Eigenvectors**:
    ```python
    np.linalg.eig(arr)  # Eigenvalues and eigenvectors of a matrix
    ```

- **Determinant**:
    ```python
    np.linalg.det(arr)  # Determinant of a matrix
    ```

#### **7. Random Module**

- **Generate Random Numbers**:
    ```python
    np.random.rand(3, 3)  # Random numbers from [0, 1) in a 3x3 array
    np.random.randint(0, 10, (3, 3))  # Random integers from 0 to 9 in a 3x3 array
    np.random.randn(3, 3)  # Random samples from a standard normal distribution
    ```

- **Random Seed**:
    ```python
    np.random.seed(42)  # Set random seed for reproducibility
    ```

#### **8. Set Operations**

- **Set Operations on Arrays**:
    ```python
    np.unique(arr)  # Unique elements in an array
    np.intersect1d(arr1, arr2)  # Intersection of two arrays
    np.setdiff1d(arr1, arr2)  # Elements in arr1 not in arr2
    np.union1d(arr1, arr2)  # Union of two arrays
    ```

#### **9. File I/O**

- **Saving and Loading Arrays**:
    ```python
    np.save('array.npy', arr)  # Save array to file
    arr_loaded = np.load('array.npy')  # Load array from file
    ```

- **Save/Load in Text Format**:
    ```python
    np.savetxt('array.txt', arr)  # Save array to a text file
    arr_loaded = np.loadtxt('array.txt')  # Load array from text file
    ```

#### **10. Advanced Features**

- **Fancy Indexing**:
    ```python
    arr[[0, 2], [1, 0]]  # Access elements at positions (0,1) and (2,0)
    ```

- **Conditional Assignment**:
    ```python
    arr[arr > 3] = 0  # Set all elements greater than 3 to 0
    ```

- **Array Comparison**:
    ```python
    np.all(arr > 0)  # Check if all elements are greater than 0
    np.any(arr < 0)  # Check if any element is less than 0
    ```

---

### **Common Operations Summary**

| **Operation**                    | **Syntax**                             |
|-----------------------------------|----------------------------------------|
| Create a 1D array                 | `np.array([1, 2, 3])`                  |
| Create a 2D array                 | `np.array([[1, 2], [3, 4]])`           |
| Array dimensions                  | `arr.shape`, `arr.ndim`                |
| Reshape an array                  | `arr.reshape(2, 3)`                    |
| Sum of elements                   | `arr.sum()`                            |
| Mean of elements                  | `arr.mean()`                           |
| Accessing specific element        | `arr[0, 1]`                            |
| Broadcasting with scalar          | `arr + 10`                             |
| Concatenate arrays                | `np.concatenate([arr1, arr2], axis=0)` |
| Matrix multiplication             | `np.dot(arr1, arr2)`                   |
| Eigenvalues of a matrix           | `np.linalg.eig(arr)`                   |
| Generate random numbers           | `np.random.rand(3, 3)`                 |

---

This cheatsheet summarizes the core functionalities of **NumPy** for working with arrays and performing mathematical operations efficiently.