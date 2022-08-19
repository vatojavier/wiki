# Machine Learning

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
