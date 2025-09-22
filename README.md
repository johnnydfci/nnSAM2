# nnSAM2

**nnU-Net-Enhanced One-Prompt SAM2 for Few-shot Multi-Modality Segmentation and Composition Analysis of Lumbar Paraspinal Muscles**

---

## 📌 Graphical Abstract
Welcome to the **nnSAM2** repository!  
This automated deep-learning (DL) pipeline enables **few-shot segmentation of lumbar paraspinal muscles (LPM)** across multi-sequence MRI and multi-protocol CT.

---

## 🔍 Method Overview
nnSAM2 integrates **Segment Anything Model 2 (SAM2)** with **nnU-Net** to achieve **state-of-the-art performance** using only **a single annotated slice per dataset**.  
The framework was validated on **1,219 scans (19,439 slices) from 762 participants across six datasets**, spanning T1-weighted, T2-weighted, Dixon MRI, and contrast-enahcned and plain CT.

---

## ⚙️ Implementation Workflow

### 1. Slice Annotation
- Manually annotate one representative slice per dataset (L4/L5 level).  
- Refer to: `slice_prompt_selection.ipynb`

### 2. Pseudo-label Generation
- Apply SAM2 with single-slice prompts to generate pseudo-labels.  
- Refer to: `sam2_pseudo_labeling.ipynb`

### 3. Iterative Refinement
- Refine pseudo-labels through **three sequential nnU-Net models** with confidence-guided filtering.  
- Refer to: `nnsam2_training_pipeline.md`

### 4. Post-Processing
- Apply largest connected component analysis and hole filling for segmentation masks.  
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
Public manual annotations (**826 MRI scans (13633 slices), 276 CT scans (3832 slices)**) are available:  
👉 [Download Data] (TBD)

---

## 🙏 Acknowledgment
This work builds upon:  
- Public datasets: Back-pain MRI, TotalSegmentator, WORD  
- Private datasets: AFL, AGBRESA (with ethics approvals)  

The framework integrates **SAM2** and **nnU-Net** for **minimal-supervision segmentation** and **muscle composition analysis**.

---

## 📄 License
This project is licensed under the **MIT License**.  
See the [LICENSE](LICENSE) file for details.

---

## 📖 Publication
TBD
