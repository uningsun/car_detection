https://ai.stanford.edu/~jkrause/cars/car_dataset.html

### Tensorflow Yolov3용 train.txt, test.txt 파일 만들기
```python
import pandas as pd

def make_txt(csvpath) :
    if csvpath.split("/")[-1].startswith("train") :
        csvfile = pd.read_csv(csvpath)
        base_path = "./cars_train/"# train_img 존재 폴더 
        savename = "train.txt"
    elif csvpath.split("/")[-1].startswith("test") :
        csvfile = pd.read_csv(csvpath)
        base_path = "./cars_test/"# test_img 존재 폴더 
        savename = "test.txt"

    yolo_text=''
    for i in range(len(csvfile)) :
        img_path = base_path + csvfile.iloc[i]['fname']
        cls = csvfile.iloc[i]['class']
        xmin = csvfile.iloc[i]['bbox_x1']
        ymin = csvfile.iloc[i]['bbox_y1']
        xmax = csvfile.iloc[i]['bbox_x2']
        ymax = csvfile.iloc[i]['bbox_y2']
        yolo_text+="{0} {1} {2} {3} {4} {5}\n".format(img_path ,cls, xmin, ymin, xmax, ymax)
    
    with open(savename, "w") as yt :
        yt.writelines(yolo_text)
```
