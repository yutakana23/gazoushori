# ディジタル信号処理と画像処理
  
プログラム  
```python
%matplotlib nbagg
import numpy as np
import cv2
import matplotlib.pyplot as plt



y = [0] * 500
i = 0

cam = cv2.VideoCapture(0)
while True:
    _, img = cam.read()
    y[i] = img.mean()
    i += 1

    cv2.imshow('PUSH ENTER KEY', img)
    if cv2.waitKey(1) == 13: break

cam.release()
cv2.destroyAllWindows()

ave_y = sum(y[20: i-20]) / len(y[20:i-20])
x = np.linspace(0, 500, 500)
plt.plot(x, y)
plt.xlabel("times")
plt.ylabel("mean of image")
plt.xlim([10, i-10])
plt.ylim([ave_y-5, ave_y +5])
plt.title("Finger blood flow")
plt.savefig('Finger.pdf')
plt.show()
```  

実行環境
  - python 3.7.3
  - Opencv 3.4.2
  - Xcode 10.1
  
実行方法
  - cv2.VideoCapture(0)において，０はカメラ番号．パソコンのカメラを起動させて，取得を開始する．
  - cam.read()で画像の読み込み．Enterボタンを押すことで画像を取得する．
  - cv2.imshow('PUSH ENTER KEY', img)で画像を出力．
  - cam.release()でキャプチャを終了．
  - cv2.destroyAllWindows()でウィンドを閉じる．
  
ライブラリ
  - matplotlib：グラフの表示をするため．
  - numpy:array型変数の格納のため．
  - cv2:Opencvの利用のため．
  
参考にしたサイトのURL
  - 「OpenCV-画像の統計量を計算する」http://pynote.hatenablog.com/entry/opencv-image-statics
  - 「OpenCVによるUSBカメラ画像の取得」https://qiita.com/vs4sh/items/4a9ce178f1b2fd26ea30
  - 「OpenCVで動画を扱う」https://code-graffiti.com/connect-with-webcam-using-opencv-in-python/
