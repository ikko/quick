# Handbook on `scipy.stats.binom` in Python

## Introduction to `scipy.stats.binom`

`scipy.stats.binom` is part of the SciPy library, specifically the `scipy.stats` module, and it represents a **binomial distribution**. The binomial distribution models the number of successes in a fixed number of independent Bernoulli trials (experiments with two possible outcomes, such as success or failure), each with the same probability of success.

The binomial distribution is commonly used in situations where you perform an experiment multiple times (e.g., flipping a coin, testing for defective items in a batch, etc.) and are interested in the probability of a certain number of successes.

### Official Documentation Link
For official documentation on `scipy.stats.binom`, visit the following link:  
[scipy.stats.binom Documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.binom.html)

## Key Features of `scipy.stats.binom`

The binomial distribution has two main parameters:
- **n**: The number of trials or experiments (integer).
- **p**: The probability of success on a single trial (float, between 0 and 1).

Given these parameters, the binomial distribution can be used to calculate probabilities for the number of successes in a series of trials.

### 1. Important Functions in `scipy.stats.binom`

`scipy.stats.binom` provides a variety of functions to work with the binomial distribution. The main ones include:

- **`pmf(k, n, p)`**: Probability mass function. It calculates the probability of getting exactly \(k\) successes in \(n\) trials, with a probability \(p\) of success on each trial.

- **`cdf(k, n, p)`**: Cumulative distribution function. It calculates the probability of getting \(k\) or fewer successes in \(n\) trials.

- **`sf(k, n, p)`**: Survival function. It is the complement of the CDF and calculates the probability of getting more than \(k\) successes.

- **`rvs(n, p, size)`**: Random variates (samples) from the binomial distribution. It generates an array of random numbers representing the number of successes in \(n\) trials, with success probability \(p\).

- **`mean(n, p)`**: The mean (expected value) of the binomial distribution. It is calculated as \(n \times p\).

- **`var(n, p)`**: The variance of the binomial distribution. It is calculated as \(n \times p \times (1 - p)\).

- **`std(n, p)`**: The standard deviation of the binomial distribution. It is the square root of the variance.

- **`entropy(n, p)`**: The entropy of the binomial distribution, which quantifies the uncertainty associated with the distribution.

### Example Usage

Here’s a simple example of using `scipy.stats.binom` to compute probabilities and generate random samples from a binomial distribution.

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import binom

# Parameters
n = 10  # Number of trials
p = 0.5  # Probability of success

# Probability Mass Function (PMF)
k = np.arange(0, n + 1)
pmf_values = binom.pmf(k, n, p)

# Plotting the PMF
plt.vlines(k, 0, pmf_values, colors='b', label='PMF')
plt.plot(k, pmf_values, 'bo', ms=8)
plt.title(f"Binomial Distribution PMF (n={n}, p={p})")
plt.xlabel("Number of Successes")
plt.ylabel("Probability")
plt.grid(True)
plt.show()

# Cumulative Distribution Function (CDF)
cdf_values = binom.cdf(k, n, p)

# Plotting the CDF
plt.step(k, cdf_values, where='mid', label='CDF', color='r')
plt.title(f"Binomial Distribution CDF (n={n}, p={p})")
plt.xlabel("Number of Successes")
plt.ylabel("Cumulative Probability")
plt.grid(True)
plt.show()

# Generate random samples
random_samples = binom.rvs(n, p, size=1000)

# Plot histogram of random samples
plt.hist(random_samples, bins=10, density=True, alpha=0.6, color='g', label="Random Samples")
plt.vlines(k, 0, pmf_values, colors='b', label='PMF')
plt.title("Random Samples vs. PMF")
plt.xlabel("Number of Successes")
plt.ylabel("Density")
plt.legend()
plt.grid(True)
plt.show()
```

### 2. Common Use Cases

The binomial distribution is widely used in various fields for different purposes:
- **Quality control**: Testing the proportion of defective items in a batch.
- **Marketing**: Estimating the probability of a certain number of successes (e.g., clicks or sales) in a given number of trials (e.g., website visits).
- **Medical studies**: Modeling the number of patients who respond to a treatment in a given group.
- **Games and gambling**: Modeling scenarios like flipping a coin or drawing cards with a fixed probability of a specific outcome.

### 3. Methods Overview

- **`pmf(k)`**: Calculates the probability of exactly \(k\) successes in \(n\) trials.
- **`cdf(k)`**: Returns the cumulative probability of up to \(k\) successes.
- **`rvs()`**: Generates random samples from the binomial distribution.
- **`mean()`**: Returns the expected number of successes.
- **`std()`**: Returns the standard deviation of the number of successes.

### 4. Example of Calculating Mean, Variance, and Sampling

```python
# Mean and Variance of the binomial distribution
mean_value = binom.mean(n, p)
variance_value = binom.var(n, p)

print(f"Mean of the binomial distribution: {mean_value}")
print(f"Variance of the binomial distribution: {variance_value}")

# Random sample generation
random_values = binom.rvs(n, p, size=5)
print(f"Random samples: {random_values}")
```

### 5. Visualizing the Distribution

The following code demonstrates how to visualize the PMF, CDF, and random samples of a binomial distribution.

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import binom

# Set parameters for the binomial distribution
n = 20  # Number of trials
p = 0.3  # Probability of success

# Create x values for plotting
x = np.arange(0, n+1)

# PMF
pmf_values = binom.pmf(x, n, p)
plt.vlines(x, 0, pmf_values, colors='b', label="PMF")
plt.plot(x, pmf_values, 'bo', ms=8)
plt.title(f"Binomial Distribution PMF (n={n}, p={p})")
plt.xlabel("Number of Successes")
plt.ylabel("Probability")
plt.grid(True)
plt.legend()
plt.show()

# CDF
cdf_values = binom.cdf(x, n, p)
plt.step(x, cdf_values, where='mid', label="CDF", color='r')
plt.title(f"Binomial Distribution CDF (n={n}, p={p})")
plt.xlabel("Number of Successes")
plt.ylabel("Cumulative Probability")
plt.grid(True)
plt.legend()
plt.show()

# Generate random samples
random_samples = binom.rvs(n, p, size=1000)
plt.hist(random_samples, bins=20, density=True, alpha=0.6, color='g', label="Random Samples")
plt.vlines(x, 0, pmf_values, colors='b', label="PMF")
plt.title("Random Samples and PMF of Binomial Distribution")
plt.xlabel("Number of Successes")
plt.ylabel("Density")
plt.legend()
plt.grid(True)
plt.show()
```

### 6. Link to Official Documentation

For a detailed explanation and the full list of available methods and attributes, refer to the official documentation:  
[scipy.stats.binom Documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.binom.html)

---

## Conclusion

The `scipy.stats.binom` module provides powerful tools for working with the binomial distribution in Python. Whether you're calculating probabilities, generating random samples, or visualizing the distribution, this module is a versatile and essential tool for statistical analysis and simulation. By understanding and using functions like `pmf`, `cdf`, and `rvs`, you can apply the binomial distribution to various real-world scenarios in fields such as quality control, marketing, and medical studies.
