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
