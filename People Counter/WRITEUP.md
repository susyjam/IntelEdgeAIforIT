[Faster_rcnn_inception_v2_coco_2018_01_28]: https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md
[person-detection-retail-0013]: https://docs.openvinotoolkit.org/2019_R3/_models_intel_person_detection_retail_0013_description_person_detection_retail_0013.html
[Ssd_inception_v2_coco]: https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md

# Project Write-Up

The people counter application will demonstrate how to create a smart video IoT solution using Intel® hardware and software tools. The app will detect people in a designated area, providing the number of people in the frame, average duration of people in frame, and total count.

![people-counter-python](./intel%20proyect%201%2013.png)
![people-counter-python](./intel%20proyecto%201%2013%2036.png)

## Explaining Custom Layers

One of the reasons of the success of deep learning is the wide range of layers that can be used an combined to create a model. But this is because developers are not constrained to the existent layers, but can create their own ones so they can solve an specific problem or implement an specific operation you can need in your model, or creating a customized version of an existing layer.
To create a custom layer for OpenVino, you must add extensions to the Model Optimizer and the Inference Engine. For this, the first step is to use the Model Extension Generator tool The MEG is going to create templates for Model Optimizer extractor extension, Model Optimizer operations extension, Inference Engine CPU extension and Inference Engine GPU extension. Once customized the templates, next step is to generate the IR files with the Model Optimizer. Finally, before using the custom layer in your model with the Inference Engine, you must: first, edit the CPU extension template files, second, compile the CPU extension and finally, execute the model with the custom layer.

## Comparing Model Performance

Comparing the two models i.e. ssd_inception_v2_coco and faster_rcnn_inception_v2_coco in terms of latency and memory, several insights were drawn. It could be clearly seen that the Latency (microseconds) and Memory (Mb) decreases in case of OpenVINO as compared to plain Tensorflow model which is very useful in case of OpenVINO applications.

## Assess Model Use Cases

Some of the potential use cases of the people counter app are:

  1. It helps to improve in-store operations and individual monitoring for certain tasks.
  2. Customer Traffic inside warehouses could help in mitigating risk factors. Also it can help to provide visitor analytics.
  3. Each of these use cases would be useful in a any Shopping Center, Retail Chain, Library, Bank etc. Counting data will help you make well-informed decisions about your business and your data analytics team to make informed decision.
  4. Controlling the number of people present in a particular area. Further, with some updations, this could also prove helpful in the current COVID-19 scenario i.e. to keep a check on the number of people in the frame.
  5. Also for COVID scenario, with some modifications it can also help in managing safe distance between individuals.

## Assess Effects on End User Needs

Lighting, model accuracy, and camera focal length/image size have different effects on a deployed edge model. The potential effects of each of these are as follows...

  Determining various models and their accuracy based on the frame size.
  Better be the model accuracy more are the chances to obtain the desired results through an app deployed at edge.
  Focal length/image also have a effect as better be the pixel quality of image or better the camera focal length,more clear results we will obtain.

## Model Research

In investigating potential people counter models, I tried each of the following three models:

- Model 1: [Faster_rcnn_inception_v2_coco_2018_01_28]

  - Converted the model to intermediate representation using the following command. it performed really well in the output video. The model works better than the previous approaches.
  - After managing the shape attribute it worked quite well.
  - I converted the model to an Intermediate Representation with the following arguments :
    - ```tar -xvf faster_rcnn_inception_v2_coco_2018_01_28.tar.gz```
    - ```cd faster_rcnn_inception_v2_coco_2018_01_28.tar.gz```
    - ```python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py --input_model frozen_inference_graph.pb --tensorflow_object_detection_api_pipeline_config pipeline.config --reverse_input_channels --tensorflow_use_custom_operations_config /opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf/faster_rcnn_support.json```
  
- Model 2: [person-detection-retail-0013]

  - Converted the model to intermediate representation using the following command. it performed really well in the output video
  - it worked quite well.
  - I converted the model to an Intermediate Representation with the following arguments...


- Model 3: [Ssd_inception_v2_coco]

  - Converted the model to intermediate representation using the following command. Further, this model lacked accuracy as it didn't detect people correctly in the video. 
  - The model was insufficient for the app because when i tested it failed on intervals and it didn't found the bounding boxes around the person and for next person.
  - I converted the model to an Intermediate Representation with the following arguments :
    - ```tar -xvf ssd_inception_v2_coco_2018_01_28.tar.gz```
    - ```cd ssd_inception_v2_coco_2018_01_28```
    - ```python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py --input_model frozen_inference_graph.pb --tensorflow_object_detection_api_pipeline_config pipeline.config --reverse_input_channels --tensorflow_use_custom_operations_config /opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf/ssd_v2_support.json```
    
 by Susyjam
  

