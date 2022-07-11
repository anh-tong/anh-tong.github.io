---
---



As in the recent post, we reviewed the notion of signatures which is a useful tool to charaterize time series data and can be used as a good representation learning for such data. 

In this post, the agenda will be the description of signature kernels and an implementation in JAX.

### Motivation:

### PDE:


### Numerical procedure.


### Auto-diff


As stated in Theorem 4.1

$$
k_{\gamma}(X, Y) = \int_0^T\int_0^T U(s,t) \tilde{U}(T-s, T - t) (\dot{\gamma}_s^\top \dot{Y}_t) ds dt
$$


To have a custom backward, we follow 2 steps: (1) defining a function with the decorator `jax.custom_vjp`; (2) implement forward function and backward function. This resembles the way that one implements custom function in `torch` by writing a class that inherits `torch.autograd.Function`. 

Note that our code is just the reimplementation of this [PyTorch code](https://github.com/crispitagorico/sigkernel/). The main point here is that we try to improve the readability in the code as well as provide a library in JAX.

Using JAX may have the befinits including using `vmap` over batch dimensions which the PyTorch code for CPU needs a double for-loop. Also, JAX will enjoy `jit` rather than using Cython like the Pytorch code.

