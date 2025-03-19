# Safety Helmet and Reflective Jacket Detection

This project focuses on training a YOLO11n model to detect safety helmets and reflective jackets worn by individuals. The goal is to accurately identify whether a person is wearing a safety helmet and/or a reflective jacket using computer vision techniques.

## Installation

To run this project, you'll need to install the necessary dependencies:

```bash
pip install ultralytics
pip install matplotlib
pip install opencv-python
```

## Dataset

The dataset used in this project contains images of individuals wearing safety helmets and reflective jackets. The dataset has been split into three parts:

- **Train**: Training images and labels
- **Validation**: Validation images and labels
- **Test**: Test images (used to evaluate the trained model)

You can access the dataset from Kaggle:
[Safety Helmet and Reflective Jacket Dataset]([https://www.kaggle.com/datasets/xxxxx](https://www.kaggle.com/datasets/niravnaik/safety-helmet-and-reflective-jacket))

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

These results show that the model performs well in detecting both helmets and jackets, with a high precision and recall.
