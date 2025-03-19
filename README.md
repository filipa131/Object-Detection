# Safety Helmet and Reflective Jacket Detection

This project focuses on training a YOLO11n model to detect safety helmets and reflective jackets worn by individuals. The goal is to accurately identify whether a person is wearing a safety helmet and/or a reflective jacket using computer vision techniques.

## Dataset

The dataset used in this project contains images of individuals wearing safety helmets and reflective jackets. The dataset has been split into three parts:

- **Train**: Training images and labels
- **Validation**: Validation images and labels
- **Test**: Test images (used to evaluate the trained model)

You can access the dataset from Kaggle:
[Safety Helmet and Reflective Jacket Dataset](https://www.kaggle.com/datasets/niravnaik/safety-helmet-and-reflective-jacket)

### Dataset Structure

```text
/safety-Helmet-Reflective-Jacket
├── train
│   ├── images
│   └── labels
├── valid
│   ├── images
│   └── labels
├── test
│   ├── images
│   └── labels
├── data.yaml
```

## Model Training

The model is based on YOLO11n, and the training process involves the following steps:

1. **Prepare the Dataset**: Create correct `data.yaml` file to define the paths for training, validation, and test images, as well as the class names (helmet, jacket).

2. **Train the Model**: The model is trained for 10 epochs with a batch size of 4 and an image size of 640. The training script automatically adjusts the optimizer, learning rate, and momentum.

3. **Model Configuration**: The `yolo11n` model is used for the task, and the model architecture is adapted to handle two classes: `helmet` and `jacket`.

## Model Evaluation

During the training process, the model's performance is evaluated based on several metrics, such as precision, recall, and mAP (mean Average Precision). These metrics help assess the accuracy of the model in detecting helmets and jackets in the images.

After training, the best model weights are saved for further use.

## Testing the Model

Once the model is trained, you can evaluate its performance on unseen test data. The test dataset contains images that the model has never seen during training. The model's predictions are visualized to show the detected helmets and jackets in the test images.

## Results

After training for 10 epochs, the model achieved the following performance metrics:

- **Precision**: 91.2%
- **Recall**: 87.4%
- **mAP50**: 94.5%
- **mAP50-95**: 72.2%

## Video Processing

After training the model, the next step is to evaluate its performance in real-world video streams. The model can detect individuals wearing safety helmets and reflective jackets in video footage. Here’s a breakdown of how the video processing works:

1. **Input Video**: The script processes a video file where each frame is analyzed for person detection and safety equipment (helmet and jacket) detection.

2. **Detecting People**: The model uses YOLO to identify people in each frame of the video. Detected bounding boxes around people are saved for further analysis.

3. **Helmet and Jacket Detection**: For each detected person, the model checks if they are wearing a safety helmet and/or reflective jacket by cropping the person’s region of interest (ROI) and running the helmet/jacket YOLO model on it.

4. **Tracking People**: The script tracks the same individual across multiple frames, using intersection-over-union (IoU) to match the current detections to previous ones. Each person is assigned a unique ID, and the helmet/jacket status is stored in a queue for each individual.

5. **Detection Rules**: The model uses the **8/10 rule** to verify the consistency of detections. The idea behind the rule is that a single detection (such as detecting a helmet or jacket in one frame) is not enough to make a final decision about whether a person is consistently wearing a helmet or jacket. Instead, you look at the last 10 frames for each individual to decide whether the detection is consistent enough to change the status.

    8/10 Rule Concept:
   
    If a person is detected wearing a helmet (or jacket), the rule ensures that the status (e.g., "Helmet" or "Jacket") isn't changed immediately if there is a small      fluctuation in the detection. The detection must remain consistent over a majority of the last 10 frames before the title is changed. In other words, the title        is only flipped from "Helmet" to "No Helmet" or "Jacket" to "No Jacket" if at least 8 of the last 10 detections support that change.

7. **Handling Missing Detections**: If a person is not detected for more than three frames in a row, their tracking is deleted.

8. **Bounding Boxes and Labels**: Bounding boxes are drawn around detected individuals, with labels indicating whether they are wearing a helmet, jacket, both, or neither.

9. **Output Video**: The processed video with visualized detections is saved as an output video file.

# DEMO VIDEO:

https://github.com/user-attachments/assets/7cdef876-36b5-4f80-88de-2c82945547a5
