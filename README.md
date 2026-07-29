# Single Person 2D HPE Exploration

[View Full Report](CS_687_Final_Project_Report_Colin_Aslett.pdf)

## Project Description
This project explores two approaches for single-person 2D Human Pose Estimation on the Leeds Sports Pose dataset. A simplified DeepPose-based model (SDP) and a simplified HigherHRNet-based bottom-up model (SHHRN) were built and evaluated. The models were evaluated on pose metrics such as PCK, MSE, and prediction plots. Results show that mHHRN performed stronger across all evaluation metrics, with mDP performing poorly due to clustering of joints. This suggests that heatmap-based approaches perform better than regression-based for single-person 2D HPE.

## Results
Both models were evaluated once on the test set. The PCK with threshold of 0.2 results are shown in table 1. SHHRN performs significantly better across all joints and in the mean. This suggests that the heatmap approach is better for single-person 2D HPE tasks. The very low score for PCK indicates that the project's task was too hard for the SDP model. For context, Zhang (2025) reported that the top models performed between 92 and 94%, with >99% PCK@0.2 for OmniPose. Toshev and Szegedy (2014) evaluated DeepPose on LSP/LSPExtended and reported an average PCP@0.5 of 0.61. Average PCP@0.5 for SDP was 0.0. HigherHRNet was evaluated primarily on the COCO dataset (Cheng et al., 2020).

<img width="668" height="307" alt="image" src="https://github.com/user-attachments/assets/5a095a71-f527-453f-aaf4-6db4d1160fd0" />

SDP performed poorly across all joints, but especially with extremity joints. Several of those joints had a reported PCK@0.2 of 0.0 meaning the model never correctly predicted the coordinate of the joint within the threshold. SDP performed its strongest on joints that were closer to the center of the person. This suggests that SDP may have learned how to estimate the rough location of the body but failed to preserve exact joint coordinates. Figure 7 shows a visual prediction for SDP on test images 1 and 2 within the LSP dataset. For both images the SDP model is placing all predicted joint coordinates roughly in the center of the person. This aligns with the analysis of SDP finding the body but losing precise joint coordinates. The limb-length loss was added to SDP in an attempt to help the model learn correct anatomical positions, however it had only a small role in the model’s learning. Limb-length loss was not able to help the model if it had already lost the precise joint coordinates. If additional ground-truth crops were given to the model, similar to the original DeepPose, SDP would have most likely performed better. However, the goal of the project was to evaluate the models on a sports image that only had joint annotations. 

## Visual Results

<img width="585" height="333" alt="image" src="https://github.com/user-attachments/assets/7fe66288-5526-469c-b382-81cdd0809c99" />

<img width="583" height="323" alt="image" src="https://github.com/user-attachments/assets/d0036f25-279d-4330-a688-7abbcb8c582c" />

## Conclusion
This project’s main goal was to build and compare regression-based and heatmap-based approaches for single-person 2D HPE. It showed that heatmap-based  approaches were superior to regression-based models. However, with a better architecture the SDP might perform significantly better at a lower computation cost.

Both models have weaknesses on joint extremity and exact joint location and are far from performing close to the performance of top models. SDP needs extensive architecture reworks to fix the joint clustering problem. It is possible to switch the SDP model to use oracle-based cropping to better align with DeepPose, however I was hesitant in this project to give one model oracle-based cropping and the other full-image letterboxing.  Additional possible improvements to SDP would be to fine tune the limb-length loss and improve convolutional backbone. 

The main improvements that could be made to SHHRN would be adding more layers and resolution pyramids. This was not included in the current implementation of  SHHRN because the model already takes several hours on paid Google Colab GPUs to train. For both models, it is unlikely that additional processing such as geometric data augmentation would improve the performance but it would need to be investigated.

Overall, this project showed that relatively lightweight models can be built to attempt to solve HPE tasks. While the performance of the regression-based SDP is disappointing, further work needs to be done to determine the true potential of the model. The performance of the SHHRN model is mixed. While it does perform significantly better than the SDP model it performs far off the best models. Compute power was the primary limitation for the SHHRN model, with higher compute allowing for a potentially stronger model. Additional research needs to be done to see what leads OmniPose to a >99% mean PCK@0.2 result. It is possible that certain aspects of OmniPose can be added to improve both models. 
