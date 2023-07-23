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
