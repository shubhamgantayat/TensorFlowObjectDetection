# Commands

## Download gitignore using curl

```bash
curl https://raw.githubusercontent.com/shubhamgantayat/general_template/main/.gitignore > .gitignore
```

# Initialization of Object Detection API
```bash
mkdir TensorFlow 
cd TensorFlow
```

## Clone the TensorFlow models folder here
```bash
git clone https://github.com/tensorflow/models.git
```

## Remove .git folder of the models directory


## Add models folder to .gitignore

## Go to TensorFlow/models/research
```bash
protoc object_detection/protos/*.proto --python_out=.
```

## Install the COCO API
```bash
pip install git+https://github.com/philferriere/cocoapi.git#subdirectory=PythonAPI
```

## Install Object Detection API
```bash
cp object_detection/packages/tf2/setup.py .
python -m pip install --use-feature=2020-resolver .
```
## Test your Installation
```bash
python object_detection/builders/model_builder_tf2_test.py
```

## Run Examples
- Creating workspace/example_1 in project root
    ```bash 
    mkdir -p workspace/example_1
    ```
- Change Directory to example_1
  ```bash
  cd workspace/example_1
  ```
- Download Notebook
  ```bash
  curl https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/_downloads/55b1ed8e083cbc9ca3bfc1c18eb6b860/plot_object_detection_saved_model.ipynb > plot_object_detection_saved_model.ipynb
  ```
  

## Create Custom Training Model
- Create Workspace
  ```bash
  mkdir workspace/training_demo
  cd workspace/training_demo
  mkdir -p annotations exported-models models pre-trained-models images/test images/train
  ```
  
- Create label_map.pbtxt in annotations folder and write content as 
  ```
  item {
    id: 1
    name: 'cat'
  }
  
  item {
      id: 2
      name: 'dog'
  }
  ```
  
- Curl generate_tfrecord.py file to training demo folder
  ```bash
  curl https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/_downloads/da4babe668a8afb093cc7776d7e630f3/generate_tfrecord.py > generate_tfrecord.py
  ```
  
- Create train and test record
  ```bash
  python generate_tfrecord.py -x [PATH_TO_IMAGES_FOLDER]/train -l [PATH_TO_ANNOTATIONS_FOLDER]/label_map.pbtxt -o [PATH_TO_ANNOTATIONS_FOLDER]/train.record
  python generate_tfrecord.py -x [PATH_TO_IMAGES_FOLDER]/test -l [PATH_TO_ANNOTATIONS_FOLDER]/label_map.pbtxt -o [PATH_TO_ANNOTATIONS_FOLDER]/test.record
  ```

## Configuring the training job

- Go to [model zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2_detection_zoo.md) and download SSD ResNet50 V1 FPN 640x640 (RetinaNet50)
- Extract the downloaded model into training_demo/pretrained-models

## Configure the training pipeline
- Create a folder my_ssd_resnet50_v1_fpn in training_demo/models folder
- copy pipeline.config to models/ from pre-trained-models directory
- update the pipeline.config as per the [documentation](https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/training.html)

## Copy training file from TensorFlow/models/research/object_detection/ to the training_demo folder
```bash
cp ../../TensorFlow/models/research/object_detection/model_main_tf2.py .
```

## start training by running the following command
```bash
python model_main_tf2.py --model_dir=models/my_ssd_resnet50_v1_fpn --pipeline_config_path=models/my_ssd_resnet50_v1_fpn/pipeline.config
```

## export the trained model
```bash
cp ../../TensorFlow/models/research/object_detection/exporter_main_v2.py .
python ./exporter_main_v2.py --input_type image_tensor --pipeline_config_path ./models/my_ssd_resnet50_v1_fpn/pipeline.config --trained_checkpoint_dir ./models/my_ssd_resnet50_v1_fpn/ --output_directory ./exported-models/my_model
```