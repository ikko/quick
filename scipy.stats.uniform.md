# Handbook on `scipy.stats.uniform` in Python

## Introduction to `scipy.stats.uniform`

`scipy.stats.uniform` is part of the SciPy library, specifically in the `scipy.stats` module, and it represents a continuous uniform distribution. In probability theory, a uniform distribution is a distribution where all outcomes are equally likely. The `uniform` distribution in SciPy provides a variety of methods to work with continuous uniform distributions.

The continuous uniform distribution is defined on the interval \([a, b]\), where:
- \(a\) is the lower bound of the distribution.
- \(b\) is the upper bound.

The probability density function (PDF) for a uniform distribution is constant between \(a\) and \(b\). It is useful in simulations and in modeling situations where all outcomes are equally likely within a given range.

### Official Documentation Link
For official documentation on `scipy.stats.uniform`, visit the following link:  
[scipy.stats.uniform Documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.uniform.html)

## Key Features of `scipy.stats.uniform`

### 1. Parameters
The uniform distribution has two primary parameters:
- **loc**: The lower bound \(a\), default is 0.
- **scale**: The width of the distribution, calculated as \(b - a\), default is 1.

Thus, the distribution is defined on the interval \([loc, loc + scale]\).

### 2. Functions in `scipy.stats.uniform`

Here are the key functions and attributes available for `scipy.stats.uniform`:

- **`pdf(x, loc=0, scale=1)`**: Probability density function at \(x\). It returns the height of the probability density at \(x\).

- **`cdf(x, loc=0, scale=1)`**: Cumulative distribution function at \(x\). It returns the probability that a random variable from this distribution is less than or equal to \(x\).

- **`rvs(loc=0, scale=1, size=1, random_state=None)`**: Random variates (samples) from the uniform distribution. It generates an array of random numbers drawn from the uniform distribution between \(loc\) and \(loc + scale\).

- **`mean(loc=0, scale=1)`**: The mean (average) of the uniform distribution. It is calculated as \( \frac{loc + (loc + scale)}{2} \).

- **`var(loc=0, scale=1)`**: The variance of the uniform distribution. It is given by \( \frac{(scale)^2}{12} \).

- **`std(loc=0, scale=1)`**: Standard deviation of the uniform distribution. It is calculated as \( \frac{scale}{\sqrt{12}} \).

- **`entropy(loc=0, scale=1)`**: The entropy of the uniform distribution, which quantifies the uncertainty of the distribution. For a uniform distribution, it is given by \( \log(scale) \).

- **`interval(alpha, loc=0, scale=1)`**: Returns the confidence interval for the uniform distribution for a given confidence level \(alpha\).

### Example Usage

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import uniform

# Parameters of the uniform distribution
loc = 0
scale = 10

# Probability Density Function
x = np.linspace(-1, 11, 1000)
pdf_values = uniform.pdf(x, loc, scale)

# Plotting the PDF
plt.plot(x, pdf_values, label="Uniform PDF")
plt.title("Uniform Distribution PDF")
plt.xlabel("x")
plt.ylabel("Probability Density")
plt.legend()
plt.grid(True)
plt.show()

# Generate random samples
random_samples = uniform.rvs(loc=loc, scale=scale, size=1000)

# Plot histogram of the random samples
plt.hist(random_samples, bins=20, density=True, alpha=0.6, color='g', label="Random Samples")
plt.plot(x, pdf_values, 'r-', label="Uniform PDF")
plt.title("Random Samples vs. PDF")
plt.xlabel("x")
plt.ylabel("Density")
plt.legend()
plt.grid(True)
plt.show()
```

### 3. Common Use Cases

- **Simulations**: Uniform distributions are often used in simulations where each outcome in a specified range has equal probability.
- **Random Sampling**: Generating random values within a specific range.
- **Monte Carlo Methods**: Uniform distributions are used in Monte Carlo simulations to generate random inputs that follow a uniform distribution.
- **Testing and Benchmarking**: Uniform random values are used for stress-testing algorithms or models.

### 4. Methods Overview

- **`pdf(x)`**: Calculates the probability density at each point in the range.
- **`cdf(x)`**: Provides the cumulative probability for a given point.
- **`rvs()`**: Useful for generating random values that follow the uniform distribution.
- **`mean()`**: Returns the mean of the distribution.
- **`std()`**: Returns the standard deviation of the distribution.

### 5. Example of Calculating Mean, Variance, and Sampling

```python
# Mean and Variance of the distribution
mean_value = uniform.mean(loc=0, scale=10)
variance_value = uniform.var(loc=0, scale=10)

print(f"Mean of the uniform distribution: {mean_value}")
print(f"Variance of the uniform distribution: {variance_value}")

# Random sample generation
random_values = uniform.rvs(loc=0, scale=10, size=5)
print(f"Random samples: {random_values}")
```

### 6. Visualizing the Distribution

The following code demonstrates how to visualize the PDF, CDF, and random samples of the uniform distribution.

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import uniform

# Set parameters
loc = 0
scale = 5

# Create x values for plotting
x = np.linspace(-1, 6, 1000)

# Plot PDF
pdf_values = uniform.pdf(x, loc, scale)
plt.plot(x, pdf_values, label="PDF")

# Plot CDF
cdf_values = uniform.cdf(x, loc, scale)
plt.plot(x, cdf_values, label="CDF", linestyle='--')

plt.title("PDF and CDF of Uniform Distribution")
plt.xlabel("x")
plt.ylabel("Probability")
plt.legend()
plt.grid(True)
plt.show()

# Generate random samples
random_samples = uniform.rvs(loc=loc, scale=scale, size=1000)

# Plot histogram of random samples
plt.hist(random_samples, bins=20, density=True, alpha=0.7, color='g', label="Random Samples")
plt.plot(x, pdf_values, 'r-', label="PDF")
plt.title("Random Samples and Uniform PDF")
plt.xlabel("x")
plt.ylabel("Density")
plt.legend()
plt.grid(True)
plt.show()
```

### 7. Link to Official Documentation

For a detailed explanation and the full list of available methods and attributes, refer to the official documentation:  
[scipy.stats.uniform Documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.uniform.html)

---

## Conclusion

`scipy.stats.uniform` provides a robust set of tools for working with continuous uniform distributions in Python. Whether you're conducting statistical analysis, generating random samples, or visualizing data, this module will be a crucial tool for a variety of applications. By understanding and utilizing its core functions like `pdf`, `cdf`, and `rvs`, you can easily incorporate the uniform distribution into your projects.
