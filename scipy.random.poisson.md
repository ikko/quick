# Handbook on `scipy.stats.poisson` in Python

## Introduction to `scipy.stats.poisson`

`scipy.stats.poisson` is part of the SciPy library and is used to represent the **Poisson distribution**. The Poisson distribution models the probability of a given number of events occurring in a fixed interval of time or space, provided these events happen independently and at a constant average rate.

The distribution is commonly used in scenarios such as:
- Modeling the number of customer arrivals at a service desk in a fixed time period.
- Modeling the number of accidents at a traffic intersection during a specific period.
- Estimating the number of defects in manufacturing.

The Poisson distribution has a single parameter:
- **λ (lambda)**: The average number of events in a fixed interval.

### Official Documentation Link
For the official documentation on `scipy.stats.poisson`, visit the following link:  
[scipy.stats.poisson Documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.poisson.html)

## Key Features of `scipy.stats.poisson`

The Poisson distribution has several useful methods that allow us to perform a variety of statistical operations, such as computing probabilities, generating random samples, and more.

### 1. Important Functions in `scipy.stats.poisson`

Here are some of the key functions provided by the `scipy.stats.poisson` module:

- **`pmf(k, mu)`**: Probability mass function. It calculates the probability of observing exactly \(k\) events when the expected number of events is \(\mu\) (lambda).

- **`cdf(k, mu)`**: Cumulative distribution function. It calculates the probability of observing \(k\) or fewer events.

- **`sf(k, mu)`**: Survival function. This is the complement of the CDF and gives the probability of observing more than \(k\) events.

- **`ppf(q, mu)`**: Percent point function (inverse of CDF). It returns the number of events \(k\) for which the cumulative probability is \(q\).

- **`rvs(mu, size)`**: Random variates (samples). It generates random values that follow a Poisson distribution with parameter \(\mu\).

- **`mean(mu)`**: Returns the mean (expected value) of the Poisson distribution, which is equal to \(\mu\).

- **`var(mu)`**: Returns the variance of the Poisson distribution, which is also equal to \(\mu\).

- **`std(mu)`**: The standard deviation of the Poisson distribution, which is the square root of \(\mu\).

- **`entropy(mu)`**: The entropy of the Poisson distribution, which measures the uncertainty or randomness.

### Example Usage

Here’s an example demonstrating how to use `scipy.stats.poisson` to calculate probabilities, generate random samples, and visualize the distribution.

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import poisson

# Parameters
mu = 3  # Average rate (lambda)

# Probability Mass Function (PMF)
k = np.arange(0, 10)  # Number of events (k)
pmf_values = poisson.pmf(k, mu)

# Plotting the PMF
plt.vlines(k, 0, pmf_values, colors='b', label="PMF")
plt.plot(k, pmf_values, 'bo', ms=8)
plt.title(f"Poisson Distribution (PMF, λ={mu})")
plt.xlabel("Number of Events (k)")
plt.ylabel("Probability")
plt.grid(True)
plt.legend()
plt.show()

# Cumulative Distribution Function (CDF)
cdf_values = poisson.cdf(k, mu)

# Plotting the CDF
plt.plot(k, cdf_values, label="CDF", color='r')
plt.title(f"Poisson Distribution (CDF, λ={mu})")
plt.xlabel("Number of Events (k)")
plt.ylabel("Cumulative Probability")
plt.grid(True)
plt.legend()
plt.show()

# Generate random samples
random_samples = poisson.rvs(mu, size=1000)

