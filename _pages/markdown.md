---
permalink: /markdown/
title: "R coding and RMarkdown"
author_profile: true
redirect_from: 
  - /md/
  - /markdown.html
---

## LitSpace: a map of the literature on immigrants, entrepreneurs and trade

[![LitSpace](/images/litspace.png){: .align-left width="300px"}](/litspace/)
**[LitSpace](/litspace/)** is an interactive two-mode network of the economic literature on immigrant workers, immigrant entrepreneurs and international trade. Each paper is coded on five dimensions: who the immigrant is, the unit of observation, the outcome, the identification strategy and the country. Papers and their features are drawn as a bipartite network, so that studies sharing more features sit closer together. Dimensions can be switched on and off, papers can be coloured by strand or by their overlap with a reference paper, and the papers closest to it are ranked by Jaccard similarity. Static, publication-quality versions are produced in R (ggplot2) using correspondence analysis of the same paper × feature matrix.

**Link:** [https://lucadebenedictis.github.io/litspace/](https://lucadebenedictis.github.io/litspace/)

**Cite as:** De Benedictis, L. (2026). *LitSpace: immigrant workers, entrepreneurs and trade* [interactive literature map]. https://lucadebenedictis.github.io/litspace/

<div style="clear: both;"></div>

---

![Pub1](/images/BlodyKernel.pdf){: .align-left width="575px"} This is the best smooth interpolator I ever produced.

#-----------------------------------------------------------------
# Kernel Density Estimation with Increasing Thickening

# Generate sample data from a function
set.seed(42)

x <- seq(-3, 3, length.out = 200)

y <- sin(x) + rnorm(200, sd = 0.1)  # Function with noise

# Apply kernel smoothing with different thickening (bandwidths)
h_seq <- c(0.1, 0.3, 0.6)  # Increasing kernel width = thicker approximation

# Plot thickened approximations
plot(x, y, pch = 16, col = rgb(0, 0, 0, 0.2), main="Function Approximation by three Kernels")

for (h in h_seq) {
	smoothed <- ksmooth(x, y, kernel="normal", bandwidth=h)
	lines(smoothed, col=rgb(1, 0, 0, 0.5))
}
legend("bottomright", legend=paste("h =", h_seq), col=rgb(1, 0, 0, 0.5), lwd=2, bty = "n")

# Dynamic thickening

# Generate sample data
set.seed(42)

x <- seq(-3, 3, length.out = 200)  # X values

y <- sin(x) + rnorm(200, sd = 0.1)  # Function with noise

# Define a function that applies thickening (smoothing) with h
thickened_function <- function(x, y, h) {
	smoothed <- ksmooth(x, y, kernel = "normal", bandwidth = h)
	return(smoothed)
}

# Define a range of h values for thickening
h_values <- seq(0.05, 0.6, length.out = 10)  # Gradual thickening

# Plot original noisy data
plot(x, y, pch = 16, col = rgb(0, 0, 0, 0.2), main = "Function Approximation with Thickening",
	xlab = "x", ylab = "Smoothed Value")

# Apply thickening dynamically by iterating over h
for (h in h_values) {
	smoothed <- thickened_function(x, y, h)
	lines(smoothed, col = rgb(1, 0, 0, h/0.6), lwd = 2)  # Increasing opacity with h
}

# Add legend
legend("bottomright", legend = sprintf("h = %.2f", h_values[c(1, 5, 10)]),
	  col = rgb(1, 0, 0, h_values[c(1, 5, 10)]/0.6), lwd = 2, bty = "n", title="bloody kernel")

#-------------------------------------------------------------------



