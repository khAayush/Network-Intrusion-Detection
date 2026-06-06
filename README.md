# Big Data Analytics for Network Intrusion Detection Using Machine Learning

## Abstract

Network intrusion detection is a critical component of modern cybersecurity infrastructure, requiring sophisticated machine learning algorithms to effectively identify malicious activities in high-volume network traffic. This research presents a comprehensive big data analytics pipeline for network intrusion detection using the UNSW-NB15 dataset. XGBoost is employed as the primary classifier, combined with advanced preprocessing techniques including SMOTE, feature engineering, and importance-based feature selection.

The proposed model achieves **99.75% accuracy**, **99.90% precision**, **99.60% recall**, **99.75% F1-score**, and a **ROC-AUC score of 0.9980**, demonstrating exceptional intrusion detection performance. Results indicate that connection-count features, traffic load metrics, and packet statistics are among the strongest indicators of malicious activity.

**Keywords:** Big Data Analytics, Intrusion Detection, Network Security, Cybersecurity, Machine Learning, XGBoost, SMOTE, Feature Engineering

# I. Background of the Study

## A. Generic Information

Network intrusion detection aims to identify and respond to unauthorized access attempts and malicious activities within computer networks. Machine learning techniques have become increasingly effective for automated threat detection due to their ability to learn attack patterns without relying solely on manually crafted security rules.

## B. Problem Statement

Traditional intrusion detection systems face challenges due to:

- Rapid growth in network traffic volume and complexity.
- Severe class imbalance in intrusion datasets.
- High-dimensional feature spaces with complex dependencies.
- Modern polymorphic attacks that evade signature-based detection.

## C. Aim and Objectives

The primary objective is to develop a high-performance machine learning pipeline capable of classifying network traffic as either **normal** or **intrusive** while minimizing false positives and maximizing attack detection.

## D. Contributions

- Advanced preprocessing pipeline with SMOTE balancing.
- Domain-specific feature engineering.
- Importance-based feature selection.
- Hyperparameter-optimized XGBoost classifier.
- Comprehensive evaluation and interpretability analysis.

# II. Related Work

Earlier intrusion detection research heavily relied on the KDD99 dataset, which suffered from unrealistic distributions and poor detection of sophisticated attacks. More recent work transitioned to the UNSW-NB15 dataset, enabling more realistic evaluation of modern cyberattacks.

Researchers have applied Random Forests, Extra Trees, Deep Neural Networks, and Multilayer Perceptrons to improve detection rates. Many studies also employ SMOTE to address dataset imbalance.

This work focuses on a streamlined, interpretable, and computationally efficient pipeline centered on XGBoost.

# III. Methodology

## A. System Architecture

The proposed pipeline consists of:

1. Data Acquisition and Exploration
2. Data Preprocessing and Feature Engineering
3. Feature Selection and Dimensionality Reduction
4. Model Development and Hyperparameter Tuning
5. Model Evaluation and Validation
6. Deployment and Monitoring

## B. Dataset Description

The UNSW-NB15 dataset contains:

| Property | Value |
|----------|--------|
| Total Records | 254,686 |
| Features | 42 |
| Training Records | 176,419 |
| Testing Records | 78,267 |
| Attack Categories | 9 |
| Attack Proportion | ~3.8% |

## C. Data Preprocessing

### Initial Cleaning

- Removal of non-feature columns.
- Missing-value handling using median imputation.
- Label encoding of categorical variables.
- Data integrity verification.

### Feature Scaling

All numerical features were standardized using StandardScaler.

## D. Feature Engineering

Eight derived features were created:

- Byte Ratio
- Packet Ratio
- Packet Rate
- Total Traffic
- Average Source Packet Size
- Average Destination Packet Size
- Load Ratio
- Loss Ratio

These features capture traffic asymmetry and behavioral anomalies associated with cyberattacks.

## E. Class Imbalance Handling

SMOTE was applied to balance the minority attack class and produce a 1:1 class ratio during training.

## F. Feature Selection

Two-stage feature selection was performed:

1. Correlation-based feature removal.
2. Importance-based selection using XGBoost.

The final feature set contained **24 features**, retaining **95% cumulative importance**.

## G. Model Development

### Algorithm

**XGBoost** was selected because of:

- Strong performance on structured data.
- Robustness to missing values.
- Built-in feature importance estimation.

### Hyperparameter Tuning

Three configurations were evaluated using stratified 5-fold cross-validation.

# IV. Results and Discussion

## A. Data Preprocessing Summary

| Pipeline Stage | Records | Features |
|---------------|---------|----------|
| Raw Data | 176,419 | 42 |
| After Cleaning | 176,419 | 41 |
| After Engineering | 176,419 | 49 |
| After Correlation Removal | 176,419 | 35 |
| After Feature Selection | 176,419 | 24 |
| After SMOTE | 352,838 | 24 |

## B. Top Features

| Rank | Feature | Importance |
|------|----------|------------|
| 1 | ct_srv_src | 0.0876 |
| 2 | ct_dst_ltm | 0.0742 |
| 3 | ct_src_dport_ltm | 0.0638 |
| 4 | sload | 0.0524 |
| 5 | dload | 0.0496 |

## C. Hyperparameter Tuning Results

| Config | Estimators | Depth | Learning Rate | Mean F1 |
|----------|-----------|--------|---------------|---------|
| 1 | 100 | 6 | 0.10 | 0.9975 |
| 2 | 150 | 6 | 0.05 | 0.9961 |
| 3 | 200 | 5 | 0.05 | 0.9968 |

Configuration 1 produced the best results and was selected for deployment.

## D. Model Performance

| Metric | Value |
|----------|--------|
| Accuracy | 99.75% |
| Precision | 99.90% |
| Recall | 99.60% |
| F1-Score | 99.75% |
| ROC-AUC | 0.9980 |

## E. Confusion Matrix Analysis

| Metric | Count |
|----------|--------|
| True Negative | 13,881 |
| False Positive | 44 |
| False Negative | 20 |
| True Positive | 4,963 |

The model achieved:

- False Positive Rate: **0.31%**
- False Negative Rate: **0.40%**

# V. Conclusion

This study presents a comprehensive machine learning pipeline for network intrusion detection using the UNSW-NB15 dataset. Through preprocessing, feature engineering, SMOTE balancing, feature selection, and XGBoost optimization, the proposed approach achieved outstanding detection performance.

The results demonstrate that ensemble machine learning techniques can effectively identify cyberattacks while maintaining low false alarm rates, making them suitable for real-world intrusion detection deployments.

# References

1. Moustafa, N., & Slay, J. *UNSW-NB15: A Comprehensive Data Set for Network Intrusion Detection Systems*. 2015.
2. Khraisat, A., Gondal, I., Vamplew, P., & Kamruzzaman, J. *Survey of Intrusion Detection Systems*. 2019.
3. Moustafa, N., & Slay, J. *The Evaluation of Network Anomaly Detection Systems*. 2016.
4. Sabhnani, M., & Serpen, G. *Application of Machine Learning Algorithms to KDD Intrusion Detection Dataset*. 2003.
5. Breiman, L. *Random Forests*. 2001.
6. Chawla, N. V., et al. *SMOTE: Synthetic Minority Over-Sampling Technique*. 2002.
7. Chen, T., & Guestrin, C. *XGBoost: A Scalable Tree Boosting System*. 2016.
