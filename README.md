# Emotion-Recognition
---
　
#### 一、概述
```
本程式為使用python語法。使用 Python語言，辨識自己的困惑表情。集，並使用OpenCV函式庫。
```

#### 二、資料集：
```
自己拍照建檔(約500張，12位不同人)
```

#### 三、檔案概解
##### 1. main.py 
最先執行檔

##### 2. GUI.py
GUI刻板

##### 3. histogram_face.py
人臉辨識與情緒辨識程式碼

##### 3.1 人臉辨識與情緒辨識程式碼概解
人臉辨識(使用直方圖差異來判別)
```
 def verify_process(self):
        self.open_camera('Face Recognition', 'output')
        cv2.waitKey(1000)
        self.catch_face('output.jpg', 'output')
        distance = self.face_distance('origin0', 'output0')
        if (self.verify_face(distance)):
            GUI.popupmsg("驗證成功！")
        else:
            GUI.popupmsg("驗證失敗！")
        try:
            os.remove("output0.jpg")
        except:pass

 def face_distance(self, origin_name, after_name):
        h1 = Image.open(str(origin_name + '.jpg')).histogram()
        h2 = Image.open(str(after_name + '.jpg')).histogram()
        rms12 = math.sqrt(reduce(operator.add,map(lambda a, b: (a-b)**2, h1, h2))/len(h1))
        return rms12
```

情緒辨識主要程式碼
```
  def detect_confused_emotion(self):
        cv2.namedWindow("detect confused emotion")
        cap = cv2.VideoCapture(0)
        while (cap.isOpened()):
            ret, img = cap.read()
            gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
            confused = self.confused_cascade.detectMultiScale(gray, 1.1, minSize=(150, 150))
            for (x, y, w, h) in confused:
                cv2.rectangle(img, (x, y), (x + w, y + h), (255, 0, 0), 2)
                cv2.putText(img, "Confused :(", (x, y), cv2.FONT_HERSHEY_SIMPLEX, 1.5, 255)
            cv2.imshow("detect confused emotion", img)
            if ret == True:
                key = cv2.waitKey(50)
                if key == ord("q") or key == ord("Q"):
                    break
        cap.release()
        cv2.destroyAllWindows()
```







