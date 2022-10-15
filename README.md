This repo contain the code for conversion of the EEG data to its corresponding MRI via Using Unet, it shows that Unet can be used for this purpouse but some modification needs to be done in the architecture of the Unet to get better results.


#### How to generate data
1. Download the data from the source "https://osf.io/94c5t/files/osfstorage"
2. Download only EEG1, EEG2, fMRI zips only.
3. Create folder EEG_to_fMRI/data_set/EEG1 and extract both EEG zips into it, copy the data insider the extracted folder EEG1 and EEG2 and paste it to its parent folder i.e. at path EEG_to_fMRI/data_set/EEG1/. After that remove the EEG1 and EEG2 folder(which should be empty now).
4. Create folder EEG_to_fMRI/data_set/fMRI and extract the fMRI zip inside it, now copy the content from the extracted folder and past the content to its parent folder i.e. at path EEG_to_fMRI/data_set/fMRI. After that remove the fMRI folder i.e. the one we get after extraction of fMRI zip.
5. The python notebook should be at same folder in which EEG_to_fMRI is, i.e. parent folder of both should be same.
6. Finally the directory structure of EEG_to_fMRI is like below :
```
EEG_to_fMRI/
└── data_set
    ├── EEG1
    │   ├── 32
    │   │   ├── export
    │   │   │   ├── 20130410320002_Segmentation_bin.dat
    │   │   │   ├── 20130410320002_Segmentation_bin.vhdr
    │   │   │   └── 20130410320002_Segmentation_bin.vmrk
    │   │   └── raw
    │   │       ├── 20130410320002.eeg
    │   │       ├── 20130410320002.vhdr
    │   │       └── 20130410320002.vmrk
    │   ├── 35
    │   │   ├── export
    │   │   │   ├── 20130424350002_Pulse_Artifact_Correction_bin.dat
    │   │   │   ├── 20130424350002_Pulse_Artifact_Correction_bin.vhdr
    │   │   │   └── 20130424350002_Pulse_Artifact_Correction_bin.vmrk
    │   │   └── raw
    │   │       ├── 20130424350002.eeg
    │   │       ├── 20130424350002.vhdr
    │   │       └── 20130424350002.vmrk
    │   ├── 36
    │   │   ├── export
    │   │   │   ├── 20130425360002_Pulse_Artifact_Correction_bin.dat
    │   │   │   ├── 20130425360002_Pulse_Artifact_Correction_bin.vhdr
    │   │   │   └── 20130425360002_Pulse_Artifact_Correction_bin.vmrk
    │   │   └── raw
    │   │       ├── 20130425360002.eeg
    │   │       ├── 20130425360002.vhdr
    │   │       └── 20130425360002.vmrk
    │   ├── 37
    │   │   ├── export
    │   │   │   ├── 20130426370002_Pulse_Artifact_Correction_bin.dat
    │   │   │   ├── 20130426370002_Pulse_Artifact_Correction_bin.vhdr
    │   │   │   └── 20130426370002_Pulse_Artifact_Correction_bin.vmrk
    │   │   └── raw
    │   │       ├── 20130426370002.eeg
    │   │       ├── 20130426370002.vhdr
    │   │       └── 20130426370002.vmrk
    │   ├── 38
    │   │   ├── export
    │   │   │   ├── 20130105380002_Pulse_Artifact_Correction_bin.dat
    │   │   │   ├── 20130105380002_Pulse_Artifact_Correction_bin.vhdr
    │   │   │   └── 20130105380002_Pulse_Artifact_Correction_bin.vmrk
    │   │   └── raw
    │   │       ├── 20130105380002.eeg
    │   │       ├── 20130105380002.vhdr
    │   │       └── 20130105380002.vmrk
    │   ├── 39
    │   │   ├── export
    │   │   │   ├── 20130501390002_Pulse_Artifact_Correction_bin.dat
    │   │   │   ├── 20130501390002_Pulse_Artifact_Correction_bin.vhdr
    │   │   │   └── 20130501390002_Pulse_Artifact_Correction_bin.vmrk
    │   │   └── raw
    │   │       ├── 20130501390002.eeg
    │   │       ├── 20130501390002.vhdr
    │   │       └── 20130501390002.vmrk
    │   ├── 40
    │   │   ├── export
    │   │   │   ├── 20130510400002_Pulse_Artifact_Correction_bin.dat
    │   │   │   ├── 20130510400002_Pulse_Artifact_Correction_bin.vhdr
    │   │   │   └── 20130510400002_Pulse_Artifact_Correction_bin.vmrk
    │   │   └── raw
    │   │       ├── 20130510400002.eeg
    │   │       ├── 20130510400002.vhdr
    │   │       └── 20130510400002.vmrk
    │   ├── 42
    │   │   ├── export
    │   │   │   ├── 20130523420002_Pulse_Artifact_Correction_bin.dat
    │   │   │   ├── 20130523420002_Pulse_Artifact_Correction_bin.vhdr
    │   │   │   └── 20130523420002_Pulse_Artifact_Correction_bin.vmrk
    │   │   └── raw
    │   │       ├── 20130523420002.eeg
    │   │       ├── 20130523420002.vhdr
    │   │       └── 20130523420002.vmrk
    │   ├── 43
    │   │   ├── export
    │   │   │   ├── 20130529430002_Pulse_Artifact_Correction_bin.dat
    │   │   │   ├── 20130529430002_Pulse_Artifact_Correction_bin.vhdr
    │   │   │   └── 20130529430002_Pulse_Artifact_Correction_bin.vmrk
    │   │   └── raw
    │   │       ├── 20130529430002.eeg
    │   │       ├── 20130529430002.vhdr
    │   │       └── 20130529430002.vmrk
    │   ├── 44
    │   │   ├── export
    │   │   │   ├── 20130605440002_Pulse_Artifact_Correction_bin.dat
    │   │   │   ├── 20130605440002_Pulse_Artifact_Correction_bin.vhdr
    │   │   │   └── 20130605440002_Pulse_Artifact_Correction_bin.vmrk
    │   │   └── raw
    │   │       ├── 20130605440002.eeg
    │   │       ├── 20130605440002.vhdr
    │   │       └── 20130605440002.vmrk
    │   ├── 45
    │   │   ├── export
    │   │   │   ├── 20130627450002_Pulse_Artifact_Correction_bin.dat
    │   │   │   ├── 20130627450002_Pulse_Artifact_Correction_bin.vhdr
    │   │   │   └── 20130627450002_Pulse_Artifact_Correction_bin.vmrk
    │   │   └── raw
    │   │       ├── 20130627450002.eeg
    │   │       ├── 20130627450002.vhdr
    │   │       └── 20130627450002.vmrk
    │   ├── 46
    │   │   ├── export
    │   │   │   ├── 20130703460002_Pulse_Artifact_Correction_bin.dat
    │   │   │   ├── 20130703460002_Pulse_Artifact_Correction_bin.vhdr
    │   │   │   └── 20130703460002_Pulse_Artifact_Correction_bin.vmrk
    │   │   └── raw
    │   │       ├── 20130703460002.eeg
    │   │       ├── 20130703460002.vhdr
    │   │       └── 20130703460002.vmrk
    │   ├── 47
    │   │   ├── export
    │   │   │   ├── 20130710470002_Pulse_Artifact_Correction_bin.dat
    │   │   │   ├── 20130710470002_Pulse_Artifact_Correction_bin.vhdr
    │   │   │   └── 20130710470002_Pulse_Artifact_Correction_bin.vmrk
    │   │   └── raw
    │   │       ├── 20130710470002.eeg
    │   │       ├── 20130710470002.vhdr
    │   │       └── 20130710470002.vmrk
    │   ├── 48
    │   │   ├── export
    │   │   │   ├── 20130717480002_Pulse_Artifact_Correction_bin.dat
    │   │   │   ├── 20130717480002_Pulse_Artifact_Correction_bin.vhdr
    │   │   │   └── 20130717480002_Pulse_Artifact_Correction_bin.vmrk
    │   │   └── raw
    │   │       ├── 20130717480002.eeg
    │   │       ├── 20130717480002.vhdr
    │   │       └── 20130717480002.vmrk
    │   ├── 49
    │   │   ├── export
    │   │   │   ├── 20130918490002_Pulse_Artifact_Correction_bin.dat
    │   │   │   ├── 20130918490002_Pulse_Artifact_Correction_bin.vhdr
    │   │   │   └── 20130918490002_Pulse_Artifact_Correction_bin.vmrk
    │   │   └── raw
    │   │       ├── 20130918490002.eeg
    │   │       ├── 20130918490002.vhdr
    │   │       └── 20130918490002.vmrk
    │   └── 50
    │       ├── export
    │       │   ├── 20131003_500002_Pulse_Artifact_Correction_bin.dat
    │       │   ├── 20131003_500002_Pulse_Artifact_Correction_bin.vhdr
    │       │   └── 20131003_500002_Pulse_Artifact_Correction_bin.vmrk
    │       └── raw
    │           ├── 20131003_500002.eeg
    │           ├── 20131003_500002.vhdr
    │           └── 20131003_500002.vmrk
    └── fMRI
        ├── 32
        │   ├── 2_fl3D_t1_sag_fun_defaced.nii.gz
        │   └── 3_nw_mepi_rest_with_cross.nii.gz
        ├── 35
        │   ├── 2_fl3D_t1_sag_fun_defaced.nii.gz
        │   └── 3_nw_mepi_rest_with_cross.nii.gz
        ├── 36
        │   ├── 2_fl3D_t1_sag_fun_defaced.nii.gz
        │   └── 3_nw_mepi_rest_with_cross.nii.gz
        ├── 37
        │   ├── 2_fl3D_t1_sag_fun_defaced.nii.gz
        │   └── 3_nw_mepi_rest_with_cross.nii.gz
        ├── 38
        │   ├── 2_fl3D_t1_sag_fun_defaced.nii.gz
        │   └── 3_nw_mepi_rest_with_cross.nii.gz
        ├── 39
        │   ├── 2_fl3D_t1_sag_fun_defaced.nii.gz
        │   └── 3_nw_mepi_rest_with_cross.nii.gz
        ├── 40
        │   ├── 04_fl3D_t1_sag_fun_defaced.nii.gz
        │   └── 05_nw_mepi_rest_with_cross.nii.gz
        ├── 42
        │   ├── 2_fl3D_t1_sag_fun_defaced.nii.gz
        │   └── 3_nw_mepi_rest_with_cross.nii.gz
        ├── 43
        │   ├── 2_fl3D_t1_sag_fun_defaced.nii.gz
        │   └── 3_nw_mepi_rest_with_cross.nii.gz
        ├── 44
        │   ├── 2_fl3D_t1_sag_fun_defaced.nii.gz
        │   └── 3_nw_mepi_rest_with_cross.nii.gz
        ├── 45
        │   ├── 2_fl3D_t1_sag_fun_defaced.nii.gz
        │   └── 3_nw_mepi_rest_with_cross.nii.gz
        ├── 46
        │   ├── 2_fl3D_t1_sag_fun_defaced.nii.gz
        │   └── 3_nw_mepi_rest_with_cross.nii.gz
        ├── 47
        │   ├── 2_fl3D_t1_sag_fun_defaced.nii.gz
        │   └── 3_nw_mepi_rest_with_cross.nii.gz
        ├── 48
        │   ├── 2_fl3D_t1_sag_fun_defaced.nii.gz
        │   └── 3_nw_mepi_rest_with_cross.nii.gz
        ├── 49
        │   ├── 2_fl3D_t1_sag_fun_defaced.nii.gz
        │   └── 3_nw_mepi_rest_with_cross.nii.gz
        └── 50
            ├── 2_fl3D_t1_sag_fun_defaced.nii.gz
            └── 3_nw_mepi_rest_with_cross.nii.gz

```
