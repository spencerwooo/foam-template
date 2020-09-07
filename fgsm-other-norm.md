# Extending FGSM to other norms

> The Fast Gradient Sign Method, with perturbations limited by the $\ell_\infty$ or the $\ell_2$ norm.

- [FGSM original definition](#fgsm-original-definition)
- [FGSM as a maximum allowable attack problem](#fgsm-as-a-maximum-allowable-attack-problem)
- [FGSM with other norms](#fgsm-with-other-norms)
- [References](#references)

## FGSM original definition

The **Fast Gradient Sign Method (FGSM)** by Goodfellow et al. (NIPS 2014) is designed to attack deep neural networks. The idea is to maximize certain loss function $\mathcal{J}(x; w)$ subject to an upper bound on the perturbation, for instance: $\|x-x_0\|_\infty \leq \eta$.

Formally, we define FGSM as follows. Given a loss function $\mathcal{J}(x; w)$, the FGSM creates an attack $x$ with:

$$
x=x_0+\eta\cdot \text{sign}(\nabla_x\mathcal{J}(x_0;w))
$$

Whereas the gradient is taken with respect to the input $x$ not the parameter $w$. Therefore, $\nabla_x\mathcal{J}(x_0;w)$ should be interpreted as the gradient of $\mathcal{J}$ with respect to $x$ evaluated at $x_0$. It is the gradient of the loss function. And also, because of the $\ell_\infty$ bound on the perturbation magnitude, the perturbation direction is the sign of the gradient.

## FGSM as a maximum allowable attack problem

Given a loss function $\mathcal{J}(x; w)$, if there is an optimization that will result the FGSM attack, then we can generalize FGSM to a broader class of attacks. To this end, we notice that for general (possibly nonlinear) loss functions, FGSM can be interpreted by applying a first order of approximation:

$$
\mathcal{J}(x;w)=\mathcal{J}(x_0+r;w)\approx\mathcal{J}(x_0;w)+\nabla_x\mathcal{J}(x_o;w)^Tr
$$

where $x=x_0+r$. Therefore, finding $r$ to maximize $\mathcal{J}(x_0+r;w)$ is approximately equivalent to finding $r$ which maximizes $\mathcal{J}(x; w)=\mathcal{J}(x_0+r; w)^Tr$. Hence FGSM is the solution to:

$$
\underset{r}{\textrm{maximize}}\quad\mathcal{J}(x_0;w)+\nabla_x\mathcal{J}(x_0;w)^Tr\quad\textrm{subject to}\quad\|r\|_\infty\leq\eta
$$

which can be simplifed to:

$$
\underset{r}{\textrm{minimize}}\quad-\nabla_x\mathcal{J}(x_0;w)^Tr-\mathcal{J}(x_0;w)\quad\textrm{subject to}\quad\|r\|_\infty\leq\eta
$$

where we flipped the maximization to minimization by putting a negative sign to the gradient. Here, we simplify this optimization problem's definition to:

$$
\underset{r}{\textrm{minimize}}\quad w^Tr+w_0\quad\textrm{subject to}\quad\|r\|_\infty\leq\eta
$$

<p class="callout">
  <b>Holder's Inequality:</b>
  Let $x \in \mathbb{R}^d$ and $y \in \mathbb{R}^d$, for any $p$ and $q$ that $1/p+1/q=1\ (p\in[1,\infty])$, we have the following Inequality: $-\|x\|_p\|y\|_q\leq|x^Ty|\leq\|x\|_p\|y\|_q$.
</p>

We consider the Holder's inequality (the negative side), and so, we can show that:

$$
w^Tr\geq-\|r\|_\infty\|w\|_1\geq-\eta\|w\|_1,\ \textrm{where}\ p=1, q=\infty
$$

and because we have:

$$
-\eta\|w\|_1=-\eta\sum_{i=1}^d|w_i|=-\eta\sum_{i=1}^dw_i\cdot\textrm{sign}(w_i)=-\eta \cdot w^T\cdot\textrm{sign}(w)
$$

Thus, the lower bound of $w^Tr$ is attained when $r=-\eta\cdot\textrm{sign}(w)$. Therefore, the solution to the original FGSM optimization problem is:

$$
r=-\eta\cdot\textrm{sign}(\nabla_x\mathcal{J}(x_0;w))
$$

And hence the perturbed data is $x=x_0+\eta\cdot\textrm{sign}(\nabla_x\mathcal{J}(x_0 ;w))$.

## FGSM with other norms

Considering FGSM as a maximum allowable attack problem, we can easily generalize the attack to other $\ell_p$ norms. Consider the $\ell_2$ norm. In this case, the Holder's inequality equation becomes:

$$
w^Tr\geq-\|r\|_2\|w\|_2\geq-\eta\|w\|_2,\ \textrm{where}\ p=2, q=2
$$

and thus, $w^Tr$ is minimized when $r=-\eta\cdot w / \|w\|_2$. As a result, the perturbed data becomes:

$$
x=x_0+\eta\cdot\frac{\nabla_x\mathcal{J}(x_0 ;w)}{\|\nabla_x\mathcal{J}(x_0 ;w)\|_2}
$$

## References

​[https://engineering.purdue.edu/ChanGroup/ECE595/files/chapter3.pdf](https://engineering.purdue.edu/ChanGroup/ECE595/files/chapter3.pdf)
