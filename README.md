# Assignment--2: Learning Probability Density Functions using data only

## Dataset

India Air Quality Data (NO₂ concentration used as feature)

## Roll Number

102303007

Derived parameters: a_r = 1.0 b_r = 0.9

Transformation: z = x + 1.0 \* sin(0.9x)

------------------------------------------------------------------------

## Methodology

1.  Extract NO₂ values and remove invalid entries
2.  Apply nonlinear transformation to obtain z
3.  Normalize z to \[-1,1\] using min--max scaling
4.  Train a 1-D Generative Adversarial Network:
    -   Generator: noise(5-dim) → z
    -   Discriminator: classify real vs fake samples
5.  After training, generate 50k samples from generator
6.  Estimate PDF using Kernel Density Estimation (KDE)
7.  Compare learned PDF with real histogram

------------------------------------------------------------------------

## GAN Architecture

Generator: Input(5) → Linear(32) → ReLU → Linear(64) → ReLU → Linear(1)
→ Tanh

Discriminator: Input(1) → Linear(16) → LeakyReLU → Linear(16) →
LeakyReLU → Linear(1)

Loss: BCEWithLogitsLoss Training: Generator updated twice per
discriminator step

------------------------------------------------------------------------

## Observations

Mode Coverage: Generator captures the main peak of the distribution and
approximates the right-skewed behaviour.

Training Stability: Loss oscillates without collapsing, indicating
adversarial balance.

Quality of Generated Distribution: KDE curve overlaps histogram trend
showing successful density learning.

------------------------------------------------------------------------

## Conclusion

The GAN successfully learned the unknown probability density of the
transformed variable using only data samples, without assuming a
parametric distribution.
