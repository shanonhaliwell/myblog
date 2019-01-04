---
title: Code Sample
subtitle: Using Hugo or Pygments
date: 2016-03-08
tags: ["example", "code"]
---

The following are two code samples using syntax highlighting.

<!--more-->

The following is a code sample using triple backticks ( ``` ) code fencing provided in Hugo. This is client side highlighting and does not require any special installation.

```javascript
    var num1, num2, sum
    num1 = prompt("Enter first number")
    num2 = prompt("Enter second number")
    sum = parseInt(num1) + parseInt(num2) // "+" means "add"
    alert("Sum = " + sum)  // "+" means combine into a string
```

### Gauss-Elimination
```python
import numpy as np

def solve(A, b):
  n = np.shape(A)[0]

  # Forward elimination
  for j in range(n-1):
    for i in range(j+1, n):
      b[i] -= (b[j] / A[j][j] * A[i][j])
      for k in range(j+1, n):
        A[i][k] -= (A[j][k] / A[j][j] * A[i][j])
      A[i][j] = 0

  x = np.zeros([n])
  # Back substitution
  for i in range(n-1, -1, -1):
    x[i] = b[i] / A[i][i]
    for j in range(i+1, n):
      x[i] -= (A[i][j] * x[j]) / A[i][i]
  return x

if __name__ == '__main__':
  A = np.array([[1, 2, 3, 4],
                [2, 2, 3, 4],
                [3, 3, 3, 4],
                [4, 4, 4, 4]], dtype='float64')
  b = np.array([1.234, 2.234, 3.334, 4.444], dtype='float64')

print solve(A, b)
```

### LU Decomposition
```python
import numpy as np

def decompose(A):
  n = np.shape(A)[0]
  LU = np.zeros([n,n])

  for i in range(n):
    LU[i][0] = A[i][0]

  # except for the diagonal element because it's always 1
  for j in range(1, n):
    LU[0][j] = A[0][j] / LU[0][0]

  for j in range(1, n):
    for i in range(j, n):
      s = 0
      for k in range(j):
        s += LU[i][k] * LU[k][j]
      LU[i][j] = A[i][j] - s
    for i in range(j+1, n):
      s = 0
      for k in range(j):
        s += LU[j][k] * LU[k][i]
      LU[j][i] = (A[j][i] - s) / LU[j][j]
  return LU

def solve(LU, b):
  n = np.shape(LU)[0]

  for i in range(n):
    s = 0
    for k in range(i):
      s += LU[i][k] * b[k]
    b[i] = (b[i] - s) / LU[i][i]

  x = np.zeros([n])
  x[n-1] = b[n-1]
  for j in range(n-2, -1, -1):
    s = 0
    for k in range(j+1, n):
      s += LU[j][k] * x[k]
    x[j] = b[j] - s

  return x

def det(LU):
  d = 1
  for i in range(np.shape(LU)[0]):
    d *= LU[i][i]
  return d

if __name__ == '__main__':
  A = np.array([[1, 2, 3, 4],
                [2, 2, 3, 4],
                [3, 3, 3, 4],
                [4, 4, 4, 4]], dtype='float64')
  b = np.array([1.234, 2.234, 3.334, 4.444], dtype='float64')
  print solve(decompose(A), b)
print det(decompose(A))
```

The following is a code sample using the "highlight" shortcode provided in Hugo. This is server side highlighting and requires Python and Pygments to be installed.

{{< highlight javascript >}}
    var num1, num2, sum
    num1 = prompt("Enter first number")
    num2 = prompt("Enter second number")
    sum = parseInt(num1) + parseInt(num2) // "+" means "add"
    alert("Sum = " + sum)  // "+" means combine into a string
{{</ highlight >}}


And here is the same code with line numbers:

{{< highlight javascript "linenos=inline">}}
    var num1, num2, sum
    num1 = prompt("Enter first number")
    num2 = prompt("Enter second number")
    sum = parseInt(num1) + parseInt(num2) // "+" means "add"
    alert("Sum = " + sum)  // "+" means combine into a string
{{</ highlight >}}


## Welcome to My Laboratory :)

This repository has implementations of many algorithms in Computer Science.

### Fundamental Algorithms

- sorting
- data structures
- algorithm design technique such as Dynamic Programming

These are based on: [Introduction to Algorithms](http://mitpress.mit.edu/books/introduction-algorithms)

### Numerical Analysis

- LU decomposition
- Gauss Elimination for linear equation systems

### Machine Learning

Not only Machine Learning, also Natural Language Processing and Information Retrieval

- BP(Back Propagation) Neural Network
- k-means
- tf-idf
- Linear Regression
