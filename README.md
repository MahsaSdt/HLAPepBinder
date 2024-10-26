# HLAPepBinder
This project provides the test steps for the HLAPepBinder model, which is designed to predict HLA-peptide binding. The test script loads pre-trained models, predicts binding scores for given peptide and HLA pairs, and evaluates the performance of both the base models and HLAPepBinder.

![image](https://github.com/user-attachments/assets/7a06bb16-eccd-4d8c-bd13-6996b1546674)

## Requirements

- Python 3.x
- Required libraries:
  - `scikit-learn`
  - `joblib` (for loading and saving models)
  - `numpy` and `pandas` (for data handling and manipulation)

Install dependencies with:
```bash
pip install -r requirements.txt
```

## Steps

1. **Loading Test Data**: The code first loads a test dataset containing pairs of peptides and HLA sequences. Each pair will be processed to gather binding predictions from multiple baseline models.

2. **Loading the Pre-trained Model**: The pre-trained HLAPepBinder model is then loaded to predict HLA-peptide binding based on  the scores from base models.

3. **Generating Base Model Predictions**: For each peptide-HLA pair, the code retrieves scores from nine baseline models that are available in http://tools.iedb.org/mhci/ . These scores are essential inputs for HLAPepBinder and must be organized respectily as follows:

   - **Ann**: IC50 value
   - **Consensus**: Percentile value
   - **NetMHCpan_BA**: IC50 value
   - **NetMHCpan_EL**: Score value
   - **SMM**: IC50 value
   - **SMMPMBEC**: IC50 value
   - **PickPocket**: IC50 value
   - **NetMHCcons**: IC50 value
   - **NetMHCStabPan**: Score value

   These values should be stored for each peptide-HLA pair, creating a feature vector for prediction.

4. **Predicting with HLAPepBinder**: Once the input data is prepared, the HLAPepBinder model is used to predict the binding outcomes for the test set.

5. **Evaluating the Model**: The script then calculates evaluation metrics for each of the base models as well as HLAPepBinder. Key metrics include accuracy, precision, recall, and F1-score, offering a comparison between the base models and HLAPepBinder.


## Files

- `HLAPepBinder.py`: Main script for loading test data, generating predictions, and calculating evaluation metrics.
- `model/compressed_model.joblib`: Pre-trained HLAPepBinder model file.
- `data/test.csv`: Test dataset with peptide-HLA pairs with feature vector.
- `data/external_test.csv`: External test dataset with peptide-HLA pairswith feature vector.

## Notes

- Ensure the test data format aligns with the expected input structure.
- Model predictions depend on accurate scoring from each base model, so check that all input values are properly formatted and scaled as specified.
