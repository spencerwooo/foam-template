# Image Quality Assessment

> IQA methods, based on my own research and survey.

- [Method overview](#method-overview)
- [Common algorithms](#common-algorithms)
  - [MSE and PSNR](#mse-and-psnr)
  - [Structural similarity (SSIM)](#structural-similarity-ssim)
- [References and articles](#references-and-articles)

## Method overview

Image quality assessment methods are mainly split into two categories:

1. Reference: requires a pristine (ground truth) image and a distorted image to calculate the quality score.
2. Reference-less or blind: focused on processes where there is no access to the pristine image.

The main goal of both approaches is to predict a quality score that correlates well with human perception. Currently, most new algorithms focus on feature learning, which takes a hybrid approach: automatically learning quality-aware features and associating such features to a perceived quality score.

## Common algorithms

### MSE and PSNR

<p class="callout">
Both MSE and PSNR rely on <b>reference images</b>, i.e, both these methods calculate <b>the quality of a distorted image</b> based on the difference of the perturbed image itself and the corresponding original reference clean image.
</p>

The most direct way to evaluate image quality is to compare the difference between the clean image and the distorted image, i.e, **calculate the visibility of errors.** For a clean image $I$ of size $m\times n$ and a distorted image $K$, **the $\text{MSE}$ (Mean Squared Error)** is calculated as:

$$
\textrm{MSE}=\frac{1}{m\cdot n}\sum_{i=0}^{m-1}\sum_{j=0}^{n-1}\left[I(i,j)-K(i,j)\right]^2
$$

Similarly, **the $\text{PSNR}$ (Peak Signal-to-Noise Ratio)** for grayscale images are calculated as:

$$
\textrm{PSNR}=10\cdot\log_{10}\left(\frac{\textrm{MAX}_I^2}{\textrm{MSE}}\right)
$$

Where $\text{MAX}_I^2$ is the max possible pixel value of an image. (For instance: 255 for 8-bit images, $2^B-1$ for $B$-bit images.) For colored images, we either ...

- ... calculate the $\text{MSE}$ for the 3 color channels and average them, or ...
- ... convert the image to YCbCr and calculate the Y channel $\text{PSNR}$ only. (Which is the implementation of `skimage.metrics.peak_signal_noise_ratio()`.)

### Structural similarity (SSIM)

Simple comparison based on the difference of two images doesn't comply with the results of the Humal Visual System. To make the evaluation result more human-focused, we use objective image quality assessment to determine the quality of an image. **Structural similarity, SSIM**, is the proposed method.

In SSIM, for samples $x$ and $y$ , we consider the following three factors:

1. Luminance: $l(x, y)=\frac{2\mu_x\mu_y+c_1}{\mu_x^2+\mu_y^2+c_1}$
2. Constrast: $c(x, y)=\frac{2\sigma_x\sigma_y+c_2}{\sigma_x^2+\sigma_y^2+c_2}$
3. Structure: $s(x, y)=\frac{\sigma_{xy}+c_3}{\sigma_x\sigma_y+c_3}$

Where, $\mu_x$ and $\mu_y$ are the mean of $x$ and $y$ respectively, $\sigma_x^2$ and $\sigma_y^2$ are the variance of $x$ and $y$ respectively, $\sigma_{xy}$ is the covariance of $x$ and $y$. To avoid zero division, $c_1, c_2, c_3$ are constants where $c_i=(k_iL)^2\ (i\in[1,2], L=2^B-1)$ and $c_3=c_2/2, k_1=0.01, k_2=0.03$ by default.

With this, we can calculate SSIM with:

$$
\textrm{SSIM}(x,y)=[l(x,y)^\alpha\cdot c(x,y)^\beta \cdot s(x,y)^\gamma]
$$

When $\alpha, \beta, \gamma$ are all 1, we get:

$$
\textrm{SSIM}=\frac{(2\mu_x\mu_y+c_1)(2\mu_{xy}+c_2)}{(\mu_x^2+\mu_y^2+c_1)(\sigma_x^2+\sigma_y^2+c_2)}
$$

We can calculate SSIM with: `skimage.metrics.structural_similarity()`.

## References and articles

- ​[Image Quality Assessment: A Survey](https://medium.com/@ocampor/advanced-methods-for-iqa-37581ec3c31f)​
- ​[Papers with code: Image Quality Assessment](https://paperswithcode.com/task/image-quality-assessment)​
- ​[Introducing NIMA: Neural Image Assessment - Google AI Blog](https://ai.googleblog.com/2017/12/introducing-nima-neural-image-assessment.html)​
- ​[图像质量评价指标之 PSNR 和 SSIM](https://zhuanlan.zhihu.com/p/50757421)​
- ​[图像质量评估指标 SSIM / PSNR / MSE](https://zhuanlan.zhihu.com/p/150865007)
