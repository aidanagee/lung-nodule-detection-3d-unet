# lung-nodule-detection-3d-unet
My work through and learning of a lung nodule detection model from the textbook "Deep Learning With PyTorch"


# 3D U-Net for Lung Nodule Detection in CT Scans
### Deep Learning with PyTorch — Medical Imaging Project

**Author:** Aidan Agee  
**Dataset:** [LUNA16](https://luna16.grand-challenge.org/) — Lung Nodule Analysis 2016  
**Framework:** PyTorch  
**Task:** Binary segmentation of lung nodules in 3D CT volumes

---

## Overview

This project implements a **3D U-Net** architecture for automated detection and segmentation of pulmonary nodules in chest CT scans. Early detection of lung nodules is critical for identifying potential malignancies — this model learns to segment nodule regions directly from volumetric imaging data.

This work extends my earlier project on [intracranial aneurysm detection](https://github.com/aidanagee/aneurysm-detection-rsna), applying similar 3D segmentation techniques to a different anatomical domain.

### Key Concepts Covered
- 3D convolutional neural networks for volumetric medical imaging
- U-Net encoder-decoder architecture with skip connections
- DICOM data preprocessing and normalization
- Handling severe class imbalance in medical segmentation tasks
- Dice loss and IoU evaluation metrics
- Data augmentation strategies for 3D volumes
---
## 1. Architecture: Why U-Net for Medical Segmentation?

The **U-Net** architecture was originally proposed for 2D biomedical image segmentation (Ronneberger et al., 2015) and has since become the dominant architecture for medical imaging tasks. We extend it to 3D to fully exploit the volumetric nature of CT data.

### Why U-Net works so well here:
- **Skip connections** preserve fine spatial detail lost during downsampling — critical for precise nodule boundary detection
- **Encoder-decoder structure** captures both global context (what region of the lung) and local detail (exact nodule boundary)
- **Works well with limited data** — medical datasets are small; U-Net's architecture is inherently data-efficient

### 2D vs 3D U-Net:
| Feature | 2D U-Net | 3D U-Net |
|---|---|---|
| Input | Single slice (H x W) | Full volume (D x H x W) |
| Convolutions | 2D conv | 3D conv |
| Context | Within-slice only | Full volumetric context |
| Memory cost | Low | High |
| Nodule detection | Misses inter-slice patterns | Captures full 3D shape |

For lung nodules — which are roughly spherical 3D structures — processing the full volume is significantly more effective than processing individual slices.
