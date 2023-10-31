# AI-report1

# Training neural networks using Google Colab - 使用Google Colab訓練神經網路
•南華大學人工智慧課程期中報告   
•11124233黃文龍 11124230葉承諺 11125005林啟陽

## 目錄   
•代碼  
•準備資料   
•實作方法   

## 代碼
研究者取得乳房腫塊的細針穿刺（FNA），然後產生數位影像。 此資料集包含描述影像中細胞核特徵的實例。 每個實例包括診斷結果：M（惡性）或 B（良性）。 我們的任務是在該數據上訓練神經網路根據上述特徵診斷乳癌。

## 準備資料   
•一隻Google Colab帳號   
•下載資料集data

## 實作方法   
### 1、下載數據   
•首先將資料集放置到該機器上，這樣我們的 notebook 就可以存取它。 你可以使用以下程式碼：
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/1-1.png)  
結果:  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/1-2.png)  
•另存為breast_cancer.csv:  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/1-3.png)  
用!ls查看结果如下：  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/1-4.png) 

### 2、資料預處理  
•現在資料已經在機器上了，我們使用 pandas 將其輸入到專案中。  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/2-1.png)  
查看一下前五行:
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/2-2.png)  
•現在，分割因變數（Dependent Variables）和自變數（Independent Variables）  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/2-3.png)  
Y 包含一列，其中的「M」和「B」分別代表「是」（惡性）和「否」（良性）。 我們需要將其編碼成數學形式，即“1”和“0”。 可以使用 Label Encoder 類別來完成此任務。  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/2-4.png)  
（如果資料類別多於兩類，則使用 OneHotEncoder）  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/2-5.png)  
查看一下Y  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/2-6.png)  
•現在資料已經準備好，我們將其分割成訓練集和測試集。 在 Scikit-Learn 中使用 train_test_split 可以輕鬆完成這項工作。  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/2-7.png) 
參數 test_size = 0.2 定義測試集比例。 這裡，我們將訓練集設定為資料集的 80%，測試集佔資料集的 20%。  
### 3.建構神經網絡  
3.1 Keras  
Keras 是一種建構人工神經網路的高階 API。 它使用 TensorFlow 或 Theano 後端執行內部運作。 要安裝 Keras，必須先安裝 TensorFlow。 CoLaboratory 已經在虛擬機器上安裝了 TensorFlow。 使用以下命令可以檢查是否安裝 TensorFlow：  
![image]()  

•將辨識的結果印在圖片中車牌的旁邊. 
![image](https://img2018.cnblogs.com/blog/1365470/201903/1365470-20190305182238699-1637109185.png) 
![image]()  
※須注意圖片路徑要更改  
### 參考資料
https://www.cnblogs.com/lfri/p/10478603.html
