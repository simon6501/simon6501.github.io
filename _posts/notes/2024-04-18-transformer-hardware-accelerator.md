---
layout: post
title: Transformer Hardware Accelerator
category: notes
---

## Survey
A Survey on Transformer Compression [arXiv'24](https://arxiv.org/html/2402.05964v1)

A Survey on Sparsity Exploration in Transformer-Based Accelerators [electronics'23](https://www.mdpi.com/2079-9292/12/10/2299)

Transformer Silicon Research [github](https://github.com/alimpk/transfomers-silicon-research)

## Transformer Hardware Accelerator on FPGA
Hardware Accelerator for MultiHead Attention and PositionWise FeedForward in the Transformer [SOCC'20](https://ieeexplore.ieee.org/abstract/document/9524802?casa_token=waZ1VVnVLHsAAAAA:WmpqhJHcrQ1SEubirzdw1WsjJyY9sbh2CNU8kP9LyS_bI1Qx6HRAFsxxdfyXNCWKcUG0rgHxg)

An Efficient Hardware Accelerator for Sparse Transformer Neural Networks [ISCAS'22](https://ieeexplore.ieee.org/abstract/document/9937659?casa_token=GU_OSiD3EkAAAAA:seTGrT2HRPaad8VXDd7TWvp0FkeSqURil1MCj8xkaEXxWgjqT3dRRVchy08jJlofdL5zm_NCOw)

Hardware Acceleration of Transformer Networks using FPGAs [PACET'22](https://ieeexplore.ieee.org/abstract/document/9976354)

Accelerating Transformer-based Deep Learning Models on FPGAs using Column Balanced Block Pruning [ISQED'21](https://ieeexplore.ieee.org/abstract/document/9424344?casa_token=OE8jWe4DwcAAAAA:lrw52KTDDBOeCqmtehQVndmbu0L2TE7EoleIaIpy3Oe9__eCqErc2VDLQcmlLZefg0RjfvH6TA)

Accommodating Transformer onto FPGA: Coupling the Balanced Model Compression and FPGA-Implementation Optimization [GLSVLSI'21](https://dl.acm.org/doi/abs/10.1145/3453688.3461739)

## Transformer Hardware Accelerator on Other Platforms
TransformerLite: Highefficiency Deployment of Large Language Models on Mobile Phone GPUs (OPPO AI Center) [arXiv'24](https://arxiv.org/abs/2403.20041)

SwiftTron: An Efficient Hardware Accelerator for Quantized Transformers [IJCNN'23](https://arxiv.org/pdf/2304.03986.pdf)

## Vision Transformer Hardware Accelerator on FPGA
Edge-MoE: Memory-Efficient Multi-Task Vision Transformer Architecture with Task-level Sparsity via Mixture-of-Experts [ICCAD'23](https://arxiv.org/abs/2305.18691)

LTrans-OPU: A Low-Latency FPGA-Based Overlay Processor for Transformer Networks [FPL'23](https://ieeexplore.ieee.org/document/10296349)

NPE: An FPGA-based Overlay Processor for Natural Language Processing [FPGA'21](https://dl.acm.org/doi/10.1145/3431920.3439477)

## Software-Hardware Co-Design
TransPIM: A Memory-based Acceleration via Software-Hardware Co-Design for Transformer [HPCA'22](https://ieeexplore.ieee.org/abstract/document/9773212?casa_token=LjFoEmvTZk8AAAAA:__alwZqW1r5yDLnv8wfX3_F5EvDJxnzkRtnJcWGFeHkm0202_j5La2jAeO8rTJW2yng8GNroqA)

Accelerating Framework of Transformer by Hardware Design and Model Compression Co-Optimization [ICCAD'21](https://ieeexplore.ieee.org/abstract/document/9643586?casa_token=2d_K8HXHBCsAAAAA:Db1BdFX8JPBQB53rIQjuu2dtmBaxLvoQMiISFyHu19vxvgcRNXdFTKgaKZghaOA3c95dXIcYNQ)

A length adaptive algorithm-hardware codesign of transformer on FPGA through sparse attention and dynamic pipelining [DAC'22](https://dl.acm.org/doi/pdf/10.1145/3489517.3530585)

Adaptable Butterfly Accelerator for Attention-based NNs via Hardware and Algorithm Co-design [arxiv'22](https://arxiv.org/abs/2209.09570) [github](https://github.com/SamsungLabs/Butterfly_Acc)

> **Summary:**
>
> - Input sequence matters for transformer or attention-based NNs. As a result, designing an end- to-end accelerator for scalable attention-based NNs remains an open problem.
>
> Various approaches and designs have been introduced to reduce computational complexity of attention-based DNNs. However, there are drawbacks:
> - Without jointly optimizing both parts, these hardware designs lack scalability when accelerating the end-to-end attention-based NNs with different input lengths.
> - The sparsity patterns introduced by these dynamic ap- proaches are often unstructured, requiring dynamic hard- ware controllers to exploit sparsity. Such complicated con- trollers often contain larger numbers of clocking elements, and their hardware overhead increases as the transistor size reduces. 
>
> Main contributions:
> - Fine-grained structured regu- larity, which possesses regular data accesses to optimize both memory and compute efficiency
> - Static sparsity pattern, no need for dynamic hardware controllers. A novel adaptable butterfly accelerator configurable at runtime via dedicated hardware control to accelerate dif- ferent layers using a single unified engine.
> - Sparsity exploitation on both linear and attention layers
Backgrounds:
> - The self-attention mechanism in the Transformer scales quadratically in terms of computation and memory as a function of the input sequence length.
> - Numerous works adopt structured linear mappings, such as sparse and low-rank matrices, to approximate the attention matrices and/or the weight matrices in the feed- forward layers. -> **Butterfly matrices**, universal representations of structured matrices. -> In this work, FFT and butterfly matrices are mixed.
> - Notably, on both CPU and GPU, linear layers take up a significant portion of execution time, 67.9% and 79.34% respectively, when the input length is small. As the input length becomes larger, the execution time of attention layers increases gradually and becomes dominant. As such, the latency is dominated by different components depending on the length of the input sequence. 
>
> Limitations:
> * Proposed for encoder-only networks, but claimed to be extendable to decoder-only networks.

## Vision Transformer
ViA: A Novel VisionTransformer Accelerator Based on FPGA [TCAD'22](https://ieeexplore.ieee.org/abstract/document/9925700?casa_token=W3nvGlo8ycAAAAA:VXPr0pn1PiJGKR8PpvLdLoAYJs7GK1pEyNm6tDXcH8JyrFUn9EjTcgqg9I1CzCXlHRUEdEIeQ)

An FPGA-Based Reconfigurable Accelerator for Convolution-Transformer Hybrid EfficientViT [arXiv'24](https://arxiv.org/abs/2403.20230)

PTQ4ViT: Post-training Quantization for Vision Transformers with Twin Uniform Quantization [ECCV'22](https://dl.acm.org/doi/abs/10.1007/978-3-031-19775-8_12)[github](https://github.com/hahnyuan/PTQ4ViT)

ViTA: A Vision Transformer Inference Accelerator for Edge Applications [ISCAS'23](https://ieeexplore.ieee.org/document/10181988)

## Two directions:
- Software-Hardware Co-Design: Accelerating Transformer-based models by optimizing both software (parallelism, memory access, etc.) and hardware (customized accelerator, etc.)
- HLS-based Accelerator: Accelerating Transformer-based models by designing customized accelerator using HLS tools like Vivado HLS, Catapult, etc.

- Transition from transformer/vision transformer to multi-modal transformer/vision transformer