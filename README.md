# 🔥 Hypersphere Memory Preservation Network: A Domain-Incremental Learning Method for Open-Circuit Fault Diagnosis in Power Converters

The implementation of the paper **[Hypersphere memory preservation network: a domain-incremental learning method for open-circuit fault diagnosis in power converters](PAPER_LINK)**.

> Replace `PAPER_LINK` with the official paper/DOI link after publication.

## Updating!

[NEWS!] The code and documentation of **HMPN** are being continuously updated.

## Brief introduction

Power converters usually operate under dynamically varying load conditions, which leads to the continual emergence of new fault diagnosis tasks. Conventional deep learning methods typically require retraining with historical data, resulting in substantial data-storage requirements. Although source-free domain adaptation methods can reduce the dependence on historical data, they are generally optimized for the current operating-condition task and may suffer from catastrophic forgetting when diagnostic tasks arrive sequentially.

To address this problem, a novel domain-incremental learning fault diagnosis method, termed **hypersphere memory preservation network (HMPN)**, is proposed. HMPN continuously adapts to newly emerging operating-condition tasks while preserving fault knowledge learned from previous tasks without storing raw historical data.

Specifically, a **wavelet-structured gated recurrent unit (WSGRU)** neural network is designed to jointly capture fault-discriminative information and temporal dependencies from three-phase current signals. Furthermore, a **variational memory preservation (VMP)** strategy is developed to constrain the parameter distribution during continual task learning. By modeling network parameters with the **von Mises–Fisher (vMF) distribution** on a unit hypersphere, the proposed strategy alleviates the "variance shrinkage" problem associated with conventional Gaussian-based parameter modeling and improves historical knowledge preservation.

The effectiveness of HMPN is validated through overlapping and non-overlapping domain-incremental tasks, cross-load extrapolation experiments, experiments on different power-converter topologies, and online fault diagnosis experiments.

## Highlights

- A novel **domain-incremental learning fault diagnosis paradigm**, termed HMPN, is developed for power converters, enabling continual learning of newly emerging diagnostic tasks without storing raw historical data.

- A new **wavelet-structured gated recurrent unit (WSGRU)** neural network with discriminative wavelet convolution is designed to simultaneously capture fault-discriminative information and temporal dependencies from three-phase current signals.

- An innovative **variational memory preservation (VMP)** strategy is proposed to preserve historical diagnostic knowledge during continual learning. The vMF distribution is introduced to avoid the "variance shrinkage" problem associated with conventional Gaussian-based parameter modeling.

- HMPN achieves an **AIA of 99.33%** and an **FGT of 1.76%** under challenging non-overlapping incremental tasks, demonstrating strong diagnostic performance and memory preservation capability.

- Experiments on different power-converter topologies and online fault diagnosis further demonstrate the generalization capability and practical application potential of HMPN.

## Paper

**Hypersphere memory preservation network: a domain-incremental learning method for open-circuit fault diagnosis in power converters**

Yang Yu<sup>a</sup>, Quan Qian<sup>a,*</sup>, Jianghong Zhou<sup>b</sup>, Fan Wu<sup>a</sup>, Kai Chen<sup>a</sup>, Yuhua Cheng<sup>a</sup>

<sup>a</sup> School of Automation Engineering, University of Electronic Science and Technology of China, Chengdu 611731, China

<sup>b</sup> State Key Laboratory of Mechanical Transmission for Advanced Equipment, Chongqing University, Chongqing 400044, China

<sup>*</sup> Corresponding author: Quan Qian

**Paper link:** [To be updated](PAPER_LINK)

---
<img width="731" height="556" alt="6826e02f6670601888024ccbaa46dc2b" src="https://github.com/user-attachments/assets/917e65b4-5f6e-4792-a1c8-7559d9075aa9" />

## HMPN

HMPN is designed for **domain-incremental fault diagnosis**, where new operating-condition tasks arrive sequentially and previously encountered raw data are unavailable.

The overall objective is to simultaneously achieve:

1. effective learning of newly emerging fault diagnosis tasks;
2. preservation of historical fault-discriminative knowledge;
3. alleviation of catastrophic forgetting;
4. reduction of historical-data storage requirements.

