# Manga-Screentone-Remover

個人練習用，藉由模糊圖片來消除漫畫網點，接著使用 Real-ESRGAN 進行影像修復。

## Google Colab

點擊以下按鈕即可直接開啟 Google Colab 執行：

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Johnknee109/Manga-Screentone-Remover/blob/main/screentone_remover.ipynb)


---

# 使用方式

## 1. 設定 GPU 執行環境

開啟 Google Colab 後，請先將執行階段切換至 GPU：

GPU 可以大幅加速 YOLO 分割以及 Real-ESRGAN 推理速度。


---

## 2. 上傳漫畫圖片

將需要處理的漫畫圖片壓縮成 `.zip` 檔案。

接著將 `.zip` 檔拖曳至 Google Colab 左側的檔案區域。

上傳後檔案會位於：
程式會自動搜尋 `/content` 底下的 zip 檔案並開始處理。


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

1. 解壓縮圖片資料
2. 使用 YOLO segmentation 模型偵測漫畫文字區域
3. 對非文字區域進行模糊處理以消除網點
4. 使用 Real-ESRGAN 進行影像修復與細節補強
5. 將結果重新壓縮


---

## 4. 下載結果

程式執行完成後：

到 Google Colab 左側檔案區：
下載 `/results` 底下的 zip 檔案並下載。

解壓縮後即可取得處理完成的漫畫圖片。

---

# 未來改進方向

目前方法主要透過模糊來消除網點，但可能造成線條與細節消失

未來預計加入漫畫線稿提取模型，補上消失的線條與細節

---

# Acknowledgement

本專案使用與參考以下開源作品，特別感謝作者提供優秀的模型、工具與方法。

---

## Real-ESRGAN

https://github.com/xinntao/Real-ESRGAN

本專案使用 Real-ESRGAN 進行影像修復與細節補強，改善移除 screentone 後可能造成的細節損失。


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



