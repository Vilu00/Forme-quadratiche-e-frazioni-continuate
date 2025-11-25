# Continued Fractions and Quadratic Irrationals - Python Implementation

This repository contains Python implementations for bidirectional conversion between quadratic polynomials and their continued fraction representations.

---

## Files Overview

### 1. frompolynomialtocontinuedfractions.ipynb
Converts quadratic polynomials to continued fractions.

### 2. Fromcontinuedfractionstopolynomials.ipynb
Converts continued fractions to quadratic polynomials and provides convergent computations.

---

## frompolynomialtocontinuedfractions.ipynb

### Purpose
Given a quadratic polynomial **Ax² + Bx + C**, computes the continued fraction representation of its roots.

### Main Function

**`from_polinomial_to_continued_fraction(A, B, C)`**

**Input:** Coefficients A, B, C (integers)

**Validation:**
- Checks that coefficients are coprime (gcd(A,B,C) = 1)
- Verifies discriminant Δ = B² - 4AC > 0
- Ensures Δ is not a perfect square (to guarantee irrational roots)

**Output:**
- Both roots: α₁ = (-B + √Δ)/(2A) and α₂ = (B + √Δ)/(-2A)
- Continued fraction representation: [preperiod; **overline{period}**]
- **Successive tails**: α₀ = α, α₁, α₂, ... for both roots

**Example:**
```python
from_polinomial_to_continued_fraction(1, -98, 72)
```

### Helper Functions

- **`analizza_polinomio(A, B, C)`**: Validates polynomial and computes discriminant
- **`calcola_radici(A, B, delta)`**: Computes symbolic roots
- **`get_continued_fraction_periodic_and_tails(P, D, Q)`**: Generates continued fraction from (P + √D)/Q using integer arithmetic
- **`print_continued_fraction(pre_period, period, tails)`**: Displays results in LaTeX format

---

## Fromcontinuedfractionstopolynomials.ipynb

### Purpose
Converts continued fractions to minimal polynomials and computes convergents.

### Main Function

**`fromcontinuedfractiontopolynomial(preperiod, period)`**

**Input:**
- `preperiod`: List (can be empty `[]`)
- `period`: List (non-empty)

**Process:**
1. Defines γ = [**overline{period}**] (purely periodic part)
2. Computes minimal polynomial of γ
3. Applies Möbius transformation using preperiod matrix
4. Computes minimal polynomial of α = [preperiod; **overline{period}**]

**Output:**
- Minimal polynomial coefficients (reduced to coprime integers)
- Symbolic root representation
- Both γ and α with their respective polynomials


## Convergent Functions

### Computing Convergents

**`Construct_convergentnth_from_continued_fraction(preperiod, period, n)`**
- **Returns:** The n-th convergent P_n/Q_n as a Sympy rational
- Handles both finite and periodic continued fractions

**`Construct_convergentslist_from_continued_fraction(preperiod, period, n)`**
- **Returns:** List [P₀/Q₀, P₁/Q₁, ..., P_n/Q_n]
- Output contains **n+1 elements** (includes 0-th convergent)

**Examples:**
```python
Construct_convergentnth_from_continued_fraction([1,5,7], [3,4], 8)
# Returns: 18251/1527

Construct_convergentslist_from_continued_fraction([1,5,7], [3,4], 8)
# Returns: [1, 6, 43/36, 135/113, ...]
```

### Reconstructing Continued Fractions from Convergents

**`from_convergentsnumb_to_continued_fraction(convergents)`**
- **Input:** List of convergents as **floats or fractions**
  ```python
  [1, 1.2, 1.194444...]  # or [1, 6/5, 43/36, ...]
  ```
- **Output:** Reconstructed continued fraction [a₀, a₁, a₂, ...]

**`from_convergentsstring_to_continued_fraction(convergents)`**
- **Input:** List of convergents as **strings**
  ```python
  ['1/1', '6/5', '43/36', '135/113', ...]
  ```
- **Output:** Reconstructed continued fraction [a₀, a₁, a₂, ...]

**Note:** Uses the inverse algorithm: a_k = (P_k - P_{k-2}) / P_{k-1}

---

## Dependencies

```python
import math
from sympy import symbols, sqrt, gcd, Integer, latex, floor, together, Add, 
                  factor, simplify, Matrix, eye, Symbol, expand, pprint
from IPython.display import display, Math
from fractions import Fraction
```

### Required Libraries
- **SymPy**: Symbolic mathematics and exact arithmetic
- **IPython**: LaTeX rendering in Jupyter notebooks
- **fractions**: Python's built-in rational number support

---

## Mathematical Background

### Continued Fraction Notation
- **[a₀, a₁, a₂, ...]**: Simple continued fraction
- **[a₀; **overline{a₁, a₂, ..., aₙ}**]**: Eventually periodic (preperiod + period)
- **[**overline{a₁, a₂, ..., aₙ}**]**: Purely periodic

### Convergents
The n-th convergent P_n/Q_n satisfies the recurrence:
- P_n = a_n · P_{n-1} + P_{n-2}
- Q_n = a_n · Q_{n-1} + Q_{n-2}

With initial conditions: P₋₁ = 1, P₀ = a₀, Q₋₁ = 0, Q₀ = 1

---

## Usage Examples

### Example 1: Polynomial → Continued Fraction
```python
# Polynomial: x² - 98x + 72
from_polinomial_to_continued_fraction(1, -98, 72)
```

### Example 2: Continued Fraction → Polynomial
```python
# α = [1, 5, 7; overline{3, 4}]
fromcontinuedfractiontopolynomial([1,5,7], [3,4])
```

### Example 3: Compute Convergents
```python
# First 9 convergents (indices 0 through 8)
convergents = Construct_convergentslist_from_continued_fraction([1,5,7], [3,4], 8)
```

### Example 4: Reverse from Convergents
```python
# Reconstruct continued fraction from string convergents
from_convergentsstring_to_continued_fraction(['1/1', '6/5', '43/36', '135/113'])
```

---

## Notes

- All functions use **exact integer arithmetic** to avoid floating-point errors
- Polynomials must have **coprime coefficients** and **positive non-square discriminant**
- Output is rendered in **LaTeX format** for Jupyter notebooks
- Möbius transformations are implemented via **2×2 matrix multiplication**
