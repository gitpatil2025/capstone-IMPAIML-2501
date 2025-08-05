# Model Card


## Model Description

**Input:**  
- RGB images of cars, typically sized to **224×224 pixels**.  
- Images may contain visible damage (e.g., dents, scratches, broken parts) or no damage at all.  
- Input format: `.jpg` or `.png` files, preprocessed with normalization and resizing.

**Output:**  
- A **binary classification**:  
  - `car` (damaged vehicle image)  
  - `non_car` (non-vehicle or irrelevant image)  
- Output includes a **confidence score** for each class.  
- Grad-CAM visualizations are optionally generated to highlight regions influencing the prediction.

**Model Architecture:**  
- The model is based on **VGG16**, a convolutional neural network pretrained on ImageNet.  
- The final layers were fine-tuned for binary classification.  
- A softmax activation is used in the output layer.  
- Grad-CAM is integrated for interpretability.



## Performance

**Evaluation Metrics:**  
- Accuracy, Precision, Recall, F1-score  
- Confusion Matrix  
- Macro and Weighted Averages

**Test Set Results (14 images):**

| Metric                  | Car Class | Non-Car Class |
|-------------------------|-----------|----------------|
| Precision               | 0.83      | 1.00           |
| Recall                  | 1.00      | 0.50           |
| F1-score                | 0.91      | 0.67           |
| Overall Accuracy        | \-        | **86%**        |
| Macro Avg F1-score      | \-        | **0.79**       |
| Weighted Avg F1-score   | \-        | **0.84**       |

**Confusion Matrix:**

```
[10  0]
[ 2  2]
```

**Performance Summary:**  

The model performs well in identifying car images, with perfect recall and strong precision. However, it struggles to consistently identify non-car images, missing half of them in the test set.



## Limitations

- **Class Imbalance**: The dataset contains significantly more car images than non-car images, which affects recall for the minority class.
- **Generalization**: The model may not generalize well to unseen damage types, lighting conditions, or vehicle models.
- **Annotation Quality**: Labels are inferred from folder structure; no bounding boxes or segmentation masks are provided.
- **Small Test Set**: Evaluation is based on a small number of samples (14), which may not reflect real-world performance.



## Trade-offs

- **High Recall for Cars vs. Low Recall for Non-Cars**: The model prioritizes detecting car damage, which may lead to false negatives for non-car images.
- **Interpretability vs. Complexity**: Grad-CAM improves transparency but adds computational overhead.
- **Speed vs. Accuracy**: VGG16 is relatively heavy, faster models (e.g., MobileNet) may be preferred for real-time applications.




