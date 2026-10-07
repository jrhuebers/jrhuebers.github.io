# 0. Abstract

In this note, connected to [[Conformal-1-Adaptive Conformal Geometry as a Dynamical System - Escaping Graph Contraction via Lyapunov Shifts]] we discuss how localized modes of the Jacobian cocycle are affected by dynamics, in particular geometric feedback:

1. localized diffusion modes are nearly invisible to the feedback inside their saturated core;
2. the conformal perturbation is supported on the boundary of localized regions;
3. first-order singular-vector perturbation necessarily injects mass into modes extending outside the localized support;
4. therefore localization cannot be structurally invariant under the conformal perturbation.

# 16. From Lyapunov Shift to Distributed Long-Range Sensitivity

The correlation-based Lyapunov theorem establishes that adaptive conformal geometry increases the asymptotic growth rate of the dominant sensitivity mode. We now investigate the spatial structure of this dominant mode and its implications for oversquashing.

While a positive Lyapunov correction guarantees that sensitivity survives longer, this alone does not imply that the surviving sensitivity is distributed across the graph. In principle, the dominant mode could remain highly localized on a small subset of nodes. We therefore study how the geometric feedback interacts with localization.

## 16.1 The Dominant Lyapunov Mode

Let $\mathcal J_L = J_{L-1}\cdots J_0$ denote the depth-$L$ Jacobian cocycle and  let 
$$\mathcal J_L = \sum_{k=1}^{Nd} \sigma_k(L) u_k(L) v_k(L)^\top
$$
be its singular value decomposition.

The correlation-based Lyapunov theorem implies that the dominant singular value satisfies
$$
\sigma_1(L) \gtrsim \exp\Big( L(\Lambda_{\mathrm{diff}} + \Delta\Lambda_\rho) \Big).
$$
Consequently, perturbations increasingly align with the dominant singular vector $v_1(L)$, which may be viewed as the dominant Lyapunov mode or dominant Oseledets mode.

Since
$$
\left\| \mathcal J_L x \right\| \approx \sigma_1(L) \, \big| v_1(L)^\top x \big|,
$$
the asymptotic sensitivity of the network is largely governed by this mode and increasingly so as $L$ grows.

## 16.2 When the Dominant Mode is Delocalized

Let $v_1=(v_1^{(1)},\ldots,v_1^{(N)})$ with $v_1^{(i)} \in \mathbb R^d$. Define the node energies
$$
e_i = \|v_1^{(i)}\|^2, \qquad \sum_i e_i=1.
$$
If $e_i$ is distributed over a large fraction of the graph ($e_i$ is significant for a large set of nodes $i$), then the dominant sensitivity channel is spatially extended. In that case, the surviving sensitivity encoded by the Lyapunov exponent also remains spatially distributed.

### Observation

If the dominant Lyapunov mode is delocalized, then the long-range sensitivity preserved by the positive Lyapunov shift is likewise distributed across the graph.
Consequently, oversquashing is mitigated. The remaining difficulty is therefore not persistence of sensitivity, but localization of the dominant, persistent sensitivity mode.

## 16.3 The Localization Problem

Suppose instead that the dominant mode becomes localized and let $\mathcal C \subseteq V$ be a subset of nodes satisfying
$$
\sum_{i\in\mathcal C} e_i = 1-\varepsilon, \qquad 0<\varepsilon\ll1.
$$
Then most of the surviving sensitivity is concentrated inside $\mathcal C$. Although $\sigma_1(L)$ may remain large, this sensitivity becomes trapped inside a small region of the graph.

In that situation communication between distant graph regions remains weak and oversquashing persists despite the Lyapunov gain. Thus a positive Lyapunov correction is not sufficient by itself. The surviving sensitivity must also remain spatially distributed.

Below, we uncover how adaptive conformal geometry interacts with localized dominant modes.

## 16.4 Geometric feedback induces delocalization

### Warm-Up: Singular Vector Perturbation via Symmetric Dilation

We will use a standard perturbation argument. However, standard Rayleigh perturbation theory strictly governs the eigenvectors of symmetric operators. Because the base diffusion operator $D_\ell$​ is non-symmetric, its left and right singular spaces diverge. To rigorously analyze singular vector hybridization, we must map the system to a symmetric eigenvalue problem using Stewart’s symmetric dilation (the Wielandt matrix).

