# Matjaz-Fras---CM3070-UoL-Final-Project
# Early Twitter Cascade Emergence — Final Project (CM3070 Using the CM3005 Template, Idea #2)

This repo contains the notebook and artefacts for my final project submission: early prediction of Twitter/X thread emergence using only the first 60 minutes of activity. 

My system outputs:

* a calibrated probability a thread will “go big” (top decile) within 6 hours, and

* a forecast of 24-hour size.

It is designed to be leakage-safe and CPU-friendly.

----------

Data

Public SemEval-2017 RumourEval (PHEME) threads (reply trees, timestamps, text). No live scraping. 
--> Dataset Link: https://alt.qcri.org/semeval2017/task8/index.php?id=data-and-tools

Labels: top-decile at 6h (binary), size at 24h (regression).


----------

Methods (Brief Rundown)

Features (≤60m): TF-IDF→SVD(300D) + sentiment aggregates; temporal rates/acceleration/burst/entropy; early reply-graph stats (depth/frontier/degree).

Classification: Logistic Regression, Random Forest, XGBoost → sigmoid calibration → OOF threshold selection.

Forecasting: Naïve → ETS (damped) → SARIMAX(exog) (first-hour cues) → compact LSTM (60×3: count, cumulative, diff).

Metrics: macro-F1 (primary), ROC-AUC, log-loss, Brier, accuracy; MAE/RMSE/NRMSE/sMAPE; latency on CPU.

Headline TEST results: RF macro-F1 ≈ 0.883 (log-loss 0.169; Brier 0.046; ~3 ms/sample).
LSTM: MAE 8.88, RMSE 19.16, NRMSE 0.857, sMAPE 0.406; SARIMAX(exog) is a strong lightweight baseline.

----------

Note 1: Alongside my main Final Code Jupyter Notebook (CM3070_FinalCode_UoL_matjazfras_FINALISED), I also included my initial Feature Protoype ( (Extra) CM3070_Feature_prototype_UoL_matjazfras_FINALISED) for the sake of completeness. Only look at my Final Code Notebook when you mark however.

----------

Thank you so much for reading! :)


