# Sign Language Recognition
Sign language is an essential communication tool for people with hearing impairment or deaf-mutes. However, only minority with hearing and speaking abilities understands and can communicate using sign language. In this study, by utilizing MediaPipe Holistic Landmarker and deep learning, two different methods were developed for sign language recognition. 
Method 1: Uses keypoints of 3D-landmark.
Method 2: Uses video frame sequence with spatio-temporal information.
For each method, two deep learning models were developed by using Convolution Neural Network (CNN) and Recurrent Neural Network (RNN) and compared.

### Challenges
- Mediapipe Landmarker failed to track the hand landmarks in part of the videos. Therefore, the distance values were normalized with respect to the signer’s shoulder width which is always present throughout the video.

- Another challenge faced when applying method 2 on WLASL dataset is that the distances between the signers and camera varies. This issue was mitigated by cropping the video frames with bounding box to focus on the signer.

- As some videos were no longer available from the source, the reduction in data size causes some words having more than one sign due to dialect variation. To alleviate the effect, each word was limit to one sign and data augmentation was performed on the training set including rotation, horizontal flip, vertical flip, cropping and the combination of these techniques.

- Most of the videos have a different resolution and video length. When applying method 2, to deal with this issue, 6 frames with 8 frame steps apart were extracted from each video in the WLASL dataset whereas 8 frames with 12 frame stpes apart were extracted from each video in the LSA64 dataset. The resolution of all videos was remain constant.

### Tools used
[MediaPipe Holistic](https://github.com/google/mediapipe/blob/master/docs/solutions/holistic.md) and [computer vision technique](https://opencv.org/) were utilized in this project. 

![image](https://github.com/suetteh/SignLanguageRecognition/assets/65590665/0f90dfa5-eae6-45d6-bd2e-ea6f627a5fd5)

MediaPipe Pose Landmarker (MediaPipe, 2023)

![image](https://github.com/suetteh/SignLanguageRecognition/assets/65590665/2fba4b32-8fda-4579-9077-8636f2068b1a)

Mediapipe Hand landmarker model bundle detects keypoint localization (MediaPipe, 2023)


library: mediapipe, cv2, numpy, matplotlib, pandas, keras, tensorflow, os, shutil, random, imageio.

### Data Source
Two secondary datasets: LSA64 and WLASL.
[LSA64](https://facundoq.github.io/datasets/lsa64/), an Argentinian Sign Language dataset is the published work of Ronchetti et al. (2016). Rochetti team recorded 3200 videos which covers 64 different words. The sign was demonstrated by 10 non-expert subjects (Ronchetti et al., 2016).

WLASL (Word-Level American Sign Language) (Li et al., 2020) is an American Sign Langauge dataset, which contains 2000 words performed by more than 100 signers. It is the largest video dataset for Word-Level  American Sign Language recognition. This database was built by the researchers of Li et al. (2020) by resorting two main sources which are the educational sign language websites and YouTube. 

### Data preprocessing
Method 1: 
- All videos were applied with MediaPipe Holistic Landmarker before data splitting. Only pose (33 pose landmarks with x, y, z coordinates) and hand landmarkers (21 landmarks per hand with x, y, z coordinates) were applied. The coordinates were normalized to the frame size.
- To further enhance the characteristics of each sign, additional 21 key points were added for each hand which representing the distance between thumb to each fingertip, wrist to each fingertip, between fingertips, within the joints of fingers (to detect bending), and distance from each fingertip to thumb joint. These values were then normalized to the shoulder distance (landmark 11 and 12).
- As a result, total of 267 key points were extracted.

Method 2: 
- Frames were cropped with respective bounding box to focus on the signer. The purpose of doing so is to keep the distance between the signer and camera consistent for all videos.
- WLASL dataset: 6 frames were extracted from all videos with 8 frame steps apart.
      ![image](https://github.com/suetteh/SignLanguageRecognition/assets/65590665/4da9139f-f3f4-4abc-9929-ab8ab8da1b70)

- LSA64 dataset: 8 frames were extracted from all videos with 12 frame steps apart.
   	 	 	 
 	 	 	 ![image](https://github.com/suetteh/SignLanguageRecognition/assets/65590665/c8677488-a89c-4009-89ec-1cb06976bbf4)


- Resolution of all videos was 100*100 for model 1 whereas 80*80 for model 2.


### Data analytics.



### Conclusion