<!-- 
Export the corresponding framework figure from the paper
and save it as: figures/HMPN_overview.png
-->

<p align="center">
  <img src="figures/HMPN_overview.png" width="90%">
</p>

The proposed framework mainly consists of two key components:

- **WSGRU neural network:** extracts fault-discriminative information and temporal dependencies.
- **VMP strategy:** preserves historical knowledge by constraining model parameter distributions during sequential task learning.

---

## WSGRU Neural Network

The monitoring currents of power converters contain both **fault-discriminative energy information** and clear **temporal dependencies** during the evolution of open-circuit faults.

To exploit these characteristics, a **wavelet-structured gated recurrent unit (WSGRU)** is developed.

<!-- 
Use Fig. 5 in the paper.
Recommended filename:
figures/WSGRU.png
-->

<p align="center">
  <img src="figures/WSGRU.png" width="70%">
</p>

Compared with a conventional GRU, WSGRU introduces two major modifications.

### Discriminative wavelet convolution

A learnable discriminative wavelet convolution is applied to the current input signal to enhance its energy representation. The resulting wavelet features are provided to the reset gate, update gate, and candidate hidden state.

This design allows the network to extract fault-sensitive information directly from the monitored three-phase currents.

### Temporal feature modeling

The previous hidden state is processed using a `1 × 1` convolution to generate historical features for different gates.

The reset and update mechanisms then dynamically regulate the contribution of current fault information and historical information, enabling WSGRU to jointly represent:

- current fault-discriminative characteristics;
- historical temporal information;
- temporal evolution dependencies of converter faults.

---

## Variational Memory Preservation Strategy

When a neural network is continuously optimized on newly arriving tasks, parameter updates may overwrite the discriminative knowledge acquired from previous tasks, resulting in **catastrophic forgetting**.

To address this issue, the **variational memory preservation (VMP)** strategy is proposed from a Bayesian optimization perspective.

<!-- 
Use Fig. 6 in the paper.
Recommended filename:
figures/VMP.png
-->

<p align="center">
  <img src="figures/VMP.png" width="75%">
</p>

For sequential tasks, the posterior parameter distribution learned from a previous task is treated as the prior distribution for the current task.

The learning objective therefore combines:

- the classification loss for the current diagnostic task;
- the KL divergence between the current and historical parameter distributions.

In this way, the network can learn new diagnostic knowledge while constraining excessive changes in historically important parameter distributions.

### Why vMF distribution?

Conventional Gaussian-based parameter modeling may suffer from the **"variance shrinkage"** problem during sequential optimization. The variance can gradually collapse, leading to an inaccurate representation of historical knowledge and a "false memory" phenomenon.

HMPN instead models network parameters using the **von Mises–Fisher (vMF) distribution** defined on the unit hypersphere.

The vMF distribution characterizes the parameter distribution through:

- a **mean direction**, which describes the location of the parameter distribution;
- a **concentration parameter**, which describes its dispersion degree.

Therefore, historical parameter knowledge can be preserved through both **directional alignment** and **distribution concentration control**, avoiding the unbounded variance-shrinkage behavior of conventional Gaussian modeling.

---

## Domain-Incremental Learning

For each newly arriving task, HMPN is trained using **only the current task data**.

The overall continual learning procedure can be summarized as:

1. receive the current operating-condition task;
2. extract fault-discriminative and temporal features using WSGRU;
3. calculate the classification loss of the current task;
4. constrain the current parameter distribution using the historical vMF prior;
5. optimize the HMPN model;
6. update the current posterior as the prior distribution for the next task;
7. evaluate the updated model on all previously learned tasks.

This process enables HMPN to continuously accumulate fault knowledge without requiring additional storage of raw historical samples.

---

## Experimental Platform

The primary experimental platform is a self-designed fault-tolerant system based on a **Vienna rectifier topology**.

<!-- 
Use Fig. 7 in the paper.
Recommended filename:
figures/experiment_platform.png
-->

<p align="center">
  <img src="figures/experiment_platform.png" width="85%">
</p>

