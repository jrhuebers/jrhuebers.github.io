
# 1. The problem with non-autonomous dynamical systems

In a discrete non-autonomous system with state space $X$ and dynamics $x_{\ell+1} = f^\ell(x_\ell)$, the dynamics (or update rule) $f^\ell$ itself changes at every step $\ell$:
$$x_1 = f^0(x_0), \quad x_2 = f^1(x_1), \quad x_3 = f^2(x_2)$$
As a result, classic dynamical systems tools break down:
- There are no static fixed points ($f(x^*) = x^*$),
- Standard semigroup composition ($\Phi_{n+m} = \Phi_n \circ \Phi_m$) fails because $f^1 \circ f^0 \neq f^0 \circ f^1$,
- Standard eigenvalue/singular value analysis does not apply,
- Standard ergodic theorems cannot be applied directly because there is no single invariant measure.
# 2. Skew-Product Construction


> [!REMARK] Rationale
> The gist of the construction below, which is a classical approach to study non-automous dynamical systems, is to restore autonomy by:
> a. Embedding into an extended state-space $X \times \Omega$ that has a bundle structure with $\Omega$ the base space and $X$ the fiber.
> b. Endowing the bundle with a skew-product with a coupled dynamics that does not depend explicitly on time. The non-autonomous dynamics on $X$ then becomes autonomous on the bundle.
> c. Equipping $\Omega$ with a base map $\theta_t$ that acts a time-shift and satisfies a time-shift symmetry $\theta_{t+s} = \theta_t \circ \theta_s$.
>This construction leads to an autonomous system with a semi-group property.


We introduce an extended state space $(\omega,x) \in \Omega \times X$, where $\omega$ represents the current "environment" or time-ordered sequence of rules (e.g., $\omega = (f^0, f^1, f^2, \dots)$). For a feedforward neural net, these could identified with the pairs of weights and biases $(W^\ell, b^\ell)$ at each layer.

Now, define a **single global map** $\Theta: \Omega \times X \to \Omega \times X$:
$$\Theta(\omega,x) = \Big(\theta \omega , \, f_\omega(x) \Big).$$
The base shift $\theta \omega$ ticks the environment forward by one step, i.e $\omega = (f^0, f^1, \ldots, )$ and $\theta \omega = (f^1, f^2, \ldots )$. The fiber map $f_\omega(x)$ applies the current rule dictated by environment $\omega$, the first element of $\omega$ to update state $x$. Crucially, $\Theta$ is entirely autonomous. The operator $\Theta$ applied at step $\ell=0$ is identical to $\Theta$ applied at step $\ell=1000$. Time dependence has been absorbed into the second coordinate $\omega$. 

# 3. Geometry, flow maps and the cocycle law

Let $E = \Omega \times X$ be the total space of the bundle with canonical projection $\pi(\omega,x) = \omega$. Define the map $\Theta_t: E \to E$ for time duration $t$ by:
$$\Theta_t(\omega, x) = \Big( \theta_t \omega, \, \phi(t, \omega, x) \Big).$$
This map is a bundle automorphism mapping the fiber over $\omega$ to a fiber over $\theta_t \omega$ with fiber transition map $\phi(t, \omega, x)$. For $\Theta_t$ to be a continuous-time flow, i.e an autonomous dynamical system on $E$, the family of maps $\{\Theta_t\}_{t \ge 0}$ must satisfy the flow composition law:
$$\Theta_{t+s} = \Theta_t \circ \Theta_s.$$
We first evaluate both sides on an arbitrary point $(\omega, x) \in E$:
$$\Theta_{t+s}(\omega, x) = \Big( \theta_{t+s} \omega, \, \phi(t+s, \omega, x) \Big),$$
and
$$\Theta_t \big( \Theta_s(\omega, x) \big) = \Theta_t \Big( \theta_s \omega, \, \phi(s, \omega, x) \Big) = \Big( \theta_t(\theta_s \omega), \, \phi(t, \theta_s \omega, \phi(s, \omega, x)) \Big).$$
Equating the two coordinates of the output vector yields two mandatory conditions:
- Base Condition: $\theta_{t+s} = \theta_t \circ \theta_s$ (the base map satisfies the time-shift symmetry).
- Fiber Condition: $\phi(t+s, \omega, x) = \phi(t, \theta_s \omega, \phi(s, \omega, x))$ (the fiber transition map satisifies a cocycle law).

# 4. Action on the original states

## 4.a Intuitive derivation

We can track the action of the total space autonomous system on $X$ via the above defined transition maps:
$$
x_L \equiv  \phi(L, \omega, x_0) = (f^L \circ f^{L-1} \circ \cdots f^1 )(x_0).
$$
Now we can resort to a classical treatment by linearizing the dynamics. The jacobian cocycle is simply
$$
\mathcal J (L,\omega,x_0) = \frac{\partial \phi(L, \omega, x_0)}{\partial x_0} = \prod_{\ell = 1}^L J_{f^\ell} (x_{\ell -1}),
$$
where $J_{f^\ell}$ is the jacobian at iteration $\ell$.

