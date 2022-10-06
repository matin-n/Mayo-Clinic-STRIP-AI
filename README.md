# Mayo-Clinic-STRIP-AI

![images/header.png](images/header.png)


## Goal

The objective is to build a model that can classify two major acute ischemic stroke etiology subtypes: 
- CE (Cardioembolic) 
- LAA (Large Artery Atherosclerosis).

## Dataset Description

>The dataset for this competition comprises over a thousand high-resolution whole-slide digital pathology images. Each slide depicts a blood clot from a patient that had experienced an acute ischemic stroke. The slides comprising the training and test sets depict clots with an etiology (that is, origin) known to be either CE (Cardioembolic) or LAA (Large Artery Atherosclerosis).

### Data Field Descriptions

**train.csv:**
- `image_id`: A unique identifier for this instance having the form `{patient_id}`_`{image_num}`. Corresponds to the image `{image_id}.tif`.
- `center_id`: Identifies the medical center where the slide was obtained.
- `patient_id`: Identifies the patient from whom the slide was obtained.
- `image_num`:Enumerates images of clots obtained from the same patient.
- `label`: The etiology of the clot, either `CE` or `LAA`. This field is the classification target.

An example can be seen: 

| **image_id** | **center_id** | **patient_id** | **image_num** | **label** |
|--------------|---------------|----------------|---------------|-----------|
| 008e5c_0     | 11            | 008e5c         | 0             | CE        |
| 00c058_0     | 11            | 00c058         | 0             | LAA       |
| 026c97_0     | 4             | 026c97         | 0             | CE        |
| 049194_0     | 5             | 49194          | 0             | CE        |
| 049194_1     | 5             | 49194          | 1             | CE        |

## Preprocessing

The training WSI (Whole Slide Images) are massive in filesize due to their high resolutions. I was able to shrink the dataset down from ~241 gigabytes down to a few gigabytes. The preprocessing can be generalized: 

1. Load large .tif WSI
2. Crop WSI using [PyVips](https://libvips.github.io/pyvips/vimage.html#pyvips.Image.smartcrop) smart crop with attention features
3. Resize image to specified width x height
4. Delete parts of image that contain low signal
5. Export as JPEG with quality set to 100%

<!--
TODO:  Add preview images. 
<table>
<thead>
  <tr>
    <th>Before</th>
    <th>After</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><img src="image1.tif" width="400" height="300"></td>
    <td><img src="image1.jpg" width="400" height="300"></td>
  </tr>
  <tr>
    <td><img src="image2.tif" width="400" height="300"></td>
    <td><img src="image2.jpg" width="400" height="300"></td>
  </tr>
</tbody>
</table>
--> 

## Training

I was able to submit two models for evaluation due to time constraints and issues with loading images without running out of memory. First, I tried [AutoGluon](https://github.com/awslabs/autogluon) with [swin_large_patch4_window7_224](https://github.com/microsoft/Swin-Transformer). Second, I used Keras with Tensorflow to apply transfer learning & fine-tuning techniques by using the latest [EfficientNet B4 with NoisyStudent + RandAugment](https://github.com/tensorflow/tpu/tree/master/models/official/efficientnet) pre-trained weights.

I attempted to use [Monai](https://monai.io), [fastMonai](https://fastmonai.no/), [PathML](http://pathml.org), and [cuCIM](https://github.com/rapidsai/cucim), but I encountered problems properly loading the WSI (memory constraints or unknown error) or slow processing. However, these libraries appear promising, and I would like to experiment with them again in the future.