The experimental platform consists of:

- grid analog power supply;
- TekMDO34;
- electronic load;
- power circuit;
- industrial personal computer;
- control sampling system.

Six single-IGBT open-circuit faults are generated by controlling the switching actions of the power circuit.

### Main experimental parameters

| Parameter | Value |
| --- | --- |
| Rated DC voltage | 700 V |
| Grid-side AC voltage | 220 V |
| Controller | DSP28377S |
| Rated power | 10 kW |
| Filter capacitor | 480 μF |
| Filter inductance | 4.3 mH |
| Sampling frequency | 800 kHz |
| Control frequency | 20 kHz |
| Load-power range | 3.4–26.9 kW |

The three-phase current signals are used as monitoring signals for open-circuit fault diagnosis.

---

## Incremental Task Settings

Two domain-incremental learning scenarios are constructed to evaluate the diagnostic performance and memory preservation capability of HMPN.

### Overlapping incremental tasks

The operating-power ranges of adjacent tasks partially overlap.

| Task | Load power |
| --- | --- |
| Task 1 | 4.5–7.0 kW |
| Task 2 | 6.1–7.9 kW |
| Task 3 | 7.0–10.9 kW |
| Task 4 | 9.0–15.6 kW |

### Non-overlapping incremental tasks

The operating-power ranges of adjacent tasks are completely separated, resulting in larger distribution discrepancies and a more challenging continual-learning scenario.

| Task | Load power |
| --- | --- |
| Task 1 | 5.4–7.0 kW |
| Task 2 | 7.1–9.0 kW |
| Task 3 | 9.1–12.4 kW |
| Task 4 | 12.8–26.9 kW |

The diagnostic performance is evaluated using three metrics:

- **Acc:** classification accuracy, higher is better;
- **FGT:** forgetting measure, lower is better;
- **AIA:** average incremental accuracy, higher is better.

---

## Experimental Results

### Overlapping Incremental Tasks

HMPN achieves the best overall memory preservation and diagnostic performance among the compared methods.

| Method | FGT (%) ↓ | AIA (%) ↑ |
| --- | ---: | ---: |
| DualGaT | 4.92 | 98.45 |
| LTCDN | 3.23 | 98.87 |
| EWC | 3.08 | 99.13 |
| TCN-SE | 2.54 | 99.38 |
| MAS | 1.94 | 99.41 |
| **HMPN** | **0.15** | **99.87** |

<!-- 
Use Fig. 8 or Fig. 9 in the paper.
Recommended filename:
figures/overlapping_results.png
-->

<p align="center">
  <img src="figures/overlapping_results.png" width="85%">
</p>

### Non-overlapping Incremental Tasks

The non-overlapping setting introduces larger operating-condition discrepancies and therefore results in a substantially more challenging domain-incremental learning problem.

Nevertheless, HMPN maintains an accuracy of **94.69% on Task 1 after Phase 4**, while achieving:

- **FGT = 1.76%**
- **AIA = 99.33%**

These results demonstrate that HMPN can effectively mitigate catastrophic forgetting while retaining high diagnostic performance on newly arriving tasks.

<!-- 
Use Table V / corresponding experimental results figure.
Recommended filename:
figures/non_overlapping_results.png
-->

<p align="center">
  <img src="figures/non_overlapping_results.png" width="85%">
</p>

---

## Effectiveness of VMP

The effectiveness of the VMP strategy is evaluated by comparing three models:

1. HMPN without VMP;
2. HMPN with Gaussian-based parameter modeling;
3. HMPN with the proposed vMF-based VMP strategy.

<!-- 
Use Fig. 10 in the paper.
Recommended filename:
figures/VMP_results.png
-->

<p align="center">
  <img src="figures/VMP_results.png" width="80%">
</p>

Without VMP, the fault-feature distributions corresponding to historical tasks exhibit significant shifts during continual learning.

Gaussian-based parameter preservation alleviates this phenomenon to some extent, but it may still suffer from variance shrinkage.

After introducing the proposed vMF-based VMP strategy, the feature distributions corresponding to different historical tasks exhibit larger overlap areas and more consistent peak positions, indicating improved historical knowledge preservation.

