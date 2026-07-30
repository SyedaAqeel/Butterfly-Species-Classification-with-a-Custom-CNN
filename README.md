# Butterfly Species Classification with a Custom CNN

This project designs, trains, and evaluates a convolutional neural network that classifies butterfly images sourced from [iNaturalist](https://www.inaturalist.org) observations. Rather than predicting across the full long-tail of species in the dataset, the model targets the 9 most frequently observed species in the training set, with every other species collapsed into a 10th "other" class — a common strategy for handling extreme class imbalance in real-world biodiversity data.

## Course

DS 542 Deep Learning for Data Science - Boston University

## Model Architecture

The proposed ButterflyCNN is a custom residual convolutional neural network developed from scratch for fine-grained butterfly species classification. Unlike transfer learning approaches that rely on pretrained models, this architecture is specifically designed to learn discriminative visual features directly from the iNaturalist butterfly dataset. The network begins with a convolutional stem that extracts low-level features such as edges, colors, and textures, followed by five sequential residual stages. Each stage contains two residual blocks, with the number of feature channels progressively increasing from 64 to 512, while max-pooling layers reduce the spatial dimensions of the feature maps. This hierarchical design enables the network to capture increasingly complex characteristics, including wing patterns, venation, color distributions, and species-specific morphological details.

Each residual block consists of two 3×3 convolutional layers, Batch Normalization, ReLU activation, and identity shortcut connections. When the input and output channel dimensions differ, a 1×1 projection shortcut is used to align dimensions before feature addition. These residual connections improve gradient flow, alleviate the vanishing gradient problem, and facilitate the training of deeper networks. After the final residual stage, Global Average Pooling compresses the feature maps into a compact representation, which is passed to a fully connected layer that outputs probabilities for the 10 target classes. The model is trained using class-weighted CrossEntropyLoss with label smoothing to address class imbalance and improve prediction calibration.
