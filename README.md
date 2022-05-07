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