Let $D_\ell​=\sum_k \sigma_k ​u_k ​v_k^\top​$ denote the singular value decomposition, where $u_k$​ and $v_k$​ are the left (output) and right (input) singular vectors. We construct the symmetric block matrix:
$$
D_\ell=
\begin{pmatrix}
0 & D_\ell^\top \\​​D_\ell​ & 0​ 
\end{pmatrix}
$$
which has eigenvalues $\pm \sigma_k$​ and corresponding orthonormal eigenvectors $\Psi_k​=1/\sqrt{2} ​​(v_k, ​u_k​​)^\top$.
### Theorem (Delocalization Through Boundary-Injected Geometric Feedback)

Let $D_\ell$ be the non-symmetric diffusion Jacobian at layer $\ell$, with isolated dominant singular value $\sigma_1​>\sigma_2$​. Let $u_1​$ and $v_1​$ be its dominant left and right singular modes, and construct the symmetric dilated mode
$$
\Psi_1​=\frac{1}{\sqrt 2}
\begin{pmatrix}
u_1 \\
v_1
\end{pmatrix}
.
$$
Let $J_\ell​=D_\ell​+R_\ell$​ with conformal feedback operator $R_\ell$​. We define the symmetrically dilated operators:
$$
\tilde D_\ell​=
\begin{pmatrix}
0 & D_\ell\\
​​D_\ell^\top & ​0​
\end{pmatrix}, \,
\tilde R_\ell ​=
\begin{pmatrix}
0 & R_\ell\\
​​R_\ell^\top & ​0
\end{pmatrix}, \, 
\tilde P_{\mathcal{C}^\perp}​=
\begin{pmatrix}
P_{\mathcal{C}^\perp} & 0\\
​0 & P_{\mathcal{C}^\perp}​​
\end{pmatrix}
,
$$
where $\tilde P_{\mathcal{C}^\perp}$ ​denotes the orthogonal projection onto nodes outside the localization region. Assume the base diffusion dynamics are localized on a node subset $\mathcal{C} \subseteq V$, i.e the symmetric dilated mode satisfies $\|\tilde P_{\mathcal{C}^\perp} \Psi_1 \| \leq \epsilon$, with $\epsilon ≪1$. 

**Assume:**

**<font color="#ff0000">(A1) Boundary-Concentrated Feedback</font>** The conformal perturbation is asymptotically concentrated near the interface $\partial \mathcal C$. This implies the geometric sensitivity vanishes inside the saturated localization core $\mathcal{C}^o$ due to the presence of the derivative of the saturating non-linearity.

**(A2) Spectral Isolation & Resolvent Boundedness** The dominant singular value is isolated $\sigma_1 > \sigma 2​$. This implies the reduced resolvent $(\sigma_1 ​I− \tilde D_\ell​)^+$ of the symmetric dilation is bounded on the orthogonal complement of $\Psi_1$​.

**(A3) Boundary Visibility** The projected dilated source term $\tilde f ​=(I − \Psi_1​\Psi_1^\top​)\tilde R_\ell \Psi_1​$ intersects a connected component that contains nodes outside the localization region:
$$
\| \tilde P_{\mathcal{C}^\perp​} \tilde f​ \| \geq \delta
$$
for some $\delta>0$.

Let $\Psi_1^\textrm{(new)} ​= \Psi_1​+ \tilde w$ denote the first-order perturbed dominant mode. Then, there exists a constant $\eta>0$ such that $\|\tilde P_{\mathcal{C}^\perp}​ \tilde w\| \geq \eta$. Consequently,
$$
\|\tilde P_{\mathcal{C}^\perp} \Psi_1^\textrm{(new)} \| \geq \eta - \epsilon.
$$
In particular, whenever $\epsilon < \eta$, the perturbed dominant singular mode carries strictly positive mass outside the localization region and therefore cannot remain fully localized.

### Proof 

<font color="#ff0000">By standard symmetric perturbation theory applied to the Wielandt block matrix, the first-order singular-mode correction satisfies the reduced-resolvent equation</font>:
$$
(\sigma_1 ​I - \tilde D_\ellℓ​) \tilde w = (I−\Psi_1 ​\Psi_1^\top) \tilde R_\ell ​\Psi_1​
$$
Define $\tilde f = (I− \Psi_1​ \Psi_1^\top​)\tilde R_\ell \Psi_1​$. By construction, $\tilde w=(\sigma_1​ I− \tilde D_\ell​)^+ \tilde f​$.

