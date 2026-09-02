# Day 3 Data Sources

Every file in this directory derives from one published dataset, which is cited
and licensed below. Nothing here was generated, and nothing was collected for
this workshop.

## The Source Dataset

- **Title:** brain tumor dataset.
- **Author:** Jun Cheng, School of Biomedical Engineering, Shenzhen University,
  Shenzhen, China.
- **Repository:** figshare.
- **DOI:** `10.6084/m9.figshare.1512427`.
- **Licence:** Creative Commons Attribution 4.0 International, which permits
  redistribution and adaptation provided the author is credited.
- **Citation:** Cheng, Jun (2017). brain tumor dataset. figshare. Dataset.
  `https://doi.org/10.6084/m9.figshare.1512427`.

The dataset accompanies two papers, which are the works to cite when writing
about results obtained from it.

- Cheng, Jun, et al. "Enhanced Performance of Brain Tumor Classification via
  Tumor Region Augmentation and Partition." PLoS ONE 10.10 (2015).
- Cheng, Jun, et al. "Retrieval of Brain Tumors by Adaptive Spatial Pooling and
  Fisher Vector Representation." PLoS ONE 11.6 (2016).

## What The Source Contains

The complete archive holds 3064 T1-weighted contrast-enhanced MRI slices from
233 patients, divided into three tumour types, being 708 meningioma slices,
1426 glioma slices, and 930 pituitary tumour slices. Every slice carries the
tumour type, a patient identifier, a boundary delineated by hand, and a binary
mask of the tumour region.

The archive records the acquisition protocol as follows. The images were
acquired after Gd-DTPA injection at Nanfang Hospital, Guangzhou, China and at
the General Hospital of Tianjin Medical University, China, between September
2005 and October 2010. It gives the in-plane resolution as 512 by 512 with
pixel dimensions of 0.49 by 0.49 millimetres, the slice thickness as 6
millimetres, and the slice gap as 1 millimetre.

## What This Directory Contains

- `slices/`, holding 844 greyscale JPEG images, being 291 glioma, 274
  meningioma, and 279 pituitary slices from 66 patients, with 22 patients of
  each tumour type and up to 14 slices per patient.
- `masks/`, holding one PNG per slice under the same name, in which a pixel
  value of 255 marks tumour and 0 marks everything else.
- `slices.csv`, holding one row per slice with the columns `file`,
  `patient_id`, and `tumor_type`.

Of the 844 images, 830 are 512 by 512 and 14 are 256 by 256.

Every file name has the form `<tumor_type>_<patient_id>_<slice>.jpg`, where the
tumour type and the patient identifier are the ones the archive records and the
slice number is the archive's own numbering for that image.

## How These Files Were Prepared

The four archive volumes were downloaded from the DOI above and read directly.
No image was cropped, rotated, filtered, or resampled, and no mask was
adjusted.

Three transformations were applied.

The pixel values were converted to 8-bit greyscale. The archive stores each
slice as 16-bit integers whose range differs from one acquisition to the next,
so each slice was scaled on its own minimum and maximum, which is the
conversion the archive's own documentation supplies for this purpose. The JPEG
encoding uses quality 85.

The arrays were transposed. The archive is a MATLAB file, which stores arrays in
the opposite order from the one the Python reader returns them in, so both the
image and its mask were transposed to recover the orientation in which the
tumour boundary was drawn.

The masks were written as PNG files, from the binary tumour mask the archive
stores alongside each image, with the value 1 rewritten as 255 so the files
display correctly in an ordinary image viewer.

## How The Subset Was Chosen

The 66 patients were drawn from the 233 in the archive by taking, for each
tumour type, every patient with at least 8 slices and then selecting 22 of them
with a random number generator seeded at 42. For each selected patient the
first 14 slices in the archive's numbering were kept. One patient, 108931, was
retained deliberately rather than drawn at random.

The subset exists because the complete archive is 880 megabytes, which is too
large to distribute through this repository.

## Network Access

Neither notebook in this day reaches the network. Every file the notebooks read
is stored in this directory.
