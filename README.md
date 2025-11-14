# Towards Unified Vision Language Models for Forest Ecological Analysis in Earth Observation

![abstract](https://REO-VLM-anonymous.github.io/picx-images-hosting/abstract.6ikgjwx7vq.webp)

**Official repository for paper: _"Towards Unified Vision Language Models for Forest Ecological Analysis in Earth Observation"_ (AAAI-26 AI4ES Workshop)**

We present **REO-Instruct**, a large-scale EO benchmark designed for **both descriptive (generation) and scientific regression** tasks, with a cognitively interpretable logical chain for forest ecological analysis.

---

## 🔍 Motivation: Scientific Regression with VLMs is Different

![fig1_abstract](https://REO-VLM-anonymous.github.io/picx-images-hosting/fig1_abstract.9rjkgkwhkh.webp)

Vision-Language Models (VLMs) show strong perception and reasoning abilities, but **scientific regression** in EO brings specific challenges:

- 🔢 **Token-based outputs vs. continuous targets**  
  VLMs generate discrete tokens, while we need precise continuous variables (e.g., AGB in Mg/ha).

- 🎯 **Semantic loss vs. numeric loss**  
  Training objectives favor fluent language and semantic coherence, not numeric accuracy.

- 🧱 **Error accumulation in multi-token numbers**  
  Numbers are split into multiple tokens; one wrong token can corrupt the full value.

- 🧬 **Different feature needs for description vs. regression**  
  Human-readable descriptions rely on salient visual patterns, but scientific regression depends on subtle spectral/spatial signals invisible to the naked eye.

REO-Instruct is built exactly around these pain points: to test and drive **regression-aware VLMs for EO**.

---

## 🧠 Logical Chain: From Human Activity to Biomass

A central design of REO-Instruct is a **logical chain** that links semantic understanding and quantitative prediction in a forest ecological scenario:

> **Human activity → Land-cover classification → Ecological patch counting → Above-Ground Biomass (AGB) regression**

- **Human Activity (VQA-style)**  
  Detects anthropogenic structures and activities (urban, agriculture, infrastructure) and their ecological impacts.

- **Land-Cover Classification**  
  Assigns each patch to professional land-cover classes (e.g., closed forest, cropland), based on Copernicus Global Land Cover.

- **Ecological Patch Counting (Regression)**  
  Estimates the number of distinct ecological patches within the tile, reflecting fragmentation and biodiversity.

- **AGB Regression (Scientific Regression)**  
  Predicts Above-Ground Biomass in Mg/ha, linking EO signals and ecological structure to biophysical quantities.

This chain ensures that all tasks are:
1. **Derivable from EO inputs**,  
2. **Logically coupled** (not arbitrary multi-tasking),  
3. **Scientifically interpretable** for forest monitoring.

---

## 🌍 EO Data Design Principles & Overview

To be useful for **scientific VLMs**, REO-Instruct follows explicit **EO data construction principles**:

1. **Sufficient & Necessary Modalities**  
   - Multispectral (Sentinel-2 L2A, 13 bands, 10 m)  
   - SAR (ALOS-2 PALSAR-2, HH & HV, 25 m)  
   - RGB extracted from Sentinel-2 ([4, 3, 2])  
   These modalities jointly capture canopy structure, vegetation status, and land use.

2. **Balanced, Diverse, Representative**  
   - Wide coverage of land-cover types  
   - Broad AGB range  
   - Varied degrees of human influence  
   - Different geographic/ecological regions  
   → Aims at **generalizable** models rather than overfitting to a few ecozones.

3. **Strict Spatial Alignment**  
   - Multispectral, SAR, and RGB patches are co-registered.  
   - Each sample corresponds to a **25 × 25 pixel** patch (~250 m × 250 m), ensuring consistent observation units across sensors.

4. **Scientifically Anchored Labels**  
   - EO imagery is derived from the **AGBD dataset (2019–2020)**.  
   - AGB values are consistent with established biomass mapping efforts.

**Dataset scale**

- **1.6M** image–text pairs for training  
- ~**20K** pairs for validation  
- ~**36K** pairs for testing  

Modalities per sample:

- ✅ RGB  
- ✅ Multispectral (Sentinel-2)  
- ✅ SAR (ALOS-2 PALSAR-2, HH & HV)  

---

## ✍️ Text Annotation Design & Hybrid Human–AI Pipeline

REO-Instruct’s text annotations are not generic captions; they are **domain-aware, task-aware** and follow clear rules to reduce noise in regression:

### 1. Annotation Principles

- **Task-aligned & derivable from EO data**  
  Each question/description is designed so that the answer can be inferred from the EO patch and associated data.

- **Logically coupled across tasks**  
  Text for human activity, land cover, patch counting, and AGB is mutually consistent and respects the logical chain.

- **Clear, concise, professionally structured**  
  Slight textual perturbations can drastically change regression outputs in LLMs; we therefore avoid noisy, redundant or stylistically ambiguous descriptions.

### 2. Content Types

- **Land-Cover Descriptions**  
  - Based on Copernicus Global Land Cover classes  
  - Over 20 categories; distribution documented in the paper (Figure 3)

- **Ecological Patch Counting**  
  - Patch = continuous land cover unit with distinct ecological traits  
  - Counts describe fragmentation and habitat complexity

- **VQA for Human Activity Monitoring**  
  - Q&A about urban areas, roads, croplands, and their potential ecological impact  
  - Supports analysis of human–environment interactions (e.g., deforestation, urban sprawl)

- **AGB Values (Regression Target)**  
  - Ground-truth AGB in Mg/ha  
  - Enables direct supervision for numeric regression and joint training with text.

### 3. Generation Pipeline

- **Model-assisted generation with ChatGPT-4o**  
  - Carefully designed prompts control:  
    - Land-cover label sets  
    - Question templates (100+ templates)  
    - Separation of regression-related vs. descriptive content

- **Automatic Consistency Checks**  
  - Scripts cross-check annotations with trusted sources, e.g. Copernicus land cover.  
  - Obvious mismatches are corrected or removed.

- **Expert Manual Review (Val/Test)**  
  - Senior experts manually inspect validation and test annotations.  
  - Ensures scientific correctness and consistent terminology for benchmarking.

This **two-stage pipeline (automatic + expert)** aims to deliver a benchmark that is both **scalable** and **trustworthy**.

---

## 📊 Benchmark Tasks & Evaluation Protocols

REO-Instruct provides standardized evaluation splits and protocols for four representative tasks:

1. **Land-Cover Classification (Generation)**  
   - Metric: Overall Accuracy, Macro-averaged Precision/Recall/F1.

2. **Ecological Patch Counting (Regression)**  
   - Metrics: RMSE, MAE, R², and discretized Overall Accuracy.

3. **Human Activity Monitoring (VQA)**  
   - Metric: Answer Accuracy (%).

4. **Above-Ground Biomass (AGB) Regression (Scientific Regression)**  
   - Metrics: RMSE, MAE, R².

We benchmark both **domain-specific VLMs** (e.g., GeoChat, LHRS-Bot) and **general-purpose VLMs** (e.g., LLaVA, Qwen2-VL, ChatGPT-4o), as well as classical EO models (e.g., U-Net on multispectral inputs).

---

## 🧪 Key Findings (High-level)

- Current VLMs can handle **content understanding & VQA**, but  
  - show **low accuracy** in fine-grained land-cover classification,  
  - and **poor numeric performance** in regression tasks.

- Even with fine-tuning, **AGB regression** with VLMs often underperforms a dedicated U-Net on multispectral imagery.

- Many VLMs **refuse or fail to answer** numeric queries reliably, resulting in many “unanswerable” cases.

These results indicate that **scientific VLMs for EO need regression-aware architectures and better exploitation of multimodal EO inputs**, beyond straightforward instruction tuning.

---

## 🗂️ Dataset Download

### 🛰️ Earth Observation Imagery  
[📥 Download All](https://pan.baidu.com/s/1CZZRzqgDsbZBCc3vfgoh4w?pwd=8efp) (extraction code: `8efp`)

- Training: [📥 Download](https://pan.baidu.com/s/1IQyNrzVverciNmqjWtsnrg?pwd=5vw6) (extraction code: `5vw6`)  
- Validation: [📥 Download](https://pan.baidu.com/s/16FTPJt4zcAxq767qApH4ww?pwd=gwjy) (extraction code: `gwjy`)  
- Test: [📥 Download](https://pan.baidu.com/s/1ABSxkBR_2s7_MUz42JoF1g?pwd=y7gv) (extraction code: `y7gv`)

### 📝 Text Annotations

- Training: [Stage 1](https://drive.google.com/file/d/1cuv4B5nfYXWaozNu3Pxe3FIsiPQYwZdL/view?usp=sharing) · [Stage 2](https://drive.google.com/file/d/1UIs3lCun1l5DXbj58gJhnw2srBwG9k9E/view?usp=sharing)  
- Validation: [📥 Download](https://drive.google.com/drive/folders/1OoQDcRyuT4npc6uxHoKi-NxBMj3MSBT9?usp=sharing)  
- Test: [📥 Download](https://drive.google.com/drive/folders/1OoQDcRyuT4npc6uxHoKi-NxBMj3MSBT9?usp=sharing)

---

## 🚀 Getting Started

```bash
# Clone the repository
git clone https://github.com/your-org/REO-VLM.git
cd REO-VLM

# (Optional) Set up environment
conda create -n reo-vlm python=3.10
conda activate reo-vlm
pip install -r requirements.txt



## 📢 Release Status

- 🤗 Hugging Face Dataset: Coming Soon
- 🧠 Model Release: In Progress
- 🗺️ [TorchGeo Integration](https://www.osgeo.org/projects/torchgeo/)[ (](https://www.osgeo.org/projects/torchgeo/)with help of outstanding colleague [Adam J. Stewart](https://github.com/adamjstewart)[):](https://github.com/adamjstewart) In Progress

##

## 🙏 Acknowledgements

We gratefully acknowledge the authors of **AGBD: A Global-scale Biomass Dataset** for providing high-quality biomass-related imagery data:

- [Ghjulia Sialelli](mailto\:gsialelli@ethz.ch), Torben Peters, Jan D. Wegner, Konrad Schindler

Please also consider citing the following works if you use REO-Instruct data or biomass-related imagery:

```bibtex

@article{xue2025towards,
  title   = {Towards Unified Vision Language Models for Forest Ecological Analysis in Earth Observation},
  author  = {Xizhe Xue and Xiaoxiang Zhu},
  journal = {Proceedings of the AAAI Conference on Artificial Intelligence AI4ES workshop},
  year    = {2025}
}

```

