# seeg_analysis
 This repo contains the materials needed to process electroencephalographic (EEG) data into a format that is compatible with the unsupervised Telemanom LSTM framework created by:
 
 title={Detecting Spacecraft Anomalies Using LSTMs and Nonparametric Dynamic Thresholding},
  author={Hundman, Kyle and Constantinou, Valentino and Laporte, Christopher and Colwell, Ian and Soderstrom, Tom},
  journal={arXiv preprint arXiv:1802.04431},
  year={2018}
  
  This repo contains a data pre-processing notebook that guides the user in converting EEG files from an EDF format into scaled, standardized numpy arrays that are easily ingested into the LSTM framework.
  
  The post-processing notebook allows users to take the anomalous sequences identified by the LSTM and convert them into time points that can be identified on the original EEG sequence, for purposes of confirming true positives, false positives, and false negatives.
  
  The LSTM folder contains the unsupervised LSTM code (originally by Hundman et al.) that was modified for the purposes of this study.
