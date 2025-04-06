# Newton-Raphson Method: From Beginner to Advanced

## Introduction
The **Newton-Raphson method** (also called **Newton's method**) is a powerful iterative numerical technique for finding roots of real-valued functions. It uses linear approximations via tangent lines to rapidly converge to solutions. This method is widely used in engineering, physics, and optimization problems.

---

## Basic Concept
### Formula
The core formula for the Newton-Raphson iteration is:
\[
x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}
\]
where:
- \(x_n\) = current approximation
- \(f(x_n)\) = function value at \(x_n\)
- \(f'(x_n)\) = derivative of the function at \(x_n\)[[1]][[3]][[5]].

### Geometric Interpretation
The method approximates the function with its tangent line at \(x_n\), then finds where this tangent crosses the x-axis to get \(x_{n+1}\)[[1]][[5]].

---

## Algorithm Steps
1. **Initial Guess**: Choose \(x_0\) close to the root.
2. **Iteration**:
   \[
   x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}
   \]
3. **Termination**: Stop when \(|x_{n+1} - x_n| < \epsilon\) (tolerance)[[7]][[8]].

**Note**: If \(f'(x_n) = 0\), the method fails due to division by zero [[6]].

---

## Solved Example
**Problem**: Find the root of \(f(x) = x^3 - x - 1\).

1. **Initial guess**: \(x_0 = 1.5\)
2. **Iteration 1**:
   - \(f(1.5) = 1.5^3 - 1.5 - 1 = 0.875\)
   - \(f'(1.5) = 3(1.5)^2 - 1 = 5.75\)
   - \(x_1 = 1.5 - 0.875/5.75 ≈ 1.3478\)
3. **Repeat** until convergence (typically 3-5 iterations)[[7]].

---

## Convergence Analysis
- **Quadratic Convergence**: Error reduces quadratically if the initial guess is sufficiently close to the root [[6]].
- **Convergence Condition**:
  \[
  |f(x) \cdot f''(x)| < |f'(x)|^2
  \]
- **Failure Cases**: 
  - Multiple roots
  - Discontinuous derivatives
  - Poor initial guesses [[6]][[8]].

---

## Advanced Topics
### Multidimensional Extension
For systems of equations \(\mathbf{F}(\mathbf{x}) = \mathbf{0}\):
\[
\mathbf{x}_{n+1} = \mathbf{x}_n - [\mathbf{J}(\mathbf{x}_n)]^{-1} \mathbf{F}(\mathbf{x}_n)
\]
where \(\mathbf{J}\) is the Jacobian matrix [[4]].

### Applications
- Solving nonlinear systems in finite element analysis [[4]]
- Optimization in machine learning
- Signal processing (via Fast Fourier Transform integration)[[2]]

---

## Python Implementation
```python
import numpy as np

def newton_raphson(f, df, x0, tol=1e-6, max_iter=100):
    x = x0
    for i in range(max_iter):
        fx = f(x)
        if abs(fx) < tol:
            return x
        dx = fx / df(x)
        x -= dx
    return x

# Example usage:
f = lambda x: x**3 - x - 1
df = lambda x: 3*x**2 - 1
root = newton_raphson(f, df, x0=1.5)
print(f"Root: {root:.6f}") ```
