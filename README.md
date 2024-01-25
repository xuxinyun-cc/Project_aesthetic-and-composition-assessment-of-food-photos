# Project
### 題目 : 美食相片的美感與構圖分析

### 研究動機和目的 :
美食是我們日常生活中最基本的元素之一，評估食物圖像的視覺美感能力
在各種任務中起著重要作用，拍攝的構圖也影響了食物的美感。因此，我們計
劃將美食相片加以分類，且提供更深入的照片構圖學習，以辨識美食相片之構
圖。在這項研究中，我們使用了美食攝影數據集 Gourmet Photography Dataset
（GPD），這是第一個支持食物圖像美學視覺評估的數據集。此資料集對用於視
覺分析任務的流行學習機制進行了一系列實驗，以驗證 GPD 數據集的標註質
量。此外，還測試了優化模型在看不見實例上的泛化能力，以展示 GPD 的有效
性。在此資料集的實驗結果顯示，GPD 在調整模型以成為對食物美學重要視覺
模式的預測方面提供了實用的幫助，實現了有效的食物照片美學評估。

### 研究方法:
運用 VGG16 模型，以 ImageNet 大規模資料集為權重基礎，在 16 層的 VGG
訓練模型中，取出倒數第二層的 256 維的特徵，作為分類美食相片的模型學習特
徵，利用 SVM 實現對於美食相片的二分類，美(Positive)和不美(Negative)。利用
綜合性的分析方法捕捉圖像中的視覺特徵，提供對美學品質的評價。再利用攝影
構圖的規則分成九個類別，包含 RoT (Rule of Thirds)、center、horizontal、symmetric、
diagonal、curved、vertical、triangle、pattern，進一步對美食相片進行構圖分析。

![GITHUB](https://github.com/xuxinyun-cc/Project_beauty-and-composition-analysis-of-food-photos/blob/main/%E6%9E%B6%E6%A7%8B%E5%9C%96.png)
`研界方法之架構圖`

![GITHUB](https://github.com/xuxinyun-cc/Project_beauty-and-composition-analysis-of-food-photos/blob/main/%E4%B9%9D%E5%80%8B%E5%88%86%E9%A1%9E%E4%B9%8B%E7%AF%84%E4%BE%8B%E6%A7%8B%E5%9C%96.png)
`九個分類之範例構圖`

### 實驗:
使用食物圖像分類的數據集 Food-101，此數據集包含 101 種不同種類的食
物，每種食物包含約 1000 張高分辨率的圖像。這個數據集旨在提供一個用於訓
練和評估食物圖像識別算法的豐富而多樣的資源，概念是創建一個比 CIFAR10
或 MNIST 更刺激的簡單的訓練集，並且用於影像分析上。

![GITHUB](https://github.com/xuxinyun-cc/Project_beauty-and-composition-analysis-of-food-photos/blob/main/food101_percent.png)
`Food-101 訓練和測試資料集數量`

為了提升 GPD 的質量，而進行審核美學標籤，盡量排除錯誤、爭議性樣本。
具體而言，此資料集是請八名具有良好美學感知能力的專業攝影師觀察標註。對
於每組圖像標籤，他們可以選擇同意或不同意標註的標籤。如果超過四名專家同
意，則美學標籤將會被保留。最終，我們建立了 GPD，內部包含了食物圖像和相
應的美學標籤。

![GITHUB](https://github.com/xuxinyun-cc/Project_beauty-and-composition-analysis-of-food-photos/blob/main/gpd_percent.png)
`GPD 在分類上的訓練和測試資料集數量`

在這個專題中，選擇了 Python 為主要程式語言來實現我們的實驗，採用了
Tensorflow 和 Keras 的深度學習框架和機器學習的模型進行開發和訓練。運用
VGG16 模型，以 ImageNet 大規模資料集為權重基礎，將 Food-101 數據集放入
16 層的 VGG 模型中訓練，並取出倒數第二層 256 維的特徵，作為分類美食相片
的模型學習的特徵。在參數上，對於損失函數，選擇了用於多類別分類任務的損
失函數 categorical _ crossentropy，及目前廣泛被使用的優化演算法 adam 作為優
化器，以調整模型的權重使最小化損失函數，這些技術和工具使我們能夠進一步
的訓練模型。透過這個過程，將 GPD 放入上述的模型中加以訓練，進而再引入
了 SVM 支援向量機作為分類器，進行模型的調整與分類工作，並且比較 rbf kernel 
function、linear kernel function 和 polynomial kernel function 何者的 SVM 模型的
準確率較高。最終以 rbf kernel function 的 SVM 模型的準確率為最高，所以採用
了 rbf kernel function。

![GITHUB](https://github.com/xuxinyun-cc/Project_beauty-and-composition-analysis-of-food-photos/blob/main/svm_accuracy.png)
`不同的 kernel 參數在 SVM 上所實驗的結果`

基於幾何元素的排列方式，將攝影構圖的規則分成 9 個類別，包含 RoT (Rule 
of Thirds)、center、horizontal、symmetric、diagonal、curved、vertical、triangle、
pattern。藉由訓練 Convolutional neural network (CNN)，建立一個演算法，對每個
元素設計一個標準辨別各個分類，而提取出最佳的構圖元素，針對每個元素的提
取結果做量化和質化的評估。

使用 KU-PCP 資料集，此資料集是由 18 個人做人工分類後，將有超過一半
的有相同答案的視為 ground-truth，而每張照片最多可歸類於 3 種不同的分類。
因原始資料集針對每個分類的分布不平均，所以利用了
* 上下翻轉、左右翻轉、上下左右翻轉
* 放大、縮小
* 左右平移

以平衡各類的分佈。最終以 8080 張作為 training_data、2902 張作為 testing_data。
為了充分利用已有的影像特徵提取的性能，載入 VGG16 作為 pre-trained 
model，且去除模型頂部的全連接層，僅保留特徵提取的部分，以適應我們的任
務。在模型的最後一層則利用 soft-max 激活函數去計算各個分類的信心分數，選
擇信心分數中最高的為該影像的 ground-truth。對於損失函數，我選擇了用於多
類別分類任務的損失函數 categorical _ crossentropy，及優化演算法 adam 作為優
化器，以調整模型的權重使最小化損失函數。這些技術和工具使我們能夠進一步
的訓練模型，以應對我們的影像佈局偵測。
採用了 batch_size 為 64 和 epochs 為 10 的參數，而在 learning rate 的部分則
設定為 0.001，且從訓練資料拿取 20%作為驗證資料，再進一步的執行結果。
最終獲得的 loss = 0.99、F1_score = 0.75 的構圖偵測模型。進而將 GPD 放入
構圖偵測模型加以辨識，以觀察何種構圖的方法利於我們拍攝出更好的美食相片。

![GITHUB](https://github.com/xuxinyun-cc/Project_beauty-and-composition-analysis-of-food-photos/blob/main/gpd_composition_analysis.png)
`GPD 的構圖分析`

### 參考文獻:
J. T. Lee, H. U. Kim, C. Lee, C., & C. S. Kim, Photographic composition 
classification and dominant geometric element detection for outdoor scenes. Journal of 
Visual Communication and Image Representation, 55, pp. 91-105, 2018.

Sheng, K., Dong, W., Huang, H., Ma, C., & Hu, B. G. Gourmet photography 
dataset for aesthetic assessment of food images. In SIGGRAPH Asia 2018 technical 
briefs, pp. 1-4, 2018.


