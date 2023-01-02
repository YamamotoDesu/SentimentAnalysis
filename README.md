# SentimentAnalysis

<img width="300" alt="スクリーンショット 2023-01-02 15 27 04" src="https://user-images.githubusercontent.com/47273077/210200305-d39e382f-0dc1-4124-9597-057f4ded6390.gif">

<img width="787" alt="epinions3_csv" src="https://user-images.githubusercontent.com/47273077/210200178-f402c1ed-a999-486a-b137-a518d1d2a74f.png">
<img width="545" alt="positive" src="https://user-images.githubusercontent.com/47273077/210200206-73ec12bd-998c-4f3e-9120-2ebc6fdfc77b.png">

```py

import os 
import shutil
import pandas as pd 

input_classes_filename = "/Users/yamamotokyou/Desktop/ESC-50-master/meta/esc50.csv"
sounds_directory = "/Users/yamamotokyou/Desktop/ESC-50-master/audio/"
output_directory = "/Users/yamamotokyou/Desktop/ESC-50-master/classes/"

classes_to_include = ["dog","rooster","pig","cow","frog","cat"]

try: 
    os.makedirs(output_directory)
except: 
    if not os.path.isdir(output_directory):
        raise 

for class_name in classes_to_include:
    class_directory = output_directory + class_name + "/"
    try: 
        os.makedirs(class_directory)
    except OSError:
        if not os.path.isdir(class_directory):
            raise 

classes_file = pd.read_csv(
    input_classes_filename, 
    encoding="utf-8",
    header = "infer"
)

for line in classes_file.itertuples(index = False): 
    file_class = line[3] # get the category/class 

    if file_class in classes_to_include:
        file_name = line[0]
        file_src = sounds_directory + file_name
        file_dst = output_directory + file_class + "/" + file_name
        try: 
            shutil.copy2(file_src, file_dst)
        except IOError: 
            raise 




```
