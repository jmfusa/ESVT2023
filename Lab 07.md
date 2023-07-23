好的，以下是網頁中列出的步驟的詳細說明：

1. 在 Google Cloud 上建立一個專案。

要建立一個專案，您需要前往 Google Cloud Console，然後點擊 **建立專案**。您需要提供專案名稱和描述。

2. 啟用 Cloud Vision API。

要啟用 Cloud Vision API，您需要前往 Google Cloud Console，然後點擊 **API 和服務**。然後，點擊 **啟用 API**，並搜索 **Cloud Vision**。點擊 **啟用**。

3. 上傳一張包含人臉的圖片。

您可以使用 Google Cloud Console 或命令列上傳圖片。要使用 Google Cloud Console 上傳圖片，您需要前往 Google Cloud Console，然後點擊 **儲存帳戶**。然後，點擊 **上傳檔案**。您需要選擇包含人臉的圖片。

要使用命令列上傳圖片，您可以使用 `gsutil cp` 命令。例如，要將名為 `image.jpg` 的圖片上傳到名為 `my-bucket` 的儲存桶，您可以使用以下命令：

```
gsutil cp image.jpg gs://my-bucket
```

4. 使用 Cloud Vision API 來偵測圖片中的人臉。

要使用 Cloud Vision API 來偵測圖片中的人臉，您需要使用 Cloud Vision API 的 HTTP 要求。您可以使用 Google Cloud Console 或命令列來建立 HTTP 要求。

要使用 Google Cloud Console 建立 HTTP 要求，您需要前往 Google Cloud Console，然後點擊 **API 和服務**。然後，點擊 **Cloud Vision API**。然後，點擊 **要求**。您需要提供圖片的 URL 和您要偵測的資訊類型。

要使用命令列建立 HTTP 要求，您可以使用 `curl` 命令。例如，要偵測圖片 `image.jpg` 中的人臉，您可以使用以下命令：

```
curl -X POST \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "requests": [
      {
        "image": {
          "content": "data:image/jpeg;base64,<base64-encoded-image>"
        },
        "features": [
          {
            "type": "FACE_DETECTION"
          }
        ]
      }
    ]
  }' \
  "https://vision.googleapis.com/v1/images:annotate"
```

5. 使用人臉的座標、大小和旋轉角度來裁剪圖片。

您可以使用 Cloud Vision API 回傳的人臉的座標、大小和旋轉角度來裁剪圖片。要裁剪圖片，您可以使用 `ImageMagick` 或 `PIL`。

要使用 `ImageMagick` 裁剪圖片，您可以使用 `crop` 命令。例如，要裁剪名為 `image.jpg` 的圖片，並只保留人臉，您可以使用以下命令：

```
convert image.jpg -crop 100x100+100+100 cropped-image.jpg
```

要使用 `PIL` 裁剪圖片，您可以使用 `Image.crop()` 方法。例如，要裁剪名為 `image.jpg` 的圖片，並只保留人臉，您可以使用以下程式碼：

```
from PIL import Image

image = Image.open('image.jpg')
face = image.crop((100, 100, 200, 200))
face.save('cropped-image.jpg')
```