---

## Cross-load Extrapolation

To further evaluate the generalization capability under large load variations, cross-load extrapolation experiments are conducted.

| Task | Training load | Testing load |
| --- | --- | --- |
| N1 | 9.0–26.9 kW | 4.5–5.2 kW |
| N2 | 8.4–19.6 kW | 5.1–5.8 kW |
| N3 | 4.5–7.9 kW | 12.8–16.33 kW |
| N4 | 5.4–9.0 kW | 16.3–26.9 kW |

Unlike source-free domain adaptation approaches, HMPN does **not access testing-task data for adaptation** before evaluation.

Even under this setting, HMPN achieves an average diagnostic accuracy of approximately **90.60%** and clearly outperforms the conventional deep learning comparison methods, demonstrating favorable extrapolation capability under unseen load conditions.

<!-- 
Use Fig. 11 in the paper.
Recommended filename:
figures/cross_load_results.png
-->

<p align="center">
  <img src="figures/cross_load_results.png" width="80%">
</p>

---

## Ablation Study

Ablation experiments are performed to analyze the contribution of the two major components of HMPN.

- **Model A:** HMPN without the VMP strategy.
- **Model B:** HMPN without the WSGRU network.

Removing either component results in a noticeable reduction in diagnostic performance.

In particular, removing VMP leads to a substantial degradation of the earliest learned task, confirming its critical role in mitigating catastrophic forgetting. Removing WSGRU also reduces diagnostic performance, demonstrating the importance of jointly modeling fault-discriminative information and temporal dependencies.

---

## Computational Complexity

The computational efficiency of HMPN is evaluated on a computer equipped with:

- Intel Core i5-14600KF CPU;
- 32 GB RAM;
- NVIDIA GeForce RTX 5060 Ti GPU.

For Task 1, the training time of HMPN is approximately **1.65 s per epoch**, while the testing time for a single sample is only **2.366 ms**.

Therefore, although WSGRU introduces additional training complexity, the inference efficiency remains suitable for real-time fault diagnosis.

---

## Further Experimental Study

To verify the applicability of HMPN to different converter topologies, additional experiments are conducted on a **single-phase full-bridge PWM converter**.

<!-- 
Use Fig. 15 in the paper.
Recommended filename:
figures/PWM_platform.png
-->

<p align="center">
  <img src="figures/PWM_platform.png" width="85%">
</p>

Four non-overlapping incremental tasks are constructed:

| Task | Load power |
| --- | ---: |
| Task 1 | 600 W |
| Task 2 | 1200 W |
| Task 3 | 1800 W |
| Task 4 | 2400 W |

HMPN again achieves the best overall performance:

- **FGT = 1.01%**
- **AIA = 99.65%**

The results indicate that HMPN can effectively preserve historical fault-discriminative knowledge across different power-converter topologies.

---

## Online Experiment

Online experiments are further conducted on the hardware platform to evaluate practical fault diagnosis performance.

<!-- 
Use Fig. 16 in the paper.
Recommended filename:
figures/online_experiment.png
-->

<p align="center">
  <img src="figures/online_experiment.png" width="85%">
</p>

During online operation, the converter experiences the following process:

**Normal operation → Open-circuit fault → Fault diagnosis → Fault-tolerant control → Normal recovery**

When an open-circuit fault occurs, the monitoring signals are buffered for fault diagnosis. After obtaining the diagnostic result, the fault-tolerant control system rapidly restores the converter to normal operation.

The experiment demonstrates the practical applicability of HMPN in an actual hardware environment.

---

## Citation

If you find this work useful in your research, please consider citing our paper.

```bibtex
@article{yu_hmpn,
  title  = {Hypersphere memory preservation network: a domain-incremental learning method for open-circuit fault diagnosis in power converters},
  author = {Yu, Yang and Qian, Quan and Zhou, Jianghong and Wu, Fan and Chen, Kai and Cheng, Yuhua},
  journal = {To be updated},
  year   = {To be updated},
  volume = {To be updated},
  pages  = {To be updated},
  doi    = {To be updated}
}
