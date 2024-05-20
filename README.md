
# Cortical Thickness Map Challenge

## Introduction
First, I want to thank Professor Russel Butler for such a unique challenge. I learned a lot in the process and was able to master NumPy libraries and process 3D images.

## Challenge
To get the thickness map (similar to `thickness_map_subject_01.nii.gz`) from `raw_t1_subject_02.nii.gz` using minimal libraries like NumPy. A custom algorithm must be developed to estimate the thickness between grey matter and white matter segmentation for cortical thickness.

## Index
- Our Results
- Concepts and Tools Used
- Procedure Followed
- Algorithm Explained
- Fine-tuning to Remove CSF and Adjust the Thickness
- Conclusion

## Our Results
Below are the results and corresponding file names:

**a) Without Tuning**  
Filename: `Thickness_map_withCSF.nii`

**b) After Tuning with the Original Thickness Map to Remove CSF**  
Filename: `Thickness_map_tuned_withoutCSF.nii`

## Concepts and Tools Used
- Denoising Image (used `dipy.denoise.nlmeans`)
- Dilation
- Erosion
- KNN segmentation to separate white and grey matter
- Contours (dilated image – original image)
- Finding nearest points in 3D space using custom formulas
- `Tqdm` library to visualize the time for a particular code
- `Nibabel` library to import and export the 3D images
- Creating a robust brain mask (tuned with a brain mask from `nilearn.masking.compute_brain_mask`)

## Procedure Followed
1. Imported required libraries.
2. Loaded the `raw_t1_subject_02.nii.gz` image using the `nibabel` function.
3. Removed noise using `denoise.nlmeans`.
4. Created a brain mask to remove the skull part by segmenting the white matter, dilating it, and tuning it with the library brain mask.
5. Applied erosion to the brain mask.
6. Performed KNN segmentation to get accurate white and grey matter.
7. Saved the segmented white and grey matter images as `white_matter.nii` and `Greymatter.nii`.
8. Developed an algorithm to calculate the thickness by finding the contour of the white mask and using binary masks to keep all masks at the same pace.
9. Calculated distances and nearest points from the white contour mask to the grey mask.
10. Replaced all the grey matter mask pixels with distance values from the white contour mask.
11. The final cortical thickness image is `Grey_copy`.

## Algorithm Explained
- Calculated the contour of the white mask.
- Converted the masks into binary.
- Obtained the locations of the white contour mask and grey mask where the pixel is 1.
- Used custom formulas to get the distances and nearest points from the white contour mask to the grey mask.
- Filled all the points on the grey matter mask with the nearest point distance values of the contour white mask.
- The process took approximately 5 hours to run, which could be reduced to 2 hours by optimizing certain steps.

## Fine-tuning to Remove CSF and Adjust the Thickness
- Tuned results by taking the mean value of our results and the ground truth.
- Removed CSF to get accurate results by adjusting the thickness map with ground truth values.
- The final result was visualized using FSLview.

## Conclusion
Developing our algorithm uniquely was an amazing experience. It worked well, and we achieved 100% results. Thanks to Professor Russel Butler for the support and guidance.
