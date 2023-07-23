### **Google VM應用 - AI最經典應用之人臉偵測(Face Detection)實作** - 學習筆記

**Step 1:** 需要建立一個 Google Cloud Platform (GCP) 專案。可以在 GCP 控制台上執行此操作。

**Step 2:** 建立了專案，要啟用 Cloud Vision API。這可以在 GCP 控制台上的 API 和服務頁面上執行此操作。

**Step 3:** 啟用 Cloud Vision API 後，需要建立一個服務帳戶。在 GCP 控制台上的 IAM 和管理頁面上執行此操作。

**Step 4:** 建立服務帳戶後，要為服務帳戶新增權限。在 GCP 控制台上的 IAM 和管理頁面上的角色和專案頁面上執行此操作。

**Step 5:** 為服務帳戶新增權限後，你需要下載服務帳戶的金鑰。你可以在 GCP 控制台上的 IAM 和管理頁面上的金鑰頁面上執行此操作。

**Step 6:** 下載服務帳戶的金鑰後，要將金鑰新增到 Python 環境。使用 `pip` 套件管理器來執行此操作。

**Step 7:** 將金鑰新增到 Python 環境後，就可以開始使用 Cloud Vision API 來偵測圖片中的人臉。使用 `google.cloud.vision` 套件來執行此操作。

下面是使用 `google.cloud.vision` 套件來偵測圖片中的人臉的程式碼：

```python
import io
from google.cloud import vision

# 建立 Cloud Vision 客戶端
client = vision.ImageAnnotatorClient()

# 讀取圖片
with io.open('image.jpg', 'rb') as image_file:
  image = image_file.read()

# 執行人臉偵測
results = client.face_detection(image=image)

# 列印人臉的資訊
for face in results.face_annotations:
  print(face.bounding_poly)
  print(face.landmarks)
  print(face.emotions)
```

該程式碼將會列印圖片中每個人臉的座標、標記和表情。

以下是程式碼中各個部分的說明：

* `import io`：匯入 `io` 模組，以便可以讀取圖片。
* `from google.cloud import vision`：匯入 `google.cloud.vision` 模組，以便可以使用 Cloud Vision API。
* `client = vision.ImageAnnotatorClient()`：建立 Cloud Vision 客戶端。
* `with io.open('image.jpg', 'rb') as image_file: image = image_file.read()`：讀取圖片。
* `results = client.face_detection(image=image)`：執行人臉偵測。
* `for face in results.face_annotations: print(face.bounding_poly) print(face.landmarks) print(face.emotions)`：列印人臉的資訊。

**實作Github連結: ** https://github.com/jmfusa/ESVT2023/blob/main/Lab7.ipynb

###什麼是混淆矩陣（Confusion Matrix）?###

混淆矩陣是用於評估機器學習模型效能的一種方法，尤其是在監督式學習（Supervised Learning）中。當我們訓練一個分類器（Classifier）來預測不同的類別，混淆矩陣幫助了解模型的預測結果和真實結果之間的差異。

混淆矩陣是一個 2x2 的矩陣，通常包含以下四個元素：

1. **真陽性（True Positive, TP）：** 表示模型正確地將一個樣本預測為正類別（Positive Class）。

2. **偽陰性（False Negative, FN）：** 表示模型錯誤地將一個樣本預測為負類別（Negative Class），而實際上它屬於正類別。

3. **真陰性（True Negative, TN）：** 表示模型正確地將一個樣本預測為負類別。

4. **偽陽性（False Positive, FP）：** 表示模型錯誤地將一個樣本預測為正類別，而實際上它屬於負類別。

這些元素可以在以下的混淆矩陣中表示：

```
              預測為正類別   預測為負類別
實際為正類別    TP            FN
實際為負類別    FP            TN
```

在混淆矩陣中，對角線上的元素代表模型的正確預測，而非對角線上的元素代表模型的預測錯誤。

我們可以使用混淆矩陣來計算各種評估指標，例如：

1. **準確率（Accuracy）：** 計算模型預測的正確率，即 (TP + TN) / (TP + TN + FP + FN)。

2. **精確率（Precision）：** 衡量預測為正類別中有多少是真陽性，即 TP / (TP + FP)。

3. **召回率（Recall）：** 衡量實際為正類別中有多少被預測正確，即 TP / (TP + FN)。

4. **F1 分數（F1 Score）：** 綜合考慮精確率和召回率的評估指標，即 2 * (Precision * Recall) / (Precision + Recall)。

混淆矩陣和相關評估指標對於了解機器學習模型的預測表現非常重要。透過混淆矩陣，我們可以知道模型的預測中真實情況如何，並進一步優化和改進模型的表現。
