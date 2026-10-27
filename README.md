# About This Project
This is a deep learning project for the VU Applied Deep Learning course. Because anomaly finding in tire measurements through sherography can be prone to errors due to noise in background, I want to build a neural network which is capable of distinguishing between foreground (tire) and background (noise).


# Assignment 1 - Initate

## References
- Y. Y. Hung. Applications of digital shearography for testing of composite structures. Composites Part B: Engineering 30(7), 765–773, 1999

- Drygala, C., Rottmann, M., Gottschalk, H. et al. Background-foreground segmentation for interior sensing in automotive industry. J.Math.Industry 12, 13 (2022). https://doi.org/10.1186/s13362-022-00128-9

- Starovoitov, Valery & Son, Nguyen & Golub, Yuliya & Lukashevich, Maryna & Giang, Nguyen & Chau, Hoang & Son, Le. (2024). A Universal Field-of-View Mask Segmentation Method on Retinal Images From Fundus Cameras. IEEE Access. 12. 77092-77103. 10.1109/ACCESS.2024.3402125. 

## Decision of a topic and project type

Title: **tire-sidewall masking in shearography result images** 

Type: **bring your own data**

## Summary

### Description
Shearographic measurement images are rectangular, but the tire itself only occupies a 
curved, partial section of the frame — the corners and edges outside the tire surface 
are background that can introduce noise and distort downstream anomaly detection. A 
fixed geometric mask (e.g. a hardcoded circular/elliptical crop) is brittle, since it 
breaks down whenever the tire is not perfectly centered or its radius varies between 
setups. This project aims to build a neural network that segments each image into 
foreground (valid tire surface) and background (non-tire region), producing a mask 
that can be applied to delete background noise. 
The task is for example closely related to mask segmentation in 
retinal fundus imaging, where a circular camera field of view must similarly be 
separated from the surrounding rectangular frame before further processing.

### Approach
1. **Data collection** — obtain shearographic tire measurement images from the 
   industrial partner.
2. **Annotation** — manually label each image into foreground (tire surface) and 
   background (non-tire region) to create binary segmentation masks.
3. **Model training** — train a U-Net as a simple baseline, then train and optimize a 
   Mask R-CNN (with hyperparameter optimization) as the main approach, to predict the 
   foreground/background mask for unseen images.
4. **Validation** — evaluate the trained model on a separate, held-out test set that 
   was not used during training, to assess generalization to new images.
5. **Demo Application** - Implement a application with GUI which is capable of 
  loading and masking tire sidewall images. Models should be switchable to show differences in Metrics


### Evaluation
The model is evaluated on the held-out test set using standard segmentation metrics:

- **Primary:** 
  - pixel-level F1-score 
  - IoU (Intersection over Union) between predicted and manually annotated masks
- **Secondary:** 
  - qualitative inspection of masked output images to check whether 
  background regions are reliably suppressed without cutting into valid tire surface
  - U-Net baseline vs. Mask R-CNN, compared on the same metrics and test set

### Dataset
Shearographic measurment result images from an industrial partner. The dataset cannot be shared in total, but some images will be included as example and for the final presentation.
1228 Images in total. 

### Work breakdown structure
| 1 | Dataset collection and preparation | Hours: 22-30 |
|----------|----------|----------|
| 1.1 | Data collection, splitting and evaluation   | 5-7 |
| 1.2 | Annotation tooling & guideline setup | 3-5 |
| 1.3 | Annotation of data   | 10-12 |
| 1.4 | Preprocessing pipeline (resize, normalize, mask format) | 4-6 |

| 2 | Designing and Training Model | Hours: 32-40 |
|----------|----------|----------|
| 2.1 | Training pipeline setup | 4-6 |
| 2.2 | U-Net baseline implementation | 8-10 |
| 2.3 | Mask R-CNN implementation/adaptation + HPO | 14-16 |
| 2.4 | Benchmarking both models on same metric/test set | 6-8 |

| 3 | Application and Presentation | Hours: 22 - 30 |
|----------|----------|----------|
| 3.1 | Demo app with overlay   | 10-14 |
| 3.2 | Writing the final report   | 4-6 |
| 3.3 | Presentation preperation   | 8-10 |

| # | # | Hours |
|----------|----------|----------|
| / | Sum | 76 - 100 |

