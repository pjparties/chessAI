# Chess AI with Computer Vision

- #### Chessboard Annotation Project with features for move tracking.
![image](https://i.imgur.com/uIS52Rj.jpg)

## Table of Contents

- [Chess AI with Computer Vision](#chess-ai-with-computer-vision)
  - [Table of Contents](#table-of-contents)
  - [1. Project Overview](#1-project-overview)
  - [2. Data Collection](#2-data-collection)
  - [3. Pre-Processing](#3-pre-processing)
  - [4. Approaches](#4-approaches)
    - [First Approach: CV Heuristic Functions](#first-approach-cv-heuristic-functions)
    - [Second Approach: CNN and YOLO for Chessboard Recognition](#second-approach-cnn-and-yolo-for-chessboard-recognition)
    - [Perspective Transform 3d to 2d projection using Perspective transfromation](#perspective-transform-3d-to-2d-projection-using-perspective-transfromation)
    - [Neural Network Training for Chess Piece Recognition](#neural-network-training-for-chess-piece-recognition)
  - [5. Integration and Enhancements](#5-integration-and-enhancements)
  - [6. Future Enhancements](#6-future-enhancements)
  - [7. References and Credits.](#7-references-and-credits)
  - [8. Contributing](#8-contributing)
  - [9. License](#9-license)


## 1. Project Overview

- **Identifying the Gap**: I initiated this project by recognizing a significant gap in the accuracy of annotating chess games during tournaments and over-the-board practice sessions.
- All the annotations have to be done via a DGT board which feeds the move via Bluetooth or USB and this board costs upwards of 1000 USD.
- Other ways to track games at a tournament require manual input of moves and this becomes harder when the time is low.
- The main objective of this algorithm should be to optimize precision and process the change in the image/feed source within 1 second of input delay which is not hard given YOLO models and other inference models work way faster than multi-layered deep CNNs like Resnet and Inception v3.
- This observation was the driving force behind the entire project.

- **Literature Review**: To gain a solid foundation, I began with an extensive literature review. This step involved delving into research papers related to computer vision, chess game analysis, and deep learning techniques. The purpose was to understand the state of the art and gather insights for my project.

## 2. Data Collection
- ### Two types of data were required. One being the chess pieces, other being the chessboards.
- given, how this data can be found on live games played on youtube videos, the combined data was not hard to source.
- But, running into low accuracy in training, we had to split the model into two parts. One to train chessboard detection, other for chesspieces detection and then annotating the pieces on the respective squares.
- Then I annotated all the raw data manually and made augmentations and Preprocessing.

## 3. Pre-Processing
- The following Preprocessing gave the best results:
  - Greyscale
  - Fit images within 1024x1024
  - Auto-Orienting Bounding Box
- The following Augmentations landed in best accuracy:
  - Noise addition
  - Rotate horizontally within the bounding box
  - Contrast range of +-20%
  - Rotation of +-15%

## 4. Approaches

### First Approach: CV Heuristic Functions

- For my initial approach, Issues related to handling various angles and achieving high confidence in board recognition prompted me to explore this approach. I decided to implement computer vision (CV) heuristic functions like Shi-Tomasi corner detection, Canny edge detection, and Hough lines transformation to recognize the chessboard layout. But this lead to overlapping lines and points which were harder to predict and eliminate using even DBSCAN functions.

![image](https://i.imgur.com/290LJvE.png)
![image](https://i.imgur.com/SUukeZe.png)

### Second Approach: CNN and YOLO for Chessboard Recognition

-  As I progressed, I encountered some challenges with the initial approach, I opted to leverage Convolutional Neural Networks (CNNs) and embarked on training a YOLO (You Only Look Once) deep learning model that works on Pytorch. This model's goal was to accurately detect the chessboard. This foundational step was crucial to establish a reliable starting point for game annotation.

### Perspective Transform 3d to 2d projection using Perspective transfromation
- This was a hard step and required a lot of math for it to correctly work. The linear algebra and Matrices part of it is kinda shaky and I'm trying to optimize how to perspective transform the image natively within Python.

### Neural Network Training for Chess Piece Recognition

- Recognizing the need for a more comprehensive solution, after training the chessboard recognition and perspective transforming it into 2d plane. I developed a neural network capable of recognizing individual chess pieces and accurately allocating their positions on the chessboard. To expedite the training process, I utilized transfer learning and incorporated pre-trained models.

## 5. Integration and Enhancements

- **Integration of FEN Notation**: To make the annotated games more accessible and compatible with popular chess engines like Stockfish, I integrated the Forsyth-Edwards Notation (FEN) system. This notation system allowed for a standardized representation of the chessboard and piece positions, simplifying the analysis and display of games.

- **Hyperparameter Tuning**: To optimize the neural network models, I engaged in rigorous hyperparameter tuning. This process included adjusting learning rates, and batch sizes, and fine-tuning network architectures to achieve the best possible results for both chess piece recognition and board layout detection.

- **Testing and Validation**: Rigorous testing and validation were essential to ensure the reliability of the developed models. I divided the dataset into training, validation, and testing sets to thoroughly assess model performance and mitigate overfitting.

- **Documentation and Open Source**: In the spirit of open-source development, I meticulously documented the project and released it as an open-source tool. This step aimed to make the project accessible to chess enthusiasts, developers, and researchers, encouraging contributions and improvements.


## 6. Future Enhancements
- **Real-time Annotation**: Recognizing the importance of real-time annotation during over-the-board chess games, I developed a feature that allowed the system to annotate games as they unfolded. This real-time capability provided immediate feedback to players and spectators, enhancing the overall chess experience.

- **Auto Learning** The model accuracy is not yet up to the mark for the dataset to be successfully implemented in real life. The perspective transform of images captured at an angle produces a challenge in correctly annotating pieces as well as assuming pieces due to previous experience and memory like a human can.
---

## 7. References and Credits.
- [Czyzewski, M. A., Laskowski, A., & Wasik, S. (2017). Chessboard and chess piece recognition with the support of neural networks. ArXiv. /abs/1708.03898](https://arxiv.org/abs/1708.03898)
- [Chessboard Vision Roboflow](https://github.com/shainisan/real-life-chess-vision?ref=blog.roboflow.com)
- [A Computer Vision System for Chess Game Tracking by Can Koray et al. ](https://vision.fe.uni-lj.si/cvww2016/proceedings/papers/21.pdf)
- [Determining Chess Game State From an Image - Georg Wölflein & Ognjen Arandjelovi´c](https://arxiv.org/pdf/2104.14963.pdf)




---
## 8. Contributing

We welcome contributions from the open-source community. If you'd like to contribute to the development of Chess AI, please follow our [Contribution Guidelines](CONTRIBUTING.md).

---
## 9. License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

Thank you for using Chess AI with Computer Vision! Enjoy your games and improve your chess skills with this exciting blend of tradition and technology. If you have any questions or encounter any issues, feel free to [create an issue](https://github.com/yourusername/chess-ai/issues) on our GitHub repository.

Happy playing!

![Chess AI Logo](images/chess_ai_logo.png)
