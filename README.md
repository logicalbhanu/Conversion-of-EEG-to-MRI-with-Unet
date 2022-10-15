This repo contain the code for conversion of the EEG data to its corresponding MRI via Using Unet, it shows that Unet can be used for this purpouse but some modification needs to be done in the architecture of the Unet to get better results.


#### How to generate data
1. Download the data from the source "https://osf.io/94c5t/files/osfstorage"
2. Download only EEG1, EEG2, fMRI zips only.
3. Create folder EEG_to_fMRI/data_set/EEG1 and extract both EEG zips into it, copy the data insider the extracted folder EEG1 and EEG2 and paste it to its parent folder i.e. at path EEG_to_fMRI/data_set/EEG1/. After that remove the EEG1 and EEG2 folder(which should be empty now).
4. Create folder EEG_to_fMRI/data_set/fMRI and extract the fMRI zip inside it, now copy the content from the extracted folder and past the content to its parent folder i.e. at path EEG_to_fMRI/data_set/fMRI. After that remove the fMRI folder i.e. the one we get after extraction of fMRI zip.
5. The python notebook should be at same folder in which EEG_to_fMRI is, i.e. parent folder of both should be same.
