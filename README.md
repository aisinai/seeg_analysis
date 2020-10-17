# SEEG Analysis
 **This repo contains the materials needed to process electroencephalographic (EEG) data into a format that is compatible with the unsupervised Telemanom LSTM framework created by:**
 
 title={Detecting Spacecraft Anomalies Using LSTMs and Nonparametric Dynamic Thresholding},
  author={Hundman, Kyle and Constantinou, Valentino and Laporte, Christopher and Colwell, Ian and Soderstrom, Tom},
  journal={arXiv preprint arXiv:1802.04431},
  year={2018}
  
 ## **Content:**
 
  This repo contains a data pre-processing jupyter notebook that guides the user in converting EEG files from an EDF format into scaled, standardized numpy arrays that are easily ingested into the LSTM framework.
  
  The post-processing jupyter notebook allows users to take the anomalous sequences identified by the LSTM and convert them into time points that can be identified on the original EEG sequence, for purposes of confirming true positives, false positives, and false negatives.
  
  The LSTM folder contains the unsupervised LSTM code (originally by Hundman et al.) that was modified for the purposes of this study.
  
  A de-identified sample EEG recording (full EDF file) for demonstrative purposes is available at: https://drive.google.com/drive/folders/13Oy5ZjePZQaUpAYVMdvXfwrcOMxbZa7M?usp=sharing
  
  ## **Instructions for Use:**
  
  Clone the repo:
  `git clone https://github.com/aisinai/seeg_analysis && cd LSTM`

  Install dependencies using Python 3.6+ (a virutal environment is recommended here):
  `pip install -r requirements.txt`

Additional details for setup and troubleshooting may be found at: https://github.com/khundman/telemanom/blob/master/README.md

  Once the Telemanom LSTM framework has been set up, pre-process the EEG data from raw EDF format to processed numpy arrays ready for ingestion into the Telemanom LSTM framework. This is done using the Pre-Processing Jupyter notebook which uses open-source code from MNE (see https://mne.tools/stable/index.html).
  
  We recommend running this notebook inside of a Docker container which has MNE and all dependent softwares pre-installed. We recommend using the Docker container available here: https://hub.docker.com/r/ejolly/mind-tools.
  
  A sample de-identified EDF for full demonstrative purposes is available at: https://drive.google.com/drive/folders/13Oy5ZjePZQaUpAYVMdvXfwrcOMxbZa7M?usp=sharing.
  
 Download this EDF file and place it in the root of the project folder where the Docker container above will be launched. Insert the path to the Sample EDF file in the relevant portions of the Pre-Processing Jupyter Notebook and execute the code to generate pre-processed train and test numpy arrays that are ready for use with the Telemanom LSTM framework.
  
  Pre-split training and test sets must be placed in directories named data/train/ and data/test in the 'LSTM' folder. One .npy file should be generated for each channel or stream (for both train and test) with shape (n_timesteps, n_inputs).
  
  Enter the virtual environment created above (with the dependencies specified in the requirements.txt installed) and start processing each of the data channels with the following command:
   
   `python run.py`
   
 Each time the system is started a unique datetime ID will be used to create a results file (in results/) that details the sequence positions of the identified anomalous sequences and related information. In addition, a data subdirectory containing data files for created models, predictions, and smoothed errors for each channel. A file called params.log is also created that contains parameter settings and logging output during processing.
 
 Once the anomalous sequences have been identified in the results files, these files can be opened using the Post-Processing Jupyter notebook to translate the anomalous sequence positions of the array into times relative to the start of the recording. These times can then be compared with the times of seizure events noted by any epileptologists who have reviewed the original data recordings (e.g. "A 2-minute seizure occurred during minutes 15:45:32 - 17:42:10 of this recording in the hippocampal leads").
 
 For concurrent video analysis, videos are recommended to be in .avi format. A convolutional long short term memory auto encoder, previously described by Chong et al. (see https://arxiv.org/abs/1701.01546), was used to successfully detect video anomalies across time. Using the code described at https://github.com/hashemsellat/video-anomaly-detection/blob/master/README.md, we determined a regularity score that was calculated for all frames of the patient videos, with anomalous events having noticeably lower regularity scores. These regularity scores over time may be represented as numpy array time series data, similar to the pre-processed numpy arrays of EEG data. The time frames of when these regularity scores decrease was used to recognize when a seizure was occurring by inputting the regularity score time series into the Telemanom LSTM framework for automated detection of regularity score changes (e.g. anomalous events). Sample datasets are not publicly available without prior request and completion of a data use agreement, due to the fact that the videos contain recognizable patient images and cannot be de-identified. We recommend that users use their own video recordings for these experiments.
  
  
  
