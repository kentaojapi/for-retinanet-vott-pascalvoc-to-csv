import os
import glob
import pandas as pd
import xml.etree.ElementTree as ET


IMG_PATH = "YOUR_IMG_FOLDER_PATH"


def xml_to_csv(path):
    xml_list = []
    for xml_file in glob.glob(path + '/*.xml'):
        print(xml_file)
        tree = ET.parse(xml_file)
        root = tree.getroot()
        for member in root.findall('object'):
            bbx = member.find('bndbox')
            xmin = int(round(float(bbx.find('xmin').text)))
            ymin = int(round(float(bbx.find('ymin').text)))
            xmax = int(round(float(bbx.find('xmax').text)))
            ymax = int(round(float(bbx.find('ymax').text)))
            label = member.find('name').text

            value = (IMG_PATH + root.find('filename').text,
                     xmin,
                     ymin,
                     xmax,
                     ymax,
                     label
                     )
            xml_list.append(value)
    column_name = ['filename', 'xmin', 'ymin', 'xmax', 'ymax', 'class']
    xml_df = pd.DataFrame(xml_list, columns=column_name)
    return xml_df


def main():
    datasets = ['train', 'val', 'test']
    for ds in datasets:
        image_path = os.path.join(os.getcwd(), 'Annotations', ds)
        print(image_path)
        xml_df = xml_to_csv(image_path)
        xml_df.to_csv('labels_{}.csv'.format(ds), header=False, index=None)
        print('Successfully converted xml to csv.')


main()
