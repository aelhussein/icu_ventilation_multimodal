# icu_ventilation_multimodal
Ongoing project predicting ventilation risk in patients admitted to the icu using multmodal learning. we use a deep and cross network with joint fusion learning.

Overall we show that multimodal learning using joint fusion learning and a deep and cross network outperforms baseline neural network models and also exsiting published models.

**Question**

Mechanical ventilators are a crucial part of patient care for critically ill patients. However, their use is often resource constrained because of limited supply and available trained staff to operate them. The aim of this study is to use EHR and chest x-ray data to predict need for mechanically ventilated patients.

**Dataset**

We used the MIMIC-IV dataset

**Cohort**

We defined our cohort as patients diagnosed with pneumonia, respiratory failure, or acute respiratory distress syndrome (ARDS) who have been taken chest x-rays within 5 days of being admitted to the ICU, followed by an outcome of either invasive ventilation or death within 3 to 7 days after the observation window. 

**Features**

Features from EHR were selected based on medical importance and include heart rate, blood pressure, CO2 pressure and saturation level, platelet count, temperature, and Glasgow coma scale (GCS) score. 
Features with missing values over 30 percent were dropped, and remaining features were imputed using random forest imputation. Standard scaler was used to scale continuous variables, and the minority positive class was augmented using Synthetic Minority Over-sampling Technique (SMOTE) 

**Modelling**

We built a multimodal model that used CXR and EHR data. CXR images were processed using a pretrained resnet model that was further trained on chexpert images.  

Joint learning was forced by propagating loss to the resnet model to ensure iterative learning:

<img width="220" alt="image" src="https://user-images.githubusercontent.com/43360672/166834907-cb0901a8-b199-429f-9f29-3a311221a3c3.png">

We also employed a deep and cross network to enforce collaborative learning between image and structured data.

**Results**

A baseline EHR only model scored an AUC of 0.8
![image](https://user-images.githubusercontent.com/43360672/166835091-6b687d98-a7ac-4546-b1fa-67f2c5b221a4.png)


A baseline CXR only model scored an AUC of 0.76
![image](https://user-images.githubusercontent.com/43360672/166835108-0abff3ad-29a6-4032-b495-fd6d6b09768f.png)


The multimodal model scored an AUC of 0.85, suggesting and improvement in model performance
![image](https://user-images.githubusercontent.com/43360672/166835132-ddffc9cb-a912-46e3-b59d-69260f8cfbb8.png)


A calibration plot showed the model was well-calibrated for most risk groups although it tended to underestimate risk in some high risk groups

![image](https://user-images.githubusercontent.com/43360672/166835203-58933074-9d61-43aa-82cb-a8cb9985b0cb.png)