Assumption (A3) dictates that $\| \tilde P_{\mathcal{C}^\perp​} \tilde f​ \| \geq \delta$. Since the dominant singular value is isolated, Assumption (A2) implies the reduced resolvent is bounded on the relevant subspace.  The reduced resolvent admits a Neumann-series representation
$$
(\sigma_1 I-\widetilde D_\ell)^+ \propto \sum_{k=0}^{\infty} \left(\frac{\widetilde D_\ell}{\sigma_1}\right)^k
$$
on the subspace orthogonal to the dominant mode. Each power $\widetilde D_\ell^k$​ corresponds to $k$-hop diffusion along the graph. Consequently, when the source term produced by geometric feedback is concentrated on the interface $\partial\mathcal C$, the resolvent accumulates contributions from walks that leave the localization core and enter $\mathcal C^\perp$. The first-order correction therefore inherits non-vanishing mass outside the localization region,  there exists a constant $m>0$ such that $\|\tilde P_{\mathcal{C}^\perp} \tilde{w} \| \geq m ​ \|\tilde P_{\mathcal{C}^\perp} \tilde f\|$. Combining with (A3) yields $\|\tilde P_{\mathcal{C}^\perp} \tilde{w} \| \geq m \delta$. We define $\eta =m \delta>0$.

Applying the projection $\tilde P_{\mathcal{C}^\perp}$​ to the updated mode $\Psi_1^\textrm{(new)}​=\Psi_1 ​+\tilde w$ gives:
$$
\tilde P_{\mathcal{C}^\perp} \Psi_1^\textrm{(new)} =\tilde P_{\mathcal{C}^\perp} \Psi_1​ + \tilde P_{\mathcal{C}^\perp}​ \tilde w.
$$
Using the reverse triangle inequality:
$$
\|\tilde P_{\mathcal{C}^\perp} \Psi_1^\textrm{(new)}\| \geq
\|\tilde P_{\mathcal{C}^\perp} \tilde w \|​ - \|\tilde P_{\mathcal{C}^\perp}​ \Psi_1 \| 
$$
Because the unperturbed mode is localized,  $\|\tilde P_{\mathcal{C}^\perp} \Psi_1 \| \leq \epsilon$, we therefore get  $\|\tilde P_{\mathcal{C}^\perp} \Psi_1^\textrm{(new)} \| \geq \eta - \epsilon$. For a sufficiently localized initial mode where $\epsilon < \eta$, we obtain $\|\tilde P_{\mathcal{C}^\perp} \Psi_1^\textrm{(new)} \| > 0$. The right and left singular vectors making up the dominant mode therefore possess non-vanishing mass outside the localization region, proving that complete spatial localization is dynamically unstable under conformal feedback. $\square$

## 16.5 Corollary: Spatially Distributed Long-Range Sensitivity

Combining the correlation-based Lyapunov theorem with the conditional delocalization theorem yields the following consequence.

### Corollary (long-range sensitivity)

Assume:

1. persistent positive correlation, $\rho_0>0$, so that $\Delta\Lambda_\rho>0$;
2. the hypothesis of the Boundary coupling Lemma.

Then the dominant sensitivity channel is persistent, i.e $\|\mathcal J_L\| \gtrsim e^{L(\Lambda_{\mathrm{diff}} +\Delta\Lambda_\rho)}$, and the dominant sensitivity mode carries non-vanishing mass across a non-negligible portion of the graph. Therefore the surviving sensitivity is not trapped inside a localized bottleneck region.

## Interpretation

The correlation-based Lyapunov theorem explains why adaptive conformal geometry preserves sensitivity. The Mode Hybridization Conjecture explains why this sensitivity should not remain localized. Together they imply that adaptive conformal geometry simultaneously promotes persistent and distributed sensitivity.

In conclusion, adaptive conformal geometry increases the strength of the dominant sensitivity channel through a positive Lyapunov shift while simultaneously hybridizing localized dominant modes with extended graph modes, thereby redistributing the surviving sensitivity across the graph.
