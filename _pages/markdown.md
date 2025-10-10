---
permalink: /markdown/
title: "R coding and RMarkdown"
author_profile: true
redirect_from: 
  - /md/
  - /markdown.html
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



