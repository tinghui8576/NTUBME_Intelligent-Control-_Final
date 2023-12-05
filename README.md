# NTUBME Intelligent Control Final Project
## 應用CNN進行蘋果葉片病害之判斷 Developing a CNN Model For Apple Leaf Disease Detection 
### Outline
* [objective](#Objective)
* [Models](#Models)
* [Results](#Results)
* [Reference](#Reference)
### Objective
蘋果是常見且極具營養價值的水果，在種植過程中當病蟲害產生時，若未及時發現、用 藥，往往會降低影響蘋果產值，對於蘋果的產量與質量是個重要威脅，而這些為害症狀經常 出現在葉片上，傳統上，農民們會透過人工一片一片檢查蘋果葉面是否出現病害徵兆，然而， 這樣的過程耗時、花費過多勞力，且往往因不同農民具有不同的經驗，不夠精確，因此本期 末專題利用卷積神經網路(Convolutional Neural Network, CNN) 模型將葉片影像進行病害辨識。 由於卷積神經網路能夠利用卷積層(Convolution Layer) 進行影像特徵擷取，降低神經網路 (Neural Network, NN) 訓練的負擔，因此卷積神經網路最適合消化並處理影像[1]，故本專題 使用兩種卷積神經網路模型:預訓練模型 InceptionV3[2,3] 與自己建構之卷積模型，來解決此次問題。
### Method
#### Data
本次期末專題使用之蘋果葉片影像來自於 Kaggle 競賽 Plant Pathology 2021 - FGVC8，共有 17277 張具標籤(label) 之訓練影像，其中影像標籤有六種不同類型之疾病，分別為: Healthy(健康)、Scab(蘋果黑星病)、Powdery Mildew(白粉病)、Frogeye Leaf Spot(蛙眼葉斑病)、 Rust(銹病) 和 Complex(複雜) 。為增加模型的強健性(Robustness)，訓練影像將進行影像擴 增(Image Augmentation)，其中包括亮度、圖像轉換、圖像縮放、水平翻轉等等，並將 2672 x 4000 像素之影像縮放置 256 x256 像素，並隨機選取資料中的 70%數據作為訓練集，10%作 為驗證集，20%作為測試集 <br> <br>
Data distribution <br>
![image](/figure/Data.png) <br>
#### Models
本研究利用 InceptionV3 卷積神經網路架構以及自己建構之卷積模型以辨識葉片影像中的病害。卷積神經網路的優化器使用 Adam，初始學習率為 0.0001，批次大小為 128，損失 率則使用交叉熵損失函數(Category cross entropy)計算。 <br>
InceptionV3 架構如下圖，由於此模型預設 Input 大小為 229x229，因此在前端接一大小 為 256x256 的輸入層，接做批次標準化與 Dropout 再接至一大小為 1024 的隱藏層，其激勵函 數使用 Relu，再做一次 Dropout 並與最終的 Output Layer 做連結，其激勵函數使用 Softmax。 <br>

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
<br>
自建的模型則使用作業五的作為參考，共使用三層卷積層與池化層，卷積核大小皆為 3x3，而 Filter 分 別為 32、64 與 128，激勵函數皆使用 Relu，接著連接 至平坦層，再接至一層大小為 1024 的隱藏層，其激勵 函數使用 Relu，最終連結至 Output Layer，其激勵函數 亦為 Softmax。<br>

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
在本專題建立訓練之葉片病害辨識模型中，InceptionV3 的訓練準確率達 95.6%，驗證準 確率達 91.5%，測試準確率則為 71.9%，總訓練時長為 8376 秒。而自建卷積神經網路模型的 訓練準確率達 68.6%，驗證準確率達 67.2%，測試準確率則為 67.7%，總訓練時長為 14282 秒。<br>
預測結果中，InceptionV3 的準確度較自建模型的準確度高，推測是卷積層數差異，也許可以增加自建模型準確度，但並未做不同層數之比較，略為可惜。 <br>
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

