# Newton-Raphson Method: From Beginner to Advanced

## Introduction
The **Newton-Raphson method** is a root-finding algorithm that uses linear approximation through tangent lines to quickly converge to solutions. Works best when the function is smooth and the initial guess is close to the true root.

---

## Core Formula
The iterative formula is:
$$
x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}
$$

### Key Components:
- $x_n$: Current approximation
- $f(x_n)$: Function value at current point
- $f'(x_n)$: Derivative at current point

---

## Geometric Interpretation
![Newton-Raphson Visualization](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8c/Newton_iteration.svg/320px-Newton_iteration.svg.png)

1. Start at $(x_0, f(x_0))$
2. Follow tangent line to x-axis
3. New x-value becomes $x_1$
4. Repeat until convergence

---

## Step-by-Step Process
1. **Choose initial guess** $x_0$
2. **Compute**:
   - Function value: $f(x_n)$
   - Derivative: $f'(x_n)$
3. **Update**:
   $$
   x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}
   $$
4. **Check convergence**: Stop when $|x_{n+1} - x_n| < \epsilon$

---

## Worked Example
**Problem**: Find root of $f(x) = x^3 - 2x - 5$

1. **Initial guess**: $x_0 = 2$
2. **First iteration**:
   - $f(2) = 8 - 4 - 5 = -1$
   - $f'(2) = 3(4) - 2 = 10$
   - $x_1 = 2 - (-1)/10 = 2.1$
3. **Second iteration**:
   - $f(2.1) = 9.261 - 4.2 - 5 = 0.061$
   - $f'(2.1) = 3(4.41) - 2 = 11.23$
   - $x_2 = 2.1 - 0.061/11.23 ≈ 2.0946$
4. **Converges to** ≈ 2.0946 after 3-4 iterations

---

## Convergence Criteria
- **Quadratic convergence**: Error squares each iteration near root
- **Requirements**:
  - $f$ is twice continuously differentiable
  - $f'(x) \neq 0$ near root
  - Initial guess sufficiently close to root

**Convergence condition**:
$$
\left| \frac{f(x) f''(x)}{[f'(x)]^2} \right| < 1
$$

---

## Advanced Topics
### Multidimensional Extension
For systems of equations \(\mathbf{F}(\mathbf{x}) = \mathbf{0}\):
\[
\mathbf{x}_{n+1} = \mathbf{x}_n - [\mathbf{J}(\mathbf{x}_n)]^{-1} \mathbf{F}(\mathbf{x}_n)
\]
where \(\mathbf{J}\) is the Jacobian matrix [[4]].

### Applications
- Solving nonlinear systems in finite element analysis
- Optimization in machine learning
- Signal processing (via Fast Fourier Transform integration)

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
