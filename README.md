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
