## Spectral Normalization

We will prove the following theorem:

**Theorem**: If the weights of a DNN are spectrally normalized [1, 2], then the function is Lipschitz continuous.

For this proof, we will start step by step, from a simple case first.

Let $f(x) = relu(wx + b)$, where $f: \mathbb{R} \rightarrow \mathbb{R}$, $w \in \mathbb{R}$, $b \in \mathbb{R}$, and $relu(x) = \max(0, x)$ is the activation function. We will prove that $f$ is Lipschitz continuous.

By definition, $w_{sn} = \frac{w}{\sigma(w)}$ is the spectrally normalized weight, where $\sigma(w)$ is the largest singular value of $w$.

Let's assume no activation function. Then 

\begin{equation}
|f(x_1) - f(x_2)| = |w_{sn}(x_1 - x_2)| = |w_{sn}||x_1 - x_2|
\end{equation}

Thus, $f$ is Lipschitz continuous with constant $|w_{sn}|$.


**References**

[1] https://pytorch.org/docs/stable/generated/torch.nn.utils.spectral_norm.html

[2] T. Miyato, T. Kataoka, M. Koyama, Y. Yoshida, ``Spectral Normalization for Generative Adversarial Networks", https://arxiv.org/abs/1802.05957


