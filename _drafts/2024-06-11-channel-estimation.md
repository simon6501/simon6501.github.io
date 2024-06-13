---
layout: post
title: Channel Estimation
---

* TOC
{:toc}

## Introduction of Channel Estimation
### **LS (Least Square) Estimation**
The information in this note is based on the video of Ref [1] [MIMO Communications](https://www.youtube.com/watch?v=TC19gMQ6azE&list=PLx7-Q20A1VYKwoWNCyWfErLArGLtKdS37) by Prof. Robert Heath from the University of Texas at Austin.
![channel-estimation-mobile-1](../../../../public/images/posts/2024/2024-06-11-channel-estimation/channel-estimation-modile-1.png)
<div class="caption">
  Channel Estimation for Mobile Communications
</div>
The equation $$ \hat{h} = (x^T x)^{-1} x^T y $$ represents the least squares (LS) estimation method for finding the channel $$ h $$ in a linear system model. Let's break down the components and understand the context given in the note.

#### Linear System Model
The general form of the linear system model is given by:
$$ y = hx + n $$
where:
- $$ y $$ is the received signal.
- $$ h $$ is the channel or the parameter we want to estimate.
- $$ x $$ is the transmitted signal.
- $$ n $$ is the noise.

#### Least Squares Estimation
The least squares estimation method aims to find the estimate $$ \hat{h} $$ that minimizes the squared difference between the observed values $$ y $$ and the predicted values $$ hx $$. The least squares solution is given by:
$$ \hat{h} = (x^T x)^{-1} x^T y $$

#### Explanation of the Components
- $$ x^T $$: The transpose of the matrix $$ x $$.
- $$ x^T x $$: The product of $$ x^T $$ and $$ x $$, resulting in a square matrix.
- $$ (x^T x)^{-1} $$: The inverse of the matrix $$ x^T x $$ . This exists only if $$ x^T x $$ is invertible.
- $$ x^T y $$: The product of the transpose of $$ x $$ and $$ y $$.

#### Intuition
1. **Transposing and Multiplying $$ x $$**: By transposing $$ x $$ and multiplying it by itself ($$ x^T x $$), we are constructing a matrix that encapsulates the relationships among the elements of $$ x $$. This helps in capturing the variance and correlation structure of $$ x $$.

2. **Multiplying with $$ y $$**: Multiplying the transpose of $$ x $$ with $$ y $$  ($$ x^T y $$) projects the received signal $$ y $$ onto the space spanned by the columns of $$ x $$.

3. **Inverting the Matrix**: The matrix $$ (x^T x)^{-1} $$  adjusts for the scaling and correlation in the data $$ x $$, ensuring that we get an unbiased estimate of $$ h $$.

#### Context in the Note
The note indicates this process in the context of 2G GSM and 4G LTE communications. Specifically:

2G GSM: It uses a training sequence (26 bits) for channel estimation.

4G LTE: It employs a grid of resource blocks where each block is used for channel estimation in both time and frequency domains.

In the case of 2G GSM, the least squares estimation could be used to estimate the channel based on the known training sequence, where the data $$ x $$ represents the known training bits and $$ y $$ represents the received signal during this training period.

#### Practical Issues
The note also mentions practical issues like:

Pilot Contamination: Interference from pilots in other cells. This is especially relevant in the context of **massive MIMO** systems.

Synchronization & PLL: Phase-locked loops for synchronizing the receiver.

Timing Recovery: Ensuring proper alignment of symbols in time.

TDD/FDD: Different duplexing methods (Time Division Duplexing/Frequency Division Duplexing) affect channel estimation strategies.

## Introduction of MIMO
### FD-MIMO
FD stands for Full Dimension. Therefore, FD-MIMO stands for Full Dimension MIMO. It means the antenna system that can form a beam (beams) in both horizontal and vertical direction so that it can cover (focus on) anywhere in 3D spaces. Following illustration would shows you a comparative picture between FD and conventional multi-antenna system.
![channel-estimation](../../../../public/images/posts/2024/2024-06-11-channel-estimation/5G_MassiveMIMO_FDMIMO.png)
<div class="caption">
  FD-MIMO
</div>

CSI (Channel State Information) is the key to the FD-MIMO system. It is used to form a beam in the desired direction.

### MU-MIMO
The information in this note is based on the video of Ref [1] [MIMO Communications](https://www.youtube.com/watch?v=TC19gMQ6azE&list=PLx7-Q20A1VYKwoWNCyWfErLArGLtKdS37) by Prof. Robert Heath from the University of Texas at Austin.
![MU-MIMO](../../../../public/images/posts/2024/2024-06-11-channel-estimation/MU-MIMO.png)
<div class="caption">
  MU-MIMO
</div>

#### Downlink (D.L.)
In the downlink, the base station transmits signals to multiple users. The signal model is given by:
$$ y = HWx + n $$. Importantly, $$ W $$ needs feedback of $$ \hat{H} $$ (estimated channel matrix) for effective precoding.

#### Uplink (U.L.)
In the uplink, multiple users transmit signals to the base station. The signal model is given by:
$$ y = W(Hx + n) $$. $$ W $$ requires synchronization, timing, and training for effective decoding.

#### Additional Points
- **Schedule Far Apart Users**: It's advantageous to schedule users that are spatially far apart to reduce interference and improve performance.
- **Narrowband**: In narrowband communications, it's necessary to have one $$ \hat{H} $$ (channel estimate) for each subcarrier in OFDM (Orthogonal Frequency Division Multiplexing).

### Modelling mmWave MIMO Channels
![mmWave MIMO model](../../../../public/images/posts/2024/2024-06-11-channel-estimation/MIMO-model.png)
<div class="caption">
  Modelling mmWave MIMO Channels
</div>

### Beamspace MIMO
- The strong path loss of wave propagation at mmWave frequencies necessitates the infrastructure basestations (BSs) to acquire accurate channel state information (CSI) in order to perform data detection in the uplink (UEs transmit to BS) and MU precoding in the downlink (BS transmits to UEs). 
- To optimally determine the beamforming weights, accurate CSI is not only of paramount importance for hybrid analog-digital BS architectures but also for emerging all-digital BS architectures.

#### Sparsity-based Channel Estimation
Compressive sensing (CS)-based methods like orthogonal matching pursuit (OMP). The majority of such methods uses a discretization procedure of the number of propagation paths that can be resolved in the beamspace (or angular) domain, which results in a problem widely known as basis mismatch. To avoid the basis mismatch problem, sparse channel estimation for mmWave channels can, for example, be accomplished with atomic norm minimization (ANM) or Newtonized OMP. 

Another strain of sparsity-exploiting channel-estimation methods build upon approximate message passing (AMP). While such methods promise high estimation accuracy, they suffer from a number of drawbacks when implemented in VLSI.

### Channel Estimation Approaches
Based on Ref [2], there are two types of channel estimation approaches:
- Estimating Channel Transfer Function
- Estimating DoA/DoD (Parametric)

## [Deep CNN-Based Channel Estimation for mmWave MIMO Systems](https://ieeexplore.ieee.org/document/8752012)
### Hybrid Architecture
Due to the limited physical space with closely placed antennas and prohibitive power consumption in mmWave massive MIMO systems, it is difficult to equip a dedicated radio frequency (RF) chain for each antenna. To reduce complexity and cost, phase shifter based two-stage architecture, usually called hybrid architecture, is widely used at both the transmitter and the receiver to connect a large number of antennas with much fewer RF chains.

### OFDM
Orthogonality of Functions: Two mathematical functions are orthogonal when the definite integral of their product is zero.

And the recovery of the OFDM signal is done by the DFT/IDFT operation, which is illustrated in the following figure.
![OFDM](../../../../public/images/posts/2024/2024-06-11-channel-estimation/OFDM.png)
<div class="caption">
  OFDM and DFT/IDFT
</div>

### Frequency-selective Channel Fading and Delay Spread
- Frequency-selective fading: The channel response varies with frequency.
- Delay spread: The time difference between the arrival of the first and last multipath components. The common metric to measure it is the standard deviation of the delay spread called RMS delay spread.

### Coherence Time and Coherence Bandwidth
- Coherence Time: The time duration over which the channel remains constant.
- Coherence Bandwidth: The bandwidth over which the channel remains constant. All frequencies within the coherence bandwidth experience the same channel response and will fade simultaneously. The coherence bandwidth is inversely proportional to the delay spread.

## References
- [1] [MIMO Communications](https://www.youtube.com/watch?v=TC19gMQ6azE&list=PLx7-Q20A1VYKwoWNCyWfErLArGLtKdS37)
- [2] [Parametric Channel Estimation for 3D mmWave Massive MIMO/FD-MIMO Systems](https://www.youtube.com/watch?v=aPR8a7pxpCU)