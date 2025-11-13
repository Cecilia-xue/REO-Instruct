# Towards Unified Vision Language Models for Forest Ecological Analysis in Earth Observation

![abstract](https://REO-VLM-anonymous.github.io/picx-images-hosting/abstract.6ikgjwx7vq.webp)









**Official repository for paper: "Towards Unified Vision Language Models for Forest Ecological Analysis in Earth Observation"**

We propose **REO-Instruct**, the first unified EO benchmark supporting both regression and generation tasks.

## ⚠️ Challenges in Scientific Regression with VLMs

![fig1_abstract](https://REO-VLM-anonymous.github.io/picx-images-hosting/fig1_abstract.9rjkgkwhkh.webp)







Despite their strong semantic capabilities, VLMs face unique technical challenges in EO regression tasks:

- 🔢 **Symbolic vs. Continuous Outputs**: VLMs typically generate discrete tokens, making it difficult to accurately regress continuous numeric values like biomass.

- 📉 **Lack of Direct Numeric Optimization**: Most VLMs are optimized for token prediction, not minimizing numeric loss, limiting precision.

- 🔁 **Error Propagation in Multi-token Numbers**: Numeric values are generated as sequences of tokens, where early mistakes propagate.

- 🧩 **Modality Misalignment**: Integrating heterogeneous inputs (e.g., RGB, MS, SAR) challenges representation alignment for joint regression and generation.

## 🌍 REO-Instruct Benchmark

![1-5](https://REO-VLM-anonymous.github.io/picx-images-hosting/1-5.3nrse4tne1.webp)







###

### 🔬 Data Collection Principles

To ensure representativeness and scientific rigor, REO-Instruct was built based on the following principles:

- **Sufficient and Necessary Modalities**: Includes RGB, Multispectral (Sentinel-2), and SAR (ALOS-2) imagery for capturing diverse geospatial and spectral features.
- **Balanced and Diverse Data**: Covers a wide range of land cover types, AGB levels, geographic regions, and anthropogenic influences.
- **Scientific Domain Knowledge in Annotations**: Text annotations include expert-informed descriptions of land cover, ecological characteristics, human activities, and ground-truth AGB values.



### 🗂️ Dataset Overview

REO-Instruct is a large-scale multimodal benchmark tailored for scientific analysis in EO. It includes:

- **1.6 million** EO image-text pairs for training
- RGB, Multispectral (Sentinel-2), and SAR (ALOS-2 PALSAR-2) imagery
- Text annotations covering:
  - Land cover classification
  - Ecological patch counting
  - VQA on human activities
  - Above-Ground Biomass regression&#x20;

### 📦 Dataset Download

#### 🖼️ Earth Observation Data [📥 Download All](https://pan.baidu.com/s/1CZZRzqgDsbZBCc3vfgoh4w?pwd=8efp) (extraction code: `8efp`)

- Training (extraction code: `5vw6`) [📥 Download](https://pan.baidu.com/s/1IQyNrzVverciNmqjWtsnrg?pwd=5vw6)
- Validation (extraction code: `gwjy`) [📥 Download](https://pan.baidu.com/s/16FTPJt4zcAxq767qApH4ww?pwd=gwjy)
- Test (extraction code: `y7gv`) [📥 Download](https://pan.baidu.com/s/1ABSxkBR_2s7_MUz42JoF1g?pwd=y7gv)

#### 📝 Text Annotations

- Training [[Stage 1](https://drive.google.com/file/d/1cuv4B5nfYXWaozNu3Pxe3FIsiPQYwZdL/view?usp=sharing)] [[Stage 2](https://drive.google.com/file/d/1UIs3lCun1l5DXbj58gJhnw2srBwG9k9E/view?usp=sharing)]
- Validation [📥 Download](https://drive.google.com/drive/folders/1OoQDcRyuT4npc6uxHoKi-NxBMj3MSBT9?usp=sharing)
- Test [📥 Download](https://drive.google.com/drive/folders/1OoQDcRyuT4npc6uxHoKi-NxBMj3MSBT9?usp=sharing)



## 🚀 Getting Started

```bash
# Clone the repository
git clone https://github.com/your-org/REO-VLM.git
cd REO-VLM

# (Optional) Set up environment
conda create -n reo-vlm python=3.10
conda activate reo-vlm
pip install -r requirements.txt
```

---

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