## 4.b Clean derivation

Linearizing the autonomous skew-product flow $\Theta_t$ on the total space $E = \Omega \times X$ reveals a block-triangular Jacobian matrix, isolating the Jacobian of the transition map as the core operator governing fiber stability.

### Derivation of the Linearized Skew-Product

Let $p = (\omega, x) \in E$. The tangent space at $p$ decomposes into base and fiber components:
$$T_p E \cong T_\omega \Omega \oplus T_x X$$
A tangent vector $\mathbf{v} \in T_p E$ is written as a column vector $\mathbf{v} = (\delta \omega, \delta x)^T$. Differentiating the flow $\Theta_t(\omega, x) = (\theta_t \omega, \, \phi(t, \omega, x))$ with respect to $(\omega, x)$ yields the differential operator $D\Theta_t(\omega, x): T_p E \to T_{\Theta_t(p)} E$:
$$D\Theta_t(\omega, x) = \begin{pmatrix} D_\omega(\theta_t \omega) & D_x(\theta_t \omega) \\ D_\omega \phi(t, \omega, x) & D_x \phi(t, \omega, x) \end{pmatrix} = \begin{pmatrix} D\theta_t(\omega) & \mathbf{0} \\ D_\omega \phi(t, \omega, x) & D_x \phi(t, \omega, x) \end{pmatrix}$$

### Key Structural Implications of the Block-Triangular Form

1. Decoupling of Fiber Disturbance ($\mathbf{0}$ block):  
    Because the base dynamics $\theta_t \omega$ depends only on the environment and are completely uncoupled from the state $x$, the upper-right block is identically zero:  
    $$D_x(\theta_t \omega) = \mathbf{0}.$$
    Perturbing the fiber state $x$ has zero effect on the base environment sequence $\omega$.
    
2. The Fiber Jacobian Cocycle ($D_x \phi(t, \omega, x)$):  
    The lower-right diagonal block is the linear operator acting on purely fiber-tangent vectors $\delta x \in T_x X$:  
    $$\mathcal{J}(t, \omega, x) \equiv D_x \phi(t, \omega, x) \in \text{End}(T_x X)$$  
    This block represents the linear Jacobian cocycle. It satisfies the chain rule composition:  
    $$\mathcal{J}(t+s, \omega, x) = \mathcal{J}(t, \theta_s \omega, \phi(s, \omega, x)) \cdot \mathcal{J}(s, \omega, x)$$
    
3. Environmental Sensitivity ($D_\omega \phi(t, \omega, x)$):  
    The lower-left block measures how a perturbation in the base sequence/environment $\delta \omega$ shifts the fiber state trajectory over time.
    

### Consequences for Stability and Lyapunov Exponents

Because $D\Theta_t(\omega, x)$ is block-triangular, its spectrum (and determinant) separates into the spectra of the two diagonal blocks:

- Spectrum Separation: The global Lyapunov exponents of the autonomous system $(E, \Theta_t)$ partition into:  
    $$\text{Spec}\left(D\Theta_t\right) = \text{Spec}\left(D\theta_t\right) \cup \text{Spec}\left(D_x \phi(t, \omega, x)\right)$$
    
- Fiber Stability: If the base shift $\theta_t$ is isometric or measure-preserving (e.g., a simple time index shift $\ell \to \ell+1$ with zero base Lyapunov exponents), all dynamical instability, chaos, vanishing/exploding gradients, and attractor geometry are determined strictly by $D_x \phi(t, \omega, x)$.
    

In deep learning, this block-triangular structure proves that backpropagation through depth calculates products of $D_x \phi$ along the fiber direction, unaffected by base coordinate transformations.


# 5. Conclusion

This approach allowed us to restore the semigroup property: multi-step evolution is now standard just function iteration. Therefore:
- Ergodic Theory is applicable: If the environment shift $\theta$ preserves a probability measure on $\Omega$, the map $\Theta$ becomes a measure-preserving transformation on $X \times \Omega$. This allows applying Oseledets Multiplicative Ergodic Theorem to derive well-defined Lyapunov exponents for non-autonomous systems.
- Fiber Bundle Geometry: You can visualize $\Omega$ as a base space (the sequence of environmental conditions) and $X$ as a fiber sitting above each point in $\Omega$. As you move along the base via $\theta$, the cocycle dictates how vectors move between fibers.

# Appendix : Application to Neural Network

- Non-Autonomous View: An $L$-layer network is $L$ different, non-commuting functions applied sequentially: $x_L = f^L \circ f^{L-1} \circ \dots \circ f^1(x_0)$.
- Autonomous View: A network is $L$ iterations of a single static operator $\Theta(x, \mathbf{w}) = (f_{\mathbf{w}}(x), \text{shift}(\mathbf{w}))$ acting on the state-weight pair $(x, \mathbf{w})$.

In [[The geometry of learning in neural nets]], we map a standard feedforward architecture to a non-autonomous system, study it with this approach and make explicit links with how these network learn.

