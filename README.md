Objective — predict freight/load posted rates.
Dataset — 48,000 development observations, future validation set.
Data cleaning —
  1. Removed 292 negative-weight observations.
  2. Retained missing values and handled them through median     imputation.

EDA —
    1. Distance had a strong relationship with posted rate.
    2. Target was right-skewed.
    3. Equipment categories showed different average rates.

Validation —
    1. Jan–Sep → training
    2. October → chronological validation

Models tested —
       Model                        MAE                     RMSE
    Median baseline               1146.98                  1569.05
    HistGradientBoosting          132.01                   655.93
    HistGradientBoosting +route   133.87                   657.41
    CatBoost                      135.69                   654.15

Final model: HistGradientBoosting.
Final prediction files: 12,000 validation predictions + 31 December scenario predictions.
Scorer: passed all structural checks.

## How to run

### 1. Clone the repository

```bash
git clone <your-github-repository-url>
cd Freight_rate_prediction

### 2. create a virtual environment
python -m venv venv

### 3. Activate the Environment
venv\Scripts\activate

### 4. install dependencies
pip install -r requirements.txt

### 5. Run the notebook
   open jupyter notebook
   open the file notebooks/01_eda.ipynb

###6. generate the predictions
     files generated should be
     result/validation_predicition.csv
     result/december_prediction.csv

###7. validate the predictions
  run
  python score.py --predictions result/validation_predictions.csv --december-predictions result/december_predictions.csv --output-dir scorer_results