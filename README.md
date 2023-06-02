# NTUBME Intelligent Control Final Project
## 應用CNN進行蘋果葉片病害之判斷 Developing a CNN Model For Apple Leaf Disease Detection 
### Outline
* [objective](#Objective)
* [Models](#Models)
* [Results](#Results)
* [Reference](#Reference)
### Objective
Data distribution <br>
![image](/figure/Data.png) <br>
### Models

[InceptionV3](蘋果葉片辨識＿Inception.ipynb) <br>
Model structure <br>
![image](/figure/incept_model.jpeg) <br>
Hyperparameters <br>
|  | value |
| --- | --- |
| Optimizer	| Adam |
| initial learning rate | 0.0001 |
| epochs	| 6 |
| batch_size	| 128 |

[Self-Built Model](蘋果葉片辨識＿self.ipynb) <br>
Model structure <br>
![image](/figure/self_model.png) <br>
Hyperparameters <br>
|  | value |
| --- | --- |
| Optimizer	| Adam |
| initial learning rate | 0.0001 |
| epochs	| 20 |
| batch_size	| 128 |
### Results
* InceptionV3
Training history <br>
![image](/figure/Incept_curve.png) <br>
Confusion Metrics <br>
![image](/figure/Incept_CM.png) <br>
Prediction <br>
![image](/figure/Incept_Predict.png) <br>
* Self-Buit Model
Training history <br>
![image](/figure/self_curve.png) <br>
Confusion Metrics <br>
![image](/figure/self_CM.png) <br>
Prediction <br>
![image](/figure/self_predict.png) <br>
### Reference
Dataset: https://www.kaggle.com/competitions/plant-pathology-2021-fgvc8/

