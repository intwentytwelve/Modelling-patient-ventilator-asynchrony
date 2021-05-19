# Modelling-Patient-Ventilator-Asynchrony
As healthcare development increasingly depends on clinical decision support systems (CDSS) to digitize high volume of breathing waveform data from ventilators, more and more advanced techniques have been applied in optimizing anomaly detection in the early stage of the respiratory diseases for patients in the intensive care unit (ICU). It would be no exaggeration to say that CDSS are widely applied in the area of ventilators for detecting patient-ventilator asynchrony (PVA). PVA is defined as a mismatch between inspiratory as well as expiratory processes of patients and ventilators regarding flow and pressure supply.

## Table of Contents
1. [Prerequisites](#Prerequisites)
2. [Data](#Data)
3. [Methodologies](#Methodologies)
4. [Implementation](#Implementation)

### Prerequisites
* Jupyter Notebook
* Numpy
* Keras
* Tensorflow
* Sklearn.svm

### Data
Ventilators display streaming waveform data to show health conditions of a patient. Ventilator waveforms describe a visual human machine interaction between the patient and the ventilator about breathing information. It is the most direct and common way to detect asynchronous data that are used by clinicians to diagnose and treat patients in real time. A normal waveform data mainly contains flow and pressure versus time scalars in Fig 1:

![Fig 1](download1.png)

In our study, breath metadata come from 5 distinctive patients who received consecutive ventilation in ICU at University of California Davis Medical Center. Each row of metadata represents an intact breath, containing 16 columns of clinically relevant data such as breath number (BN), tidal volume inhaled (TVi), tidal volume exhaled (TVe) and so on. The main breath metadata are shown as follows:
| Name | Units | Description |
| ------------- | ------------- | ------------- |
| TVi | ml | Amount of air breathed in |
| TVe	| ml | Amount of air breathed out |
| TVe/TVi ratio |	N/A |	Ratio of TVi/TVe |
| I-time | seconds | Inspiratory time |
| E-time | seconds | Expiratory time |
| I:E ratio	| N/A	| Ratio of I-time/E-time |


Raw ventilator data needs to be formatted in an expected way so that our software is able to understand and read it. With the help of a python library called ventmap, an open-source multi-purpose ventilator analytic was developed for processing ventilator waveform data, raw breath metadata can be turned into a 2-column waveform PB-840 (Puritan Bennett 840, Covidien, U.S.) format.

### Methodologies
The proposed system is designed to have two components including a 1D CNN time-series forecasting model and a one-class SVM anomaly detection model. The 1D CNN is used for predicting next step breathing observation based on previous one. The predicted data and the actual data are then fed into the one-class SVM, which acts as an anomaly detector for detecting PVA in the out of sample dataset that lies out of the boundary it creates. At the same time, it has the ability of real-time monitoring, locating when the PVA happened within a breath against time sequences.

### Implementation
The specific implementation is shown in:

[main.ipynb](main.ipynb)

## Authors
* Wen Li - MEng in Department of Electrical and Computer Engineering, University of Alberta, Canada
* Wenjie Xu - Ph.D in Department of Electrical and Computer Engineering, University of Alberta, Canada
* Omashor Precious - MEng in Department of Electrical and Computer Engineering, University of Alberta, Canada
* Scott Dick - Professor in Department of Electrical and Computer Engineering, University of Alberta, Canada
