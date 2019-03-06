# Human Detection
This repository contains annotations of the UCF-ARG dataset  (not images) and some of the configuration files to train the human detector for a Search And Rescue application, 
using [Tensorflow's object detection API](https://github.com/tensorflow/models/tree/master/research/object_detection). 

The final model has been fine-tuned using ssd_mobilenet_v1_coco of the [models pre-trained](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md)
on the [COCO dataset](http://mscoco.org/) as a starting point (*transfer learning*).




## Installation 

### Trying the dataset
In order to try the dataset, you first need to follow the [installation instructions](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/installation.md) on the Tensorflow page. 
### Google Cloud
In to use Google Cloud resources, you need to install the [google SDK](https://cloud.google.com/sdk/) on the Google Cloud page. 



## File configuration 
* *pipeline*: *.config* In order to fine-tune the model, you need to configurate the *fine_tune_checkpoint, label_map_path and input_path* to your own repository. If you will run with a Google Cloud bucket, you can use *gs://my-bucket*. 
* *annotations*: *.xml* In you want to create new FTRecord files with other images, you need to change the path of the *xml* files to your own path. 
* *hyperparameters*: *cloud.yuml.* Probably you need to change the *runtime version, masterType, workerType, parameterServerType* if you will train with a distribute architecture and GPU resources such in [google cloud platform] (https://cloud.google.com/solutions/running-distributed-tensorflow-on-compute-engine).

## File description
### Folders
* *annotations*: *xml* files with the boundig boxes of each image, obtained using [labelImg](https://github.com/tzutalin/labelImg), and a text file assigning each image to one of person class. 
* *graph_images*: plots of the Total Loss of the trained model.
* *images*: 1947 jpg train images.
* *data*: configuration file of the net trained, label map and tensorflow records (created with [create_sw_tf_record.py](create_sw_tf_record.py)).
* *test_images*: 493 images not used to train the model.

### Scripts
* *check_duplicate_images.py*: script that allows you to check if there are duplicate images in one or two directories. Useful when collecting the train and test images.
* *create_sw_tf_record.py*: modified version of [create_pet_tf_record.py](https://github.com/tensorflow/models/blob/master/research/object_detection/create_pet_tf_record.py), where the paths have been changed along with the regular expression in *line 60* to adapt to my images names.
* *export_inference_graph.py*: an exact copy of [export_inference_graph.py](https://github.com/tensorflow/models/blob/master/research/object_detection/export_inference_graph.py) in Tensorflow's API.
