
# KITTI Road Segmentation and Robustness Evaluation

A deep learning project for pixel-level road segmentation using a custom U-Net architecture built with TensorFlow/Keras, extended with robustness testing under synthetic image degradation.

## Key Results

| Metric | Result |
|:---|---:|
| Clean validation images | 58 |
| Mean Dice score | **0.9499** |
| Mean Intersection over Union (IoU) | **0.9076** |
| Validation pixel accuracy | Approximately **0.985** |
| Image degradation types tested | 4 |
| Severity levels per degradation | 3 |

### Project Highlights

- Implemented a U-Net model for binary road segmentation on KITTI road-scene images.
- Built image preprocessing, mask conversion, and TensorFlow data pipelines.
- Evaluated segmentation performance under synthetic blur, brightness reduction, Gaussian noise, and fog.
- Compared Dice and IoU scores across increasing degradation severity levels.

> **Note:** The robustness results represent synthetic image-corruption tests, not real-world adverse-weather evaluation.

## Project Overview

Road segmentation is a computer vision task that identifies road pixels in an image. This project uses the KITTI Road dataset to train a U-Net model that separates the road from the background.

In addition to evaluating segmentation on clean validation images, the project examines how image quality changes affect model predictions. The same trained model is evaluated on synthetically degraded images without retraining.

## Visual Results

<img width="2979" height="3362" alt="segmentation_comparison" src="https://github.com/user-attachments/assets/08d791b5-1618-4c0d-94e5-95fae16f8413" />

## Robustness Evaluation

Four synthetic image degradations were tested at three severity levels.

| Condition | Severity 1 Dice | Severity 2 Dice | Severity 3 Dice |
|:---|---:|---:|---:|
| Blur | 0.9296 | 0.8756 | 0.8209 |
| Brightness reduction | 0.9239 | 0.7861 | 0.1410 |
| Synthetic fog | 0.9060 | 0.6784 | 0.5299 |
| Gaussian noise | 0.9428 | 0.3967 | 0.0001 |

**Clean baseline:** Dice = **0.9499**; IoU = **0.9076**.

The results show that segmentation performance decreased under stronger corruption settings. The largest drops occurred with severe brightness reduction and Gaussian noise in the tested configurations.

<img width="800" height="473" alt="image" src="https://github.com/user-attachments/assets/18aa113f-b365-4164-a2aa-eee1e29fe3c1" />

## Implementation Details

### Dataset Preparation

- Used KITTI road-scene images and their corresponding color-coded segmentation masks.
- Paired images with the correct ground-truth masks.
- Converted road annotations into binary masks.
- Resized images and masks to **256 × 512**.
- Normalized image pixel values to `[0, 1]`.
- Created a training and validation split using a fixed random seed.

### U-Net Model

- Implemented a U-Net encoder-decoder architecture with skip connections.
- Used TensorFlow and Keras for model construction and training.
- Trained the model using binary cross-entropy and monitored Dice-based performance.
- Applied early stopping with restoration of the best validation-loss weights.

### Image Degradation Tests

- **Blur:** Reduced image sharpness.
- **Brightness reduction:** Simulated lower illumination.
- **Gaussian noise:** Added random pixel-level noise.
- **Synthetic fog:** Reduced image contrast using a pale overlay.

The model was evaluated on the same validation images under clean and degraded conditions.

## Evaluation Metrics

- **Dice coefficient:** Measures overlap between the predicted road region and the ground-truth mask.
- **Intersection over Union (IoU):** Measures intersection relative to the union of predicted and ground-truth road pixels.
- **Pixel accuracy:** Measures the proportion of correctly classified pixels.

## Technologies

- Python
- TensorFlow and Keras
- OpenCV
- NumPy and Pandas
- Matplotlib


## Limitations

- Robustness testing uses synthetic image corruptions rather than real adverse-weather recordings.
- The evaluation covers 58 validation images.
- Results depend on the selected corruption methods and severity settings.
- The project does not evaluate a method for improving robustness.

## Possible Extensions

- Test the model on real adverse-weather road images.
- Compare U-Net with another segmentation architecture.
- Evaluate image preprocessing or augmentation methods for robustness improvement.
- Investigate how visual degradation affects downstream autonomous-driving perception.



<img width="1090" height="137" alt="image" src="https://github.com/user-attachments/assets/77ea669c-26ee-475a-88d9-79861bbb2aae" />

<img width="1061" height="193" alt="image" src="https://github.com/user-attachments/assets/78d008f0-1f08-4882-a02c-b788605cd186" />


