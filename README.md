# Linguistic-based-Augmentation-Dataset
**Tiêu đề** Bộ dữ liệu được thu gom và sưu tầm trên internet gồm có các câu phản hồi của khách hàng trên các trang thương mại điện tử, nhằm mục đích học tập và nghiên cứu

**Nội dung**

-Bộ dữ liệu gồm 2 tệp 
    TrainSEOLE.txt  : Gồm 16107 câu bình luận
    TestSEOLE.txt  : Gồm 4000 câu bình luận trong đó 2000 câu tích cực và 2000 câu tiêu cực

-Cách gán nhãn 
    Nhãn "1" cho câu mang nghĩa tiêu cực
    Nhãn "0" cho câu mang nghĩa tích cực

-Hướng dẫn đọc file
----- python language ------

    #-*- coding: utf-8 -*-
    
    import pandas as pd

    class LoadData(object):

        def load_data_file(self, filename):
            a = []
            b = []
            regex = 'train_'
            with open(filename, 'r', encoding='UTF-8') as file:
                for line in file:
                    if regex in line:
                        b.append(a)
                        a = [line]
                    elif line != '\n':
                        a.append(line)
            b.append(a)
            return b[1:]

        def create_row(self, text):
            d = {}
            d['id'] = text[0].replace('\n', '')
            comment = ""
            for clause in text[1:-1]:
                comment += clause.replace('\n', ' ')
                comment = comment.replace('.', ' ')
            d['label'] = int(text[-1].replace('\n', ' '))
            d['comment'] = comment
            return d

        def load_data(self, filename):

            raw_data = self.load_data_file(filename)
            lst = []
            for row in raw_data:
                lst.append(self.create_row(row))
            return lst
        
    ld = LoadData()
    train_data = pd.DataFrame(ld.load_data('trainSEOLE.txt'))
    test_data = pd.DataFrame(ld.load_data('testSEOLE.txt'))
    print(train_data['comment'])
    print(test_data['comment'])



