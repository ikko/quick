# Handbook on `scipy.stats.norm` in Python

## Introduction to `scipy.stats.norm`

`scipy.stats.norm` is part of the SciPy library, specifically in the `scipy.stats` module, and it represents the **normal (Gaussian) distribution**. The normal distribution is one of the most commonly used distributions in statistics, often referred to as the bell curve. It describes data that clusters around a mean value with a specific spread or variance. The shape of the distribution is symmetric, meaning the data is equally likely to fall above or below the mean.

In mathematical terms, a normal distribution is characterized by two parameters:
- **Mean (\(\mu\))**: The center of the distribution, where the peak of the curve occurs.
- **Standard deviation (\(\sigma\))**: A measure of the spread of the distribution. A larger standard deviation results in a wider, flatter curve, while a smaller standard deviation leads to a narrower, steeper curve.

### Official Documentation Link
For the official documentation on `scipy.stats.norm`, visit the following link:  
[scipy.stats.norm Documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.norm.html)

## Key Features of `scipy.stats.norm`

The normal distribution is widely used in statistics due to its properties, and `scipy.stats.norm` provides several functions for working with it.

### 1. Important Functions in `scipy.stats.norm`

Here are some essential functions available in the `scipy.stats.norm` module:

- **`pdf(x, loc=0, scale=1)`**: Probability density function (PDF). It computes the height of the normal distribution at the given value \(x\).
  
- **`cdf(x, loc=0, scale=1)`**: Cumulative distribution function (CDF). It computes the probability that a random variable \(X\) from the normal distribution is less than or equal to \(x\).

- **`sf(x, loc=0, scale=1)`**: Survival function (1 - CDF). It calculates the probability that a random variable is greater than \(x\).

- **`ppf(q, loc=0, scale=1)`**: Percent point function (inverse of CDF). It returns the value \(x\) for which the cumulative probability is \(q\).

- **`rvs(loc=0, scale=1, size=1, random_state=None)`**: Random variates (samples). It generates random values that follow a normal distribution with the specified mean and standard deviation.

- **`mean(loc=0, scale=1)`**: The mean of the normal distribution, which is equal to \(loc\).

- **`var(loc=0, scale=1)`**: The variance of the normal distribution, which is equal to \(scale^2\).

- **`std(loc=0, scale=1)`**: The standard deviation of the normal distribution, which is equal to \(scale\).

- **`entropy(loc=0, scale=1)`**: The entropy of the normal distribution, which measures the uncertainty or randomness.

### Example Usage

Here’s an example of how to use `scipy.stats.norm` to calculate probabilities and generate random samples from a normal distribution:

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import norm

# Parameters
mu = 0  # Mean
sigma = 1  # Standard deviation

# Probability Density Function (PDF)
x = np.linspace(-5, 5, 1000)
pdf_values = norm.pdf(x, mu, sigma)

# Plotting the PDF
plt.plot(x, pdf_values, label="PDF")
plt.title("Normal Distribution (PDF)")
plt.xlabel("x")
plt.ylabel("Probability Density")
plt.grid(True)
plt.legend()
plt.show()

# Cumulative Distribution Function (CDF)
cdf_values = norm.cdf(x, mu, sigma)

# Plotting the CDF
plt.plot(x, cdf_values, label="CDF", color='red')
plt.title("Normal Distribution (CDF)")
plt.xlabel("x")
plt.ylabel("Cumulative Probability")
plt.grid(True)
plt.legend()
plt.show()

# Generate random samples
random_samples = norm.rvs(mu, sigma, size=1000)

# Plot histogram of random samples
plt.hist(random_samples, bins=30, density=True, alpha=0.6, color='g', label="Random Samples")
plt.plot(x, pdf_values, 'r-', label="PDF")
plt.title("Random Samples and PDF of Normal Distribution")
plt.xlabel("x")
plt.ylabel("Density")
plt.legend()
plt.grid(True)
plt.show()
```

### 2. Common Use Cases

The normal distribution is widely applicable in various fields for different purposes:

- **Statistical Analysis**: The normal distribution is often used in hypothesis testing, confidence intervals, and regression analysis.
- **Natural Phenomena**: Many real-world phenomena, such as height, weight, and test scores, follow a normal distribution.
- **Signal Processing**: In signal processing, noise is often modeled using a normal distribution.
- **Financial Modeling**: Financial returns, stock prices, and many economic variables are modeled as normally distributed variables in various types of quantitative finance models.

### 3. Methods Overview

- **`pdf(x)`**: Calculates the probability density at a given point \(x\).
- **`cdf(x)`**: Returns the cumulative probability for a given point \(x\).
- **`rvs()`**: Generates random values that follow the normal distribution.
- **`mean()`**: Returns the mean of the normal distribution.
- **`std()`**: Returns the standard deviation of the normal distribution.
- **`entropy()`**: Returns the entropy of the normal distribution.

### 4. Example of Calculating Mean, Variance, and Sampling

```python
# Mean and Variance of the normal distribution
mean_value = norm.mean(loc=mu, scale=sigma)
variance_value = norm.var(loc=mu, scale=sigma)

print(f"Mean of the normal distribution: {mean_value}")
print(f"Variance of the normal distribution: {variance_value}")

# Random sample generation
random_values = norm.rvs(loc=mu, scale=sigma, size=5)
print(f"Random samples: {random_values}")
```

### 5. Visualizing the Distribution

Here’s how you can visualize the PDF, CDF, and random samples of a normal distribution:

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import norm

# Parameters for the normal distribution
mu = 0  # Mean
sigma = 2  # Standard deviation

# Create x values for plotting
x = np.linspace(-10, 10, 1000)

# Probability Density Function (PDF)
pdf_values = norm.pdf(x, mu, sigma)
plt.plot(x, pdf_values, label="PDF")
plt.title(f"Normal Distribution (PDF, $\mu={mu}, \sigma={sigma}$)")
plt.xlabel("x")
plt.ylabel("Probability Density")
plt.grid(True)
plt.legend()
plt.show()

# Cumulative Distribution Function (CDF)
cdf_values = norm.cdf(x, mu, sigma)
plt.plot(x, cdf_values, label="CDF", color='r')
plt.title(f"Normal Distribution (CDF, $\mu={mu}, \sigma={sigma}$)")
plt.xlabel("x")
plt.ylabel("Cumulative Probability")
plt.grid(True)
plt.legend()
plt.show()

# Generate random samples
random_samples = norm.rvs(mu, sigma, size=1000)
plt.hist(random_samples, bins=30, density=True, alpha=0.6, color='g', label="Random Samples")
plt.plot(x, pdf_values, 'r-', label="PDF")
plt.title(f"Random Samples and Normal Distribution PDF ($\mu={mu}, \sigma={sigma}$)")
plt.xlabel("x")
plt.ylabel("Density")
plt.legend()
plt.grid(True)
plt.show()
```

### 6. Link to Official Documentation

For a detailed explanation and the full list of available methods and attributes, refer to the official documentation:  
[scipy.stats.norm Documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.norm.html)

---

## Conclusion

The `scipy.stats.norm` module is a powerful tool for working with the normal (Gaussian) distribution in Python. Whether you're calculating probabilities using the PDF and CDF, generating random samples, or visualizing the distribution, this module provides the functions needed to work effectively with the normal distribution. The normal distribution is central to many statistical methods, making `scipy.stats.norm` an essential tool for anyone working in statistics, data science, or related fields. By understanding its key functions and how to apply them, you can easily incorporate normal distributions into your analyses and models.
