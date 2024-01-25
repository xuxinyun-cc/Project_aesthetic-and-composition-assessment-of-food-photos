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
