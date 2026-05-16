# TUMTraf-I Background-Assisted Detection Extension

This repository provides the **modified label files** and **frame indices** used in our research on background-assisted 3D object detection for stationary roadside LiDAR systems. This extension is designed to be used in conjunction with the official [TUMTraf Intersection Dataset (TUMTraf-I)](https://innovation-mobility.com/en/project-providentia/tumtraf-dataset/).

## 1. Overview
Our research proposes a modular background-assistance framework that integrates environmental spatial priors into deep learning models to enhance 3D detection performance, particularly for small or heavily occluded objects. The original TUMTraf-I dataset provides annotations in the OpenLABEL format, which utilizes a complex, nested JSON structure. 

To ensure full reproducibility and improve compatibility with modern 3D object detection frameworks, we converted all 3D bounding box annotations into the standard **KITTI format** (individual `.txt` files containing normalized bounding box parameters). This extension allows the data to be loaded directly into popular training pipelines without requiring additional pre-processing scripts.

## 2. Class Conversion Mechanism (Taxonomy Merging)
Due to the extreme class imbalance inherent in real-world traffic scenarios within the TUMTraf-I dataset (e.g., the number of standard `Car` instances vastly overwhelms minority classes like `Trailer` or `Emergency Vehicle`), training the network on the original 10 independent classes often leads to severe convergence instability and overfitting.

To address this, we implemented a pragmatic mapping mechanism that concentrates the original 10 categories into **3 functional super-classes** to ensure training stability:

* **Car** (Four-wheeled motor vehicles): Merges `Car`, `Van`, `Trailer`, `Truck`, `Bus`, and `Emergency Vehicle`. The substantial intra-class geometric scale variations within this super-class are effectively accommodated by the network via K-means clustering for anchor box generation during training.
* **Wheeler** (Two-wheeled vehicles): Merges `Cyclist` and `Motorcycle`.
* **Pedestrian**: Retained directly from the original `Pedestrian` class.

## 3. Repository Structure
```text
.
├── ImageSet
│   ├── new_train.txt       # Modified train frame IDs
│   ├── new_val.txt         # Modified validation frame IDs
│   ├── original_train.txt  # Official TUMTraf-I train frame IDs
│   └── original_val.txt    # Official TUMTraf-I validation frame IDs
├── labels
│   ├── modified            # Converted KITTI labels (3 classes)
│   └── original            # Converted KITTI labels (Original classes)
└── LICENSE
```

## 4. Acknowledgments
We sincerely thank the creators of the official [TUMTraf Intersection Dataset](https://innovation-mobility.com/en/project-providentia/tumtraf-dataset/) for providing the raw data. 

