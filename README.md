# About This Project
This is a deep learning project for the VU Applied Deep Learning course. Shearographic 
tire inspection results can contain stickers and repair patches that must be identified. 
I want to build a neural network that segments these two object classes from tire 
measurement images, using both infrared (IR) and shearography (SG) images as complementary 
inputs to increase the available information.

# Assignment 1 - Initiate

## References
- Y. Y. Hung. Applications of digital shearography for testing of composite structures. 
  Composites Part B: Engineering 30(7), 765–773, 1999

- C. Zhang, Z. Yang, X. He, L. Deng. Deep multimodal fusion for semantic image 
  segmentation: A survey. Image and Vision Computing 105, 104042 (2021). 
  https://doi.org/10.1016/j.imavis.2020.104042

- Drygala, C., Rottmann, M., Gottschalk, H. et al. Background-foreground segmentation for 
  interior sensing in automotive industry. J.Math.Industry 12, 13 (2022). 
  https://doi.org/10.1186/s13362-022-00128-9

## Decision of a topic and project type

Title: **sticker and repair-patch segmentation in tire inspection images**

Type: **bring your own data**

## Summary

### Description
Shearographic tyre inspection produces measurement images in which two types of applied objects need to be identified: stickers and repair patches. These objects need to be detected in order to obtain information for downstream algorithms. The Shearographic Measurement System produces infrared (IR) images, which provide more information for distinguishing between the objects, as well as shearography images (SG). Rather than relying on a single modality, this project combines both types of image to provide the model with more information.  

### Approach
1. **Data collection** — obtain paired IR and SG tire measurement images from 
   the industrial partner.
2. **Annotation** — manually label the IR images (richer information) into the classes 
   sticker and repair patch to create segmentation masks; the SG images are 
   used as an additional input
3. **Model training** — train two models: a U-Net on the IR images as a 
   simple baseline, and a Enhanced U-Net with IR and SG Images with hyperparameter 
   optimization as the main approach.
4. **Validation** — evaluate the trained models on a separate, held-out test set that was 
   not used during training, to assess generalization to new images.
5. **Demo Application** — implement a GUI application capable of loading an image pair and 
   displaying the predicted sticker/repair-patch masks. Models should be switchable to 
   show differences in metrics.

### Evaluation
The models are evaluated on the held-out test set using standard segmentation metrics:

- **Primary:**
  - pixel-level F1-score
  - IoU (Intersection over Union) and mIoU (mean-IoU) between predicted and manually annotated masks, 
    reported per class (sticker, repair patch)
  - Precision
  - Recall
- **Secondary:**
  - qualitative inspection of predicted masks overlaid on the input images
  - single-modality U-Net baseline vs. Enhanced U-Net with both Image types, compared on the same 
    metrics and test set, to quantify the benefit of adding the second modality

### Dataset
Paired IR and SG tire measurement images from an industrial partner. The 
dataset cannot be shared in total, but some images will be included as examples and for 
the final presentation. Classes: sticker and repair patch.

### Work breakdown structure
| 1 | Dataset collection and preparation | Hours: 22-30 |
|----------|----------|----------|
| 1.1 | Data collection, splitting and evaluation | 5-7 |
| 1.2 | Annotation tooling & guideline setup | 3-5 |
| 1.3 | Annotation of data | 10-12 |
| 1.4 | Preprocessing pipeline (resize, normalize, mask format) | 4-6 |

| 2 | Designing and Training Model | Hours: 34-44 |
|----------|----------|----------|
| 2.1 | Training pipeline setup  | 5-7 |
| 2.2 | U-Net baseline implementation (IR only) | 8-10 |
| 2.3 | Enhanced U-Net with both Image types implementation + HPO | 15-19 |
| 2.4 | Benchmarking both models on same metric/test set | 6-8 |

| 3 | Application and Presentation | Hours: 22-30 |
|----------|----------|----------|
| 3.1 | Demo app with overlay | 10-14 |
| 3.2 | Writing the final report | 4-6 |
| 3.3 | Presentation preparation | 8-10 |

| # | # | Hours |
|----------|----------|----------|
| / | Sum | 78-104 |