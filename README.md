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
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/1-1.png)  
結果:  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/1-2.png)  
•另存為breast_cancer.csv:  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/1-3.png)  
用!ls查看结果如下：  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/1-4.png) 

### 2、資料預處理  
•現在資料已經在機器上了，我們使用 pandas 將其輸入到專案中。  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/2-1.png)   
查看一下前五行:  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/2-2.png)  
•現在，分割因變數（Dependent Variables）和自變數（Independent Variables）  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/2-3.png)  
Y 包含一列，其中的「M」和「B」分別代表「是」（惡性）和「否」（良性）。 我們需要將其編碼成數學形式，即“1”和“0”。 可以使用 Label Encoder 類別來完成此任務。  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/2-4.png)  
（如果資料類別多於兩類，則使用 OneHotEncoder）  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/2-5.png)  
查看一下Y  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/2-6.png)  
•現在資料已經準備好，我們將其分割成訓練集和測試集。 在 Scikit-Learn 中使用 train_test_split 可以輕鬆完成這項工作。  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/2-7.png)  
參數 test_size = 0.2 定義測試集比例。 這裡，我們將訓練集設定為資料集的 80%，測試集佔資料集的 20%。  

### 3、建構神經網絡  
3.1 Keras  
•安装 Keras：  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/3-1.png)  

3.2  然後導入Keras庫和套件  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/3-2.png)  
•使用 Sequential 和 Dense 類別指定神經網路的節點、連接和規格。 如上所示，我們將使用這些自訂網路的參數並進行調整。  

3.3 初始化神經網絡  
•為了初始化神經網絡，我們將建立一個 Sequential 類別的物件。  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/3-3.png)  

3.4 設計神經網絡  
•對於每個隱藏層，我們需要定義三個基本參數：units、kernel_initializer 和 activation。 units 參數定義每層包含的神經元數量。 Kernel_initializer 定義神經元在輸入資料上執行時的初始權重。 activation 定義資料的激活函數。  
•輸入層與第一個隱藏層：16 個具備統一初始權重的神經元，活化函數為 ReLU。 此外，定義參數 input_dim = 30 作為輸入層的規格。 注意我們的資料集中有 30 個特徵列。 註：如何決定第一個隱藏層的節點數，對於初學者來說，一個簡單方式是：x 和 y 的總和除以 2。 如 (30+1)/2 = 15.5 ~ 16，因此，units = 16.  
•第二層：第二層和第一層一樣，不過第二層沒有 input_dim 參數.  
•由於我們的輸出是 0 或 1，因此我們可以使用具備統一初始權重的單一單元。 但是，這裡我們使用 sigmoid 來啟動函數。  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/3-4.png)  

3.5 編譯  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/3-5.png)  

3.6 擬合  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/3-6.png)  
•運行人工神經網絡，發生反向傳播。 你將在 CoLaboratory 上看到所有處理過程，而不是在自己的電腦上。  
這裡 batch_size 是你希望同時處理的輸入量。 epoch 指數據通過神經網路一次的整個週期。 它們在 Colaboratory Notebook 中顯示如下：  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/3-7.png)  

3.7 進行預測，建構混淆矩陣  
•訓練網路後，就可以在 X_test set 上進行預測，以檢查模型在新資料上的效能。 在代碼單元中輸入和執行 cm 查看結果。  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/3-8.png)  

•混淆矩陣  
混淆矩陣是模型做出的正確、錯誤預測的矩陣表徵。 此矩陣可供個人調查哪些預測和另一種預測混淆。 這是一個 2×2 的混淆矩陣。  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/3-9.png)  

混淆矩陣如下所示[cm (Ctrl+Enter)]  
![image](https://raw.githubusercontent.com/Lanco332/AI-report1/main/png/3-10.png)  

•上圖表示：1 個真負類、67 個假正類、0 個假負類、46 個真正類。 很簡單。 此平方矩陣的大小隨著分類類別的增加而增加。  
這個範例中的準確率達到 100%，只有 0 個錯誤預測。 但並不總是這樣。 有時我們可能需要投入更多時間，研究模型的行為，提出更好、更複雜的解決方案。 如果一個網路效能不夠好，則需要調整超參數來改進模型。  



### 參考資料
網頁  
https://www.cnblogs.com/lfri/p/10478603.html  
資料集data  
https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic

