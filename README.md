# 🔥 Hypersphere Memory Preservation Network: A Domain-Incremental Learning Method for Open-Circuit Fault Diagnosis in Power Converters

The implementation of the paper **[Hypersphere memory preservation network: a domain-incremental learning method for open-circuit fault diagnosis in power converters](PAPER_LINK)**.

> Replace `PAPER_LINK` with the official paper/DOI link after publication.

## Updating!

[NEWS!] The code and documentation of **HMPN** are being continuously updated.

## Brief introduction

The operating conditions of power converters are continuously adjusted according to actual demands, thereby leading to the continual emergence of new fault diagnosis tasks. The existing methods typically rely on retraining with all raw historical data, causing heavy storage pressure. Although source-free domain adaptation methods can alleviate the above problem, their model performance tends to be biased toward the current operating-condition task, and thus they still suffer from catastrophic forgetting in such scenarios. To this end, this study proposes a novel domain-incremental learning fault diagnosis method named **hypersphere memory preservation network (HMPN)**. Firstly, a **wavelet-structured gated recurrent unit (WSGRU)** neural network is designed to capture fault-discriminative and temporal features. Then, the **variational memory preservation(VMP)** strategy is constructed to alleviate catastrophic forgetting during continual task learning, which theoretically solves the “variance shrinkage” issue. Finally, the experimental results on the self-designed hardware platform demonstrate its superiority over state-of-the-art diagnostic methods


## Highlights

- A novel **domain-incremental learning fault diagnosis paradigm**, named the **hypersphere memory preservation network (HMPN)**, is proposed for power converters. It can continuously learn and accumulate fault knowledge from new tasks, fundamentally transforming the design methodology of conventional fault diagnosis models and effectively alleviating the substantial storage burden caused by storing historical data.
  
- This study designs a new **wavelet-structured gated recurrent unit (WSGRU)** neural network with discriminative wavelet convolution to simultaneously capture temporal dependencies and fault-discriminative information from three-phase current signals, thereby improving the open-circuit fault diagnosis performance of power converters.
  
- An innovative **variational memory preservation (VMP)** strategy is developed, which can continuously adapt to new tasks and preserve knowledge from previous tasks without storing historical data, thereby overcoming the catastrophic forgetting problem. In particular, the von Mises–Fisher (vMF) distribution is put forward to address the “variance shrinkage” problem in conventional Gaussian-based modeling, further enhancing memory preservation capability.


## Paper

**Hypersphere memory preservation network: a domain-incremental learning method for open-circuit fault diagnosis in power converters**

Yang Yu<sup>a</sup>, Quan Qian<sup>a,*</sup>, Jianghong Zhou<sup>b</sup>, Fan Wu<sup>a</sup>, Kai Chen<sup>a</sup>, Yuhua Cheng<sup>a</sup>

<sup>a</sup> School of Automation Engineering, University of Electronic Science and Technology of China, Chengdu 611731, China

<sup>b</sup> State Key Laboratory of Mechanical Transmission for Advanced Equipment, Chongqing University, Chongqing 400044, China

<sup>*</sup> Corresponding author: Quan Qian

**Paper link:** [To be updated](PAPER_LINK)

## Domain-Incremental Learning
<img width="2088" height="1280" alt="5d08edb3fea065b9f7f95f6335e3cbfe" src="https://github.com/user-attachments/assets/0f96aa4f-7ad4-460c-a307-6f5f2b18dc1e" />

## WSGRU Neural Network
<img width="1122" height="646" alt="3fa9cc6bac883c1571501881c29cfbac" src="https://github.com/user-attachments/assets/bbe5f885-9d57-46e9-a679-939e6ccfa8a7" />

## VMP Strategy
<img width="2088" height="1280" alt="5d08edb3fea065b9f7f95f6335e3cbfe" src="https://github.com/user-attachments/assets/d2514566-505d-4c30-8883-bd44cff65603" />

## Citation

If you find this work useful in your research, please consider citing our paper.
