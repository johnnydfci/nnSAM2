# nnSAM2

**nnU-Net-Enhanced One-Prompt SAM2 for Few-shot Multi-Modality Segmentation and Composition Analysis of Lumbar Paraspinal Muscles**

---

## 📌 Graphical Abstract
Welcome to the **nnSAM2** repository!  
This automated deep-learning (DL) pipeline enables **few-shot segmentation of lumbar paraspinal muscles (LPM)** across multi-sequence MRI and multi-protocol CT.

---

## 🔍 Method Overview

nnSAM2 combines **SAM2** with **nnU-Net**, achieving state-of-the-art performance with only **6 annotated slices out of 19,439**, validated across six MRI and CT datasets.

---

## ⚙️ Implementation Workflow

### 1. Region Interception
- Select the **L4-L5 region** (from L3/L4 to L5/S1 disc level).  
- One representative slice per dataset is manually annotated.
- img_intercept_L4-L5_github.ipynb
- Refer to:  [img_intercept_L4-L5_github.ipynb](img_intercept_L4-L5_github.ipynb)

### 2. nnsam2 Initialization — SAM2 Pseudo-label Generation
- Use **SAM2 in a training-free manner** with single-slice prompts.  
- Pseudo-labels are generated across MRI and CT volumes within each dataset.  
- IoU scores are recorded to guide later refinement.  
- Notebooks:  
  - [Github_SAM2seg_LPM_T1W.ipynb](Github_SAM2seg_LPM_T1W.ipynb)  
  - [Github_SAM2seg_LPM_T2W.ipynb](Github_SAM2seg_LPM_T2W.ipynb)  
- For environment setup and data preparation, refer to: [Implementation_steps_sam2.md](documentation/Implementation_steps_sam2.md)

### 3. Iterative Refinement with nnU-Net
- Refine pseudo-labels through **three sequential nnU-Net models** with confidence-guided filtering.  
- Refer to: [Implementation_steps_nnunet.md](documentation/Implementation_steps_nnunet.md)

### 4. Post-Processing
- Apply largest connected component (LCC) analysis and hole filling.  
- Refer to: `nnsam2_postprocessing.ipynb`

### 5. Segmentation Accuracy Evaluation
- Evaluate performance using **Dice Similarity Coefficient (DSC)**.  
- Refer to: `nnsam2_eval_dsc.ipynb`

### 6. Quantitative Analysis
- **Muscle Volume**: MRI & CT masks  
- **Fat Ratio**: Dixon MRI  
- **CT Attenuation**: Hounsfield Units (HU)  
- Refer to: `nnsam2_quant_analysis.ipynb`


---

## 📥 Model Download
Pretrained nnSAM2 models are available:  
👉 [Download Model] (TBD)

## 📥 Data Download


### 📊 Released Annotations
- **Back-pain patients (T2W MRI):** 411 scans, 6,784 slices  
- **Back-pain patients (T1W MRI):** 415 scans, 6,849 slices  
- **TotalSegmentator (CT):** 176 scans, 2,614 slices  
- **WORD (CT):** 100 scans, 1,218 slices  

**Total:** 826 MRI scans (13,633 slices) and 276 CT scans (3,832 slices).  

👉 [Download Annotations](https://drive.google.com/drive/folders/1zBKoy3cctG5pYEWl9EAqhEqMabw_BzTy) *(no password required)*  


---

## 🙏 Acknowledgment
We acknowledge that this work builds upon the following **public datasets**:  

- **Back-pain MRI** — [Mendeley Data](https://data.mendeley.com/datasets/k57fr854j2/2)  
- **TotalSegmentator (CT)** — [Zenodo](https://zenodo.org/records/10047292)  
- **WORD (CT)** — [GitHub](https://github.com/HiLab-git/WORD)  

Our contribution is the **manual segmentation of LPM** in these datasets, which were **not originally segmented for LPM** (with the exception of *TotalSegmentator*, where we re-segmented the muscles to improve label quality).

The nnsam2 framework integrates:  
- **[SAM2](https://github.com/facebookresearch/sam2)** — Segment Anything Model 2  
- **[nnU-Net](https://github.com/MIC-DKFZ/nnUNet)** — nnU-Net


## 📄 License

This project (code and released annotations) is licensed under the **GNU General Public License v3.0 (GPL-3.0)**.  
You are free to use, modify, and distribute this work, provided that any derivative works are also released under GPL-3.0.  

For details, see the [LICENSE](LICENSE) file.

---

## 📖 Publication
TBD
