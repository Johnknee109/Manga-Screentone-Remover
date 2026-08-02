# Manga-Screentone-Remover

個人練習用漫畫網點去除專案。

本專案透過影像模糊處理降低漫畫網點造成的干擾，接著使用 Real-ESRGAN 進行影像修復與細節補強，最後利用 MangaLineExtraction_PyTorch 提取漫畫線稿，將線條細節重新融合至修復後影像中。

整體流程如下：

1. 使用 YOLO segmentation 模型偵測漫畫文字區域，避免文字受到影像處理影響
2. 對非文字區域進行模糊處理，以降低漫畫網點干擾
3. 使用 Real-ESRGAN 進行超解析與細節修復
4. 使用 MangaLineExtraction_PyTorch 提取漫畫線稿
5. 將影像轉換至 LAB 色彩空間，針對 L（亮度）通道調整，使黑色線條更加明顯


## Google Colab

點擊以下按鈕即可直接開啟 Google Colab 執行：

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Johnknee109/Manga-Screentone-Remover/blob/main/screentone_remover.ipynb)


---

# 使用方式

## 1. 設定 GPU 執行環境

開啟 Google Colab 後，請先將執行階段切換至 GPU。

GPU 可以大幅加速 YOLO segmentation、Real-ESRGAN 以及線稿提取模型的推理速度。


---

## 2. 上傳漫畫圖片

將需要處理的漫畫圖片壓縮成 `.zip` 檔案。

接著將 `.zip` 檔拖曳至 Google Colab 左側的檔案區域。

上傳後程式會自動搜尋 `/content` 底下的 zip 檔案並開始處理。


支援圖片格式：

- `.jpg`
- `.jpeg`
- `.png`
- `.webp`
- `.bmp`
- `.tif`
- `.tiff`


---

## 3. 執行程式

執行 Notebook 中所有程式碼。

程式流程：

1. 解壓縮漫畫圖片資料
2. 使用 YOLO segmentation 模型偵測漫畫文字區域
3. 藉由模糊消除網點
4. 使用 Real-ESRGAN 進行影像修復與細節補強
5. 使用 MangaLineExtraction_PyTorch 提取漫畫線稿資訊
6. 將修復後影像轉換至 LAB 色彩空間
7. 利用線稿資訊調整 L（亮度）通道，使黑色線條更加深邃，同時維持原始色彩資訊
8. 輸出最終修復結果


---

## 4. 下載結果

程式執行完成後：

到 Google Colab 左側檔案區：

下載 `/results` 底下的 zip 檔案。

解壓縮後即可取得處理完成的漫畫圖片。


---

# 未來改進方向

目前方法主要透過模糊處理移除漫畫網點，但過程中可能造成部分線條與細節損失。

未來預計：

- 爆調參數
- 修復部分路徑問題
- 加入自適應參數調整，使不同漫畫風格能取得更佳效果


---

# Acknowledgement

本專案使用與參考以下開源作品，特別感謝作者提供優秀的模型、工具與方法。


---

## Real-ESRGAN

https://github.com/xinntao/Real-ESRGAN

本專案使用 Real-ESRGAN 進行影像超解析與細節修復，改善移除 screentone 後可能造成的細節損失。


---

## Manga109 Panel, Text, and Balloon Segmentation

https://huggingface.co/ShadowB/Manga109-panel-balloon-text-yolov26-segmentation

本專案使用 ShadowB 提供的 YOLO26s 漫畫分割模型。

該模型可分割：

- Panels / Frames
- Text regions
- Speech or narration balloons

本專案主要使用 Text Region segmentation 功能，用於保護文字區域，避免文字受到模糊處理影響。


---

## Screentone Removal Method

https://github.com/natethegreate/Screentone-Remover

本專案的 screentone 移除方法參考 natethegreate 提供的實作與方法。

感謝 natethegreate 開源漫畫網點移除方法，作為本專案影像處理流程的重要參考。


---

## MangaLineExtraction_PyTorch

[https://github.com/CarloLepelaars/MangaLineExtraction_PyTorch](https://github.com/ljsabc/MangaLineExtraction_PyTorch)

本專案使用 MangaLineExtraction_PyTorch 進行漫畫線稿提取。

透過模型取得漫畫線條資訊，並將其作為後處理階段的細節補強資訊，使 Real-ESRGAN 修復後可能減弱的黑色線條重新強化。
