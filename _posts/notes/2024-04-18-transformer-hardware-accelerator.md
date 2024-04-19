---
layout: post
title: Transformer Hardware Accelerator
category: notes
---

## Survey
A Survey on Transformer Compression [arXiv'24](https://arxiv.org/html/2402.05964v1)

Transformer Silicon Research [github](https://github.com/alimpk/transfomers-silicon-research)

## Transformer Hardware Accelerator on FPGA
Hardware Accelerator for MultiHead Attention and PositionWise FeedForward in the Transformer [SOCC'20](https://ieeexplore.ieee.org/abstract/document/9524802?casa_token=waZ1VVnVLHsAAAAA:WmpqhJHcrQ1SEubirzdw1WsjJyY9sbh2CNU8kP9LyS_bI1Qx6HRAFsxxdfyXNCWKcUG0rgHxg)

An Efficient Hardware Accelerator for Sparse Transformer Neural Networks [ISCAS'22](https://ieeexplore.ieee.org/abstract/document/9937659?casa_token=GU_OSiD3EkAAAAA:seTGrT2HRPaad8VXDd7TWvp0FkeSqURil1MCj8xkaEXxWgjqT3dRRVchy08jJlofdL5zm_NCOw)

Hardware Acceleration of Transformer Networks using FPGAs [PACET'22](https://ieeexplore.ieee.org/abstract/document/9976354)

Accelerating Transformer-based Deep Learning Models on FPGAs using Column Balanced Block Pruning [ISQED'21](https://ieeexplore.ieee.org/abstract/document/9424344?casa_token=OE8jWe4DwcAAAAA:lrw52KTDDBOeCqmtehQVndmbu0L2TE7EoleIaIpy3Oe9__eCqErc2VDLQcmlLZefg0RjfvH6TA)

Accommodating Transformer onto FPGA: Coupling the Balanced Model Compression and FPGA-Implementation Optimization [GLSVLSI'21](https://dl.acm.org/doi/abs/10.1145/3453688.3461739)

## Transformer Hardware Accelerator on Other Platforms
TransformerLite: Highefficiency Deployment of Large Language Models on Mobile Phone GPUs (OPPO AI Center) [arXiv'24](https://arxiv.org/abs/2403.20041)

## Software-Hardware Co-Design
TransPIM: A Memory-based Acceleration via Software-Hardware Co-Design for Transformer [HPCA'22](https://ieeexplore.ieee.org/abstract/document/9773212?casa_token=LjFoEmvTZk8AAAAA:__alwZqW1r5yDLnv8wfX3_F5EvDJxnzkRtnJcWGFeHkm0202_j5La2jAeO8rTJW2yng8GNroqA)

Accelerating Framework of Transformer by Hardware Design and Model Compression Co-Optimization [ICCAD'21](https://ieeexplore.ieee.org/abstract/document/9643586?casa_token=2d_K8HXHBCsAAAAA:Db1BdFX8JPBQB53rIQjuu2dtmBaxLvoQMiISFyHu19vxvgcRNXdFTKgaKZghaOA3c95dXIcYNQ)

A length adaptive algorithm-hardware codesign of transformer on FPGA through sparse attention and dynamic pipelining [DAC'22](https://dl.acm.org/doi/pdf/10.1145/3489517.3530585)

Adaptable Butterfly Accelerator for Attention-based NNs via Hardware and Algorithm Co-design [arxiv'22](https://arxiv.org/abs/2209.09570)

## Vision Transformer
ViA: A Novel VisionTransformer Accelerator Based on FPGA [TCAD'22](https://ieeexplore.ieee.org/abstract/document/9925700?casa_token=W3nvGlo8ycAAAAA:VXPr0pn1PiJGKR8PpvLdLoAYJs7GK1pEyNm6tDXcH8JyrFUn9EjTcgqg9I1CzCXlHRUEdEIeQ)

An FPGA-Based Reconfigurable Accelerator for Convolution-Transformer Hybrid EfficientViT [arXiv'24](https://arxiv.org/abs/2403.20230)

## Two directions:
- Software-Hardware Co-Design: Accelerating Transformer-based models by optimizing both software (parallelism, memory access, etc.) and hardware (customized accelerator, etc.)
- HLS-based Accelerator: Accelerating Transformer-based models by designing customized accelerator using HLS tools like Vivado HLS, Catapult, etc.

- Transition from transformer/vision transformer to multi-modal transformer/vision transformer