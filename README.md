
### Detection of Unique Persons in CCTV Video Based on Facial Area


#### **1. Introduction**

This project focuses on identifying unique individuals captured in CCTV footage using facial recognition techniques. The primary goal is to detect and recognize each person in the video and assign them a unique ID based on facial characteristics. By doing so, we can track each individual throughout the video, even if they reappear in different frames.

#### **2. Objectives**

- To develop an end-to-end system capable of detecting faces in CCTV videos.
- To extract facial embeddings and compare them to identify unique individuals.
- To assign a unique ID to each detected person based on facial similarities.

#### **3. Methodology**

The project is divided into several key steps, each crucial for achieving the desired outcomes:

##### **3.1. Face Detection**

Initially, multiple face detection models were tested to identify the most effective one for this task. The models evaluated were:

- **dlib**
- **YOLOv3**
- **MTCNN**
- **YOLOv8n**

After comparing the performance of these models, **YOLOv8n** was selected due to its superior accuracy and speed in detecting faces within the video frames.

##### **3.2. Face Embedding Extraction**

The next step involved extracting face embeddings, which are unique numerical representations of the detected faces. These embeddings allow for comparing and recognizing faces throughout the video.

- **Initial Attempt**: The first approach involved using the Keras library to load the FaceNet weights for extracting the face embedding vector. However, this method proved unsuccessful due to various challenges and bugs.

- **Final Solution**: After researching alternative approaches, the **DeepFace** library was identified as a comprehensive tool for facial recognition tasks. This library supports various functions, including face embedding extraction using the FaceNet model, which is pre-trained on the LFW dataset.

  - **Embedding Process**:
    - The detected face areas are resized to a 160x160 patch.
    - The resized face patches are passed through the FaceNet model, which generates a 128-dimensional vector as the face embedding.

##### **3.3. Face Recognition and Identification**

Once the face embeddings are extracted, they are compared using the **cosine distance** metric. This distance measures the similarity between the embeddings:

- **Threshold Setting**: A threshold is established to determine whether two embeddings correspond to the same person. If the cosine distance between two embeddings is below this threshold, they are considered to represent the same person.

  The process is as follows:

  - **Initial Frame**: Detect faces and store their embeddings in a **FaceBank**.
  - **Subsequent Frames**:
    1. Compare the detected faces with those in the previous frame.
    2. If a match is found, no action is needed.
    3. If no match is found, compare the face with the embeddings in the FaceBank.
    4. If a match is found with the FaceBank, no action is needed.
    5. If no match is found, assign a new ID to the face and store its embedding in the FaceBank.

##### **3.4. Fine-Tuning and Optimization**

To improve the accuracy of the system, several strategies were proposed:

- **Threshold Adjustment**: The threshold for the cosine distance is crucial in balancing false positives and false negatives. Experiments were conducted with different threshold values to identify the optimal setting.
- **Saving Multiple Face Areas**: It is suggested to save multiple face images for each individual to enhance recognition accuracy.
- **Fine-Tuning the Detection Model**: Further fine-tuning of the YOLOv8n model could potentially improve detection accuracy.

#### **4. Experimental Results**

"In Vid1, there are 6 unique persons. Five of them were successfully detected, but one was not."

- **Vid1 Results**:
  - **Threshold = 0.15**: The model detected 29 unique persons.
  - **Threshold = 0.3**: The model detected 8 unique persons.

  The results indicate that a higher threshold value (0.3) provided better accuracy for this video, with fewer false positives.


#### **5. Challenges**

Throughout the project, several challenges were encountered:

- **Recognizing the Same Person as Different Individuals**: This issue was primarily caused by variations in facial expressions, lighting, and angles.
- **False Positives and False Negatives**: Incorrect identifications due to threshold settings and detection inaccuracies.

#### **6. Solutions and Future Work**

To address these challenges, the following solutions were proposed:

- **Proper Threshold Setting**: Tuning the threshold for cosine similarity checks is crucial for improving accuracy.
- **Saving Multiple Face Areas**: Storing multiple face images for each individual in the FaceBank can help in better recognition.
- **Model Fine-Tuning**: Fine-tuning the YOLOv8n detection model could enhance performance.



#### **7. Conclusion**

This project successfully developed a system to detect and recognize unique individuals in CCTV footage based on facial embeddings. While the system performed well in initial tests, further fine-tuning and optimization are necessary to achieve more reliable results. The code, along with all relevant resources such as notebooks and weights is available in the accompanying GitHub repository for further exploration and development.