# Plot histogram of random samples
plt.hist(random_samples, bins=30, density=True, alpha=0.6, color='g', label="Random Samples")
plt.vlines(k, 0, pmf_values, colors='b', label="PMF")
plt.title(f"Random Samples and PMF of Poisson Distribution (λ={mu})")
plt.xlabel("Number of Events (k)")
plt.ylabel("Density")
plt.legend()
plt.grid(True)
plt.show()
```

### 2. Common Use Cases

The Poisson distribution is widely used in many areas, particularly in cases where events occur randomly and independently over time or space:
- **Queueing Theory**: Estimating the number of customers arriving at a service desk in a given time.
- **Telecommunications**: Modeling the number of phone calls arriving at a switchboard within a time period.
- **Biology**: Estimating the number of mutations in a segment of DNA or the number of occurrences of a specific type of bacteria in a sample.
- **Traffic Flow**: Estimating the number of cars passing through an intersection in a given time frame.
- **Manufacturing**: Modeling the number of defects in a batch of products.

### 3. Methods Overview

- **`pmf(k)`**: Computes the probability of observing exactly \(k\) events.
- **`cdf(k)`**: Computes the probability of observing \(k\) or fewer events.
- **`rvs()`**: Generates random values that follow a Poisson distribution.
- **`mean()`**: Returns the mean (λ) of the Poisson distribution.
- **`var()`**: Returns the variance (λ) of the Poisson distribution.
- **`std()`**: Returns the standard deviation (\(\sqrt{\lambda}\)) of the Poisson distribution.
- **`entropy()`**: Returns the entropy of the Poisson distribution.

### 4. Example of Calculating Mean, Variance, and Sampling

```python
# Mean and Variance of the Poisson distribution
mean_value = poisson.mean(mu)
variance_value = poisson.var(mu)

print(f"Mean of the Poisson distribution: {mean_value}")
print(f"Variance of the Poisson distribution: {variance_value}")

# Random sample generation
random_values = poisson.rvs(mu, size=5)
print(f"Random samples: {random_values}")
```

### 5. Visualizing the Distribution

Here’s an example of visualizing the Poisson distribution using the PMF, CDF, and random samples.

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import poisson

# Set parameters for the Poisson distribution
mu = 4  # Average rate (lambda)

# Create x values for plotting
k = np.arange(0, 15)

# Probability Mass Function (PMF)
pmf_values = poisson.pmf(k, mu)
plt.vlines(k, 0, pmf_values, colors='b', label="PMF")
plt.plot(k, pmf_values, 'bo', ms=8)
plt.title(f"Poisson Distribution (PMF, λ={mu})")
plt.xlabel("Number of Events (k)")
plt.ylabel("Probability")
plt.grid(True)
plt.legend()
plt.show()

# Cumulative Distribution Function (CDF)
cdf_values = poisson.cdf(k, mu)
plt.plot(k, cdf_values, label="CDF", color='r')
plt.title(f"Poisson Distribution (CDF, λ={mu})")
plt.xlabel("Number of Events (k)")
plt.ylabel("Cumulative Probability")
plt.grid(True)
plt.legend()
plt.show()

# Generate random samples
random_samples = poisson.rvs(mu, size=1000)
plt.hist(random_samples, bins=30, density=True, alpha=0.6, color='g', label="Random Samples")
plt.vlines(k, 0, pmf_values, colors='b', label="PMF")
plt.title(f"Random Samples and Poisson Distribution PMF (λ={mu})")
plt.xlabel("Number of Events (k)")
plt.ylabel("Density")
plt.legend()
plt.grid(True)
plt.show()
```

### 6. Link to Official Documentation

For a detailed explanation and the full list of available methods and attributes, refer to the official documentation:  
[scipy.stats.poisson Documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.poisson.html)

---

## Conclusion

The `scipy.stats.poisson` module provides powerful tools to work with the Poisson distribution in Python. Whether you're calculating probabilities, generating random samples, or visualizing the distribution, this module offers all the necessary functions to handle Poisson-related statistical tasks effectively. The Poisson distribution is widely applicable in fields such as queueing theory, telecommunications, biology, traffic flow, and manufacturing, making `scipy.stats.poisson` an essential tool for anyone working in these areas. By understanding and utilizing the methods provided by this module, you can easily incorporate Poisson processes into your analyses and models.
