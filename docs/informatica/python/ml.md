# Machine Learning

## Time Series splits
Example of 5 splits, each one with a train and test sets (test set size limited)
```python
from sklearn.model_selection import TimeSeriesSplit

test_size = int(0.05*len(X))

max_train_size = 300

ts_cv = TimeSeriesSplit(
    n_splits=5,
    gap=2,
    # max_train_size=max_train_size,
    test_size=test_size,
)
all_splits = list(ts_cv.split(X, y))
```

### Cross validation for model performance
```python
cv_results = cross_validate(
    model,
    X,
    y,
    cv=all_splits, # or the splitter
    scoring=["neg_mean_absolute_error", "neg_root_mean_squared_error", "r2"],
    return_estimator=True
)
mae = -cv_results["test_neg_mean_absolute_error"]
rmse = -cv_results["test_neg_root_mean_squared_error"]
r2 = cv_results["test_r2"]

print(
    f"CV performance: \n"
    f"Mean Absolute Error:     {mae.mean():.3f} +/- {mae.std():.3f}\n"
    f"Root Mean Squared Error: {rmse.mean():.3f} +/- {rmse.std():.3f}\n"
    f"R2: {r2.mean():.3f} +/- {r2.std():.3f}\n"
)
```

### Visualize the predictions for that cross validation
The average score of the model for this method should be the same as the cross_validate

```python
def plot_predictions(model, X, y, splits, fit=True, normalize=False, good_r2=0.2):
    
    # Each split has a Train and Test set
    for idx, split in enumerate(splits):
        train, test = split
        
        if fit is True:
            model.fit(X.iloc[train], y.iloc[train])
            
        model_preds = model.predict(X.iloc[test])
        
        df_test_true_pred = y.iloc[test].to_frame()
        df_test_true_pred["preds"] = [p for p in model_preds]
        
        # escalating values
        if normalize is True:
            df_test_true_pred["preds"] = df_test_true_pred["preds"] / y.max()
            df_test_true_pred["revenue"] = df_test_true_pred["revenue"] / y.max()

        
        mae = mean_absolute_error(df_test_true_pred["revenue"], df_test_true_pred["preds"])
        rmse = mean_squared_error(df_test_true_pred["revenue"], df_test_true_pred["preds"])
        r2 = r2_score( df_test_true_pred["revenue"],  df_test_true_pred["preds"])

        if r2 < good_r2:
            print(f"❗Low r2 for split {idx}")
        
        print(
            f"For this split {idx}\n"
            f"MAE: {mae:.3f}\n"
            f"RMSE: {rmse:.3f}\n"
            f"R2: {r2:.3f}"
            )
        
        fig = px.line(df_test_true_pred, title=f"Predictions for test set {idx}")
        fig.show()

    if fit:
        return model
```

## Pipelines for column transformation
Apply functions to columns so it will be handled better by the model

```python
categorical_columns = [
    "season", 
    "is_covid"
]
categories = [
    ["spring", "summer", "autumn", "winter"],
    [False, True]
]

# Ordinal encoder will create new columns with 0,1 values 
ordinal_encoder = OrdinalEncoder(categories=categories)

xgb_pipeline = make_pipeline(
    ColumnTransformer(
        transformers=[
            ("categorical", ordinal_encoder, categorical_columns),
        ],
        remainder="passthrough",
        verbose_feature_names_out=False
    ),
    xgb.XGBRegressor() # The model
)
```

### Applying the pipeline transformers to the data matrix
So it is easyly accesible to the the transformer data passed to the model.

```python
scaled_values = xgb_pipeline.named_steps["columntransformer"].fit_transform(X)
transformed_columns = xgb_pipeline.named_steps["columntransformer"].get_feature_names_out()
X_transformed = pd.DataFrame(scaled_values, X_new.index, columns=transformed_columns)
```

## XGBoost
```python
# XGBoost param search
params = { 'max_depth': [3, 5, 6, 10, 15, 20],
           'learning_rate': [0.01, 0.1, 0.2, 0.3],
           'subsample': np.arange(0.5, 1.0, 0.1),
           'colsample_bytree': np.arange(0.4, 1.0, 0.1),
           'colsample_bylevel': np.arange(0.4, 1.0, 0.1),
           'n_estimators': [100, 500, 1000]
        }

# Try RandomizedSearchCV for shorter computing times
clf = GridSearchCV(estimator=xgb.XGBRegressor(), 
                    param_grid=params,
                    scoring='neg_mean_squared_error', 
                    verbose=1,
                    cv=all_splits
                 )
 
clf.fit(X.values, y)
print("Best parameters:", clf.best_params_)
print("Lowest RMSE: ", (-clf.best_score_)**(1/2.0))
```

## Shap
Machine Learning explainability
### Shap with XGBoost
```python
xgb_model = xgb_model.fit(X_transformed.values, y) # Don't use a pipeline! first transform the data matrix

explainer = shap.TreeExplainer(xgb_model)
shap_values = explainer.shap_values(X_transformed[0:].values) # computing all shap values of the data (only useful if you gonna use them all)

# The API is a bit crappy and the plots are very tiquismiquis
def show_waterfall_plot_for(index, max_features=20):

    shap_object = ShapObject(base_value=explainer.expected_value, # Baseline value
                            values=explainer.shap_values(X_transformed.iloc[index:index+1].values)[0],
                            feature_names=X_transformed.columns,
                            data=X_transformed.iloc[index] # The feature values for this observation
                            )

    shap.waterfall_plot(shap_object, max_display=max_features)
    return shap_object

# a very sunny day
shap_obj = show_waterfall_plot_for(585);
shap.force_plot(explainer.expected_value, shap_obj.values, features=X_transformed.iloc[585])
```

