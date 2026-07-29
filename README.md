# Single Person 2D HPE Exploration

[View Full Report](CS_687_Final_Project_Report_Colin_Aslett.pdf)

## Project Description
This project explores two approaches for single-person 2D Human Pose Estimation on the Leeds Sports Pose dataset. A simplified DeepPose-based model (SDP) and a simplified HigherHRNet-based bottom-up model (SHHRN) were built and evaluated. The models were evaluated on pose metrics such as PCK, MSE, and prediction plots. Results show that mHHRN performed stronger across all evaluation metrics, with mDP performing poorly due to clustering of joints. This suggests that heatmap-based approaches perform better than regression-based for single-person 2D HPE.

## Results

<img width="668" height="307" alt="image" src="https://github.com/user-attachments/assets/5a095a71-f527-453f-aaf4-6db4d1160fd0" />


## Conclusion
This project’s main goal was to build and compare regression-based and heatmap-based approaches for single-person 2D HPE. It showed that heatmap-based  approaches were superior to regression-based models. However, with a better architecture the SDP might perform significantly better at a lower computation cost.

Both models have weaknesses on joint extremity and exact joint location and are far from performing close to the performance of top models. SDP needs extensive architecture reworks to fix the joint clustering problem. It is possible to switch the SDP model to use oracle-based cropping to better align with DeepPose, however I was hesitant in this project to give one model oracle-based cropping and the other full-image letterboxing.  Additional possible improvements to SDP would be to fine tune the limb-length loss and improve convolutional backbone. 

The main improvements that could be made to SHHRN would be adding more layers and resolution pyramids. This was not included in the current implementation of  SHHRN because the model already takes several hours on paid Google Colab GPUs to train. For both models, it is unlikely that additional processing such as geometric data augmentation would improve the performance but it would need to be investigated.

Overall, this project showed that relatively lightweight models can be built to attempt to solve HPE tasks. While the performance of the regression-based SDP is disappointing, further work needs to be done to determine the true potential of the model. The performance of the SHHRN model is mixed. While it does perform significantly better than the SDP model it performs far off the best models. Compute power was the primary limitation for the SHHRN model, with higher compute allowing for a potentially stronger model. Additional research needs to be done to see what leads OmniPose to a >99% mean PCK@0.2 result. It is possible that certain aspects of OmniPose can be added to improve both models. 
