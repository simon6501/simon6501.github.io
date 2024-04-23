---
layout: post
title: Hardware Accelerator for Transformers
---

* TOC
{:toc}

## Common Hardware Accelerator for ViT
### Overlay Architecture
- Specific design of corresponding ISA is required
![LTrans-OPU](../../../../public/images/posts/2024/2024-04-23-transformer-hardware-acclerator/LTrans-OPU.png)
<div class="caption">
  LTrans-OPU: A Low-Latency FPGA-Based Overlay Processor for Transformer Networks [FPL'23]
</div>

![OPU](../../../../public/images/posts/2024/2024-04-23-transformer-hardware-acclerator/OPU.png){: style="height: 300px; display: block; margin: 0 auto;"}
<div class="caption">
  OPU: An FPGA-Based Overlay Processor for Convolutional Neural Networks [VLSI'20]
</div>

- **Instruction blocks** are used to describe model inference, and each instruction block consists of several **instruction units**.
- There are **C-type** and **U-type** instructions in each unit, both of which are 32 bits in length. 
C-type instructions define the operations to be performed and trigger conditions, and U-type instructions pass parameters to related C-type instructions. Therefore, each C type instruction is followed by multiple U type instructions. For example, for each memory access instruction, there will be multiple U-shaped instructions to pass the corresponding memory address, memory size and other parameters.

### Stream Architecture
The stream architecture implements corresponding hardware units for **each operator** in the calculation process of the target network and optimizes them separately to take advantage of **inter-block parallelism**.
![alt text](../../../../public/images/posts/2024/2024-04-23-transformer-hardware-acclerator/stream_architecture.png){: style="height: 250px; display: block; margin: 0 auto;"}
<div class="caption">
  ViA: A Novel VisionTransformer Accelerator Based on FPGA [TCAD'22]
</div>

### Comparision
**Overlay Architecture:**

**Pros**
- Strong flexibility and applicability: The hardware supports universal inference acceleration for one/multiple models. When the model structure or configuration is updated, the underlying circuit logic does not need to be re-synthesized, only the instruction flow corresponding to the newly generated model needs to be re-synthesized by the software.

**Cons**
- The design is difficult and time-consuming: to achieve good flexibility, it is necessary to design an efficient ISA and corresponding hardware units; and additional development of supporting software compilers is required.

**Stream Architecture:**

**Pros**
- High performance: Independent computing resources are allocated to each layer of the network, which is suitable for dedicated field accelerators and can achieve very low latency. But the hardware resources occupied are relatively high. 
- High optimization: Different methods and parallel schemes can be used to optimize the implementation and implementation of each hardware core according to the computing characteristics of different layers to improve throughput.

**Cons**
- Poor flexibility: For different models or the same model with different configurations, new hardware computing units need to be designed or the circuit needs to be re-synthesized.

## Algorithm-level optimization - Quantization
PTQ4ViT: Post-training Quantization for Vision Transformers with Twin Uniform Quantization [ECCV'22](https://dl.acm.org/doi/abs/10.1007/978-3-031-19775-8_12)[github](https://github.com/hahnyuan/PTQ4ViT)

Research motivation:
- The purpose of quantization is to reduce the number of bits required to represent network weights or intermediate features to reduce the internal storage and computing costs of ViT.
- Quantization is one of the most effective methods for compressing neural networks and has achieved great success on CNNs. However, post-training quantization (PTQ) methods perform poorly on ViT, with accuracy dropping by more than 1% even in INT8 quantization.
Issues found to be resolved:
- By analyzing the quantization process of ViT, the author observed that the distribution of activation values after the Softmax and GELU functions is very different from the Gaussian distribution. And commonly used quantitative metrics such as MSE and cosine distance are not accurate in determining the optimal scaling factor.
Solution/Design Plan:
- This paper proposes a twin uniform quantization method to reduce the quantization error of activation values. And using the Hessian bootstrap metric to evaluate different scaling factors improves the accuracy of the calibration at a smaller cost. In order to achieve rapid quantification of ViT, an efficient framework PTQ4ViT was developed.
Experimental results:
- Experiments show that quantized ViT achieves nearly lossless prediction accuracy on the ImageNet classification task (the accuracy decreases when INT8 is quantized by less than 0.5%).

## Hardware-level optimization
### ViA: A Novel VisionTransformer Accelerator Based on FPGA [TCAD'22](https://ieeexplore.ieee.org/abstract/document/9925700?casa_token=W3nvGlo8ycAAAAA:VXPr0pn1PiJGKR8PpvLdLoAYJs7GK1pEyNm6tDXcH8JyrFUn9EjTcgqg9I1CzCXlHRUEdEIeQ)

Motivation:
There are obvious differences between the image data used in CV and the sequence data used in NLP. The model details of Transformers in these two fields are different. However, this difference has not been noticed in existing related accelerator designs.
- Different data structures: image data has more segmentation dimensions and redundant information than sequence data
- Different calculation processes: The shortcut mechanism in ViT has relatively regular distribution and can eliminate path dependencies through optimization.

Target:
Design an FPGA-based accelerator architecture to efficiently perform VisionTransformer model inference

Design method
- Algorithm optimization:
1. Use half-layer mapping and throughput analysis to reduce the impact of path dependencies caused by shortcut structures
2. Analyze ViT data flow and design partitioning strategies to improve computing and memory access efficiency

- Hardware design:
1. Proposed a novel ViT accelerator architecture called ViA, which features two reused processing engines with internal flows
2. Detailed analysis of the workload and required throughput of the core NSA and NMP modules to ensure efficient processing of the stream computing structure
3. Realize Swin-T model reasoning through double buffering mechanism and PE reuse

### ViTA: A Vision Transformer Inference Accelerator for Edge Applications [ISCAS'23](https://ieeexplore.ieee.org/document/10181988)

Motivation:
VisionTransformer is currently computationally intensive, making it difficult to deploy in resource-constrained edge devices. However, existing Transformet hardware accelerators are not designed for highly resource-constrained environments.

Target:
For resource-constrained FPGA devices (Zynq ZC7020 MPSoC, 53200LUT, 220DSP and 630KB BRAM), ViTA is proposed - an efficient hardware accelerator architecture that supports multiple popular ViT models.

Design method:
- Algorithm optimization:
1. Quantize all weights and activations to INT8 using PTQ for inference.
2. Analyze ViT data flow and design partitioning strategies to improve computing and memory access efficiency.
- Hardware design: 
1. Avoid repeated off-chipmemoryaccess, using head-level pipeline and inter-layer MLP optimization.
2. The weight is read through a column-based double buffering mechanism, and the calculation module performs data processing in a row-granularity pipeline.
3. Proposed a hardware accelerator based on a configurable processing element array and a corresponding scheduling scheme.

## Possible Research Fields
### Algorithm-level: Reduce the need for high bandwidth and large memory
- Low precision quantization -> One-bit LLM
- Pruning -> Sparsity matrices
- MoE

### Hardware-level: Improve the performance
- Approximate calculation/efficient implementation of nonlinear functions -> GELU/Softmax/LayerNorm
- Efficient implementation of attention mechanism and linear layer