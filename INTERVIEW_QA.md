# mlops-zoomcamp — interview questions and answers

[README](README.md) · [Project architecture](PROJECT_ARCHITECTURE.md)

Answers below use this repository’s files and implementation. They distinguish existing behavior from suggested extensions; source links let you verify each walkthrough.

## 1. What problem does mlops-zoomcamp address, and what can you demonstrate?

Course materials and exercises for productionizing machine learning services through training, deployment, orchestration, and monitoring.

I would demonstrate the linked implementation or examples and distinguish that evidence from any planned production features. Start with [`README.md`](README.md).

## 2. How is this repository organized?

- [`04-deployment/web-service-mlflow/predict.py`](04-deployment/web-service-mlflow/predict.py): Implementation or supporting configuration.
- [`04-deployment/web-service/predict.py`](04-deployment/web-service/predict.py): Implementation or supporting configuration.
- [`cohorts/2022/05-monitoring/homework/prediction_service/app.py`](cohorts/2022/05-monitoring/homework/prediction_service/app.py): Implementation or supporting configuration.
- [`cohorts/2023/03-orchestration/prefect/3.5/orchestrate_s3.py`](cohorts/2023/03-orchestration/prefect/3.5/orchestrate_s3.py): Implementation or supporting configuration.
- [`cohorts/2023/03-orchestration/prefect/3.6/orchestrate_s3.py`](cohorts/2023/03-orchestration/prefect/3.6/orchestrate_s3.py): Implementation or supporting configuration.
- [`cohorts/2023/02-experiment-tracking/homework-wandb/preprocess_data.py`](cohorts/2023/02-experiment-tracking/homework-wandb/preprocess_data.py): Implementation or supporting configuration.
- [`cohorts/2023/03-orchestration/prefect/3.3/orchestrate.py`](cohorts/2023/03-orchestration/prefect/3.3/orchestrate.py): Implementation or supporting configuration.
- [`cohorts/2023/03-orchestration/prefect/3.3/orchestrate_pre_prefect.py`](cohorts/2023/03-orchestration/prefect/3.3/orchestrate_pre_prefect.py): Implementation or supporting configuration.

[PROJECT_ARCHITECTURE.md](PROJECT_ARCHITECTURE.md) contains the component diagram and the implementation walkthrough.

## 3. Can you walk through `train_best_model` and explain the decision it makes?

The main walkthrough here is `train_best_model(X_train: scipy.sparse._csr.csr_matrix, X_val: scipy.sparse._csr.csr_matrix, y_train: np.ndarray, y_val: np.ndarray, dv: sklearn.feature_extraction.DictVectorizer)` in [`cohorts/2023/03-orchestration/prefect/3.5/orchestrate_s3.py`](cohorts/2023/03-orchestration/prefect/3.5/orchestrate_s3.py#L69). train a model with best hyperparams and write everything out

```python
def train_best_model(
    X_train: scipy.sparse._csr.csr_matrix,
    X_val: scipy.sparse._csr.csr_matrix,
    y_train: np.ndarray,
    y_val: np.ndarray,
    dv: sklearn.feature_extraction.DictVectorizer,
) -> None:
    """train a model with best hyperparams and write everything out"""

    with mlflow.start_run():
        train = xgb.DMatrix(X_train, label=y_train)
        valid = xgb.DMatrix(X_val, label=y_val)

        best_params = {
            "learning_rate": 0.09585355369315604,
            "max_depth": 30,
            "min_child_weight": 1.060597050922164,
            "objective": "reg:linear",
            "reg_alpha": 0.018060244040060163,
            "reg_lambda": 0.011658731377413597,
```

This is an excerpt; follow the source link for the rest of the branches.

The implementation calls `booster.predict`, `create_markdown_artifact`, `date.today`, `mean_squared_error`, `mlflow.log_artifact`, `mlflow.log_metric`, `mlflow.log_params`, `mlflow.start_run`, `mlflow.xgboost.log_model`. In an interview, trace those calls in execution order using a fixture input.

## 4. What responsibility does `train_best_model` have?

`train_best_model(X_train: scipy.sparse._csr.csr_matrix, X_val: scipy.sparse._csr.csr_matrix, y_train: np.ndarray, y_val: np.ndarray, dv: sklearn.feature_extraction.DictVectorizer)` is defined in [`cohorts/2023/03-orchestration/prefect/3.6/orchestrate_s3.py`](cohorts/2023/03-orchestration/prefect/3.6/orchestrate_s3.py#L69). train a model with best hyperparams and write everything out

Its return expressions include:

- `None`

It uses `booster.predict`, `create_markdown_artifact`, `date.today`, `mean_squared_error`, `mlflow.log_artifact`, `mlflow.log_metric`, `mlflow.log_params`, `mlflow.start_run`. This is the code path I would compare against the caller to explain responsibility boundaries.

## 5. What input validation and failure behavior are implemented?

Explicit failure paths include:

- `Exception()` in [`cohorts/2023/03-orchestration/prefect/3.2/cat_facts.py`](cohorts/2023/03-orchestration/prefect/3.2/cat_facts.py#L10).

I would test both the condition that reaches each exception and the caller that translates it. An explicit raise does not mean every malformed input or dependency failure is handled.

## 6. Which files provide verification evidence?

The repository includes [`04-deployment/streaming/test_docker.py`](04-deployment/streaming/test_docker.py), [`06-best-practices/code/integration-test/test_docker.py`](06-best-practices/code/integration-test/test_docker.py), [`06-best-practices/code/integration-test/test_kinesis.py`](06-best-practices/code/integration-test/test_kinesis.py), [`06-best-practices/code/scripts/test_cloud_e2e.sh`](06-best-practices/code/scripts/test_cloud_e2e.sh), [`06-best-practices/code/tests/__init__.py`](06-best-practices/code/tests/__init__.py). I would explain the scenarios and assertions in these files, then run the matching test command from the appropriate project directory. File presence alone is not a passing test result.

## 7. What HTTP interface does the code expose?

- `ROUTE /predict` → `predict_endpoint` in [`04-deployment/web-service-mlflow/predict.py`](04-deployment/web-service-mlflow/predict.py#L31).
- `ROUTE /predict` → `predict_endpoint` in [`04-deployment/web-service/predict.py`](04-deployment/web-service/predict.py#L26).
- `ROUTE /` → `get_info` in [`cohorts/2022/05-monitoring/homework/prediction_service/app.py`](cohorts/2022/05-monitoring/homework/prediction_service/app.py#L49).
- `ROUTE /predict-duration` → `predict_duration` in [`cohorts/2022/05-monitoring/homework/prediction_service/app.py`](cohorts/2022/05-monitoring/homework/prediction_service/app.py#L66).

These are literal decorators. Application/router prefixes, authentication, and middleware must be checked in the corresponding setup code.

## 8. Where does state live, and what happens with multiple workers?

Module-level containers include `num_features`, `cat_features` in [`05-monitoring/evidently_metrics_calculation.py`](05-monitoring/evidently_metrics_calculation.py); `num_features`, `cat_features` in [`05-monitoring/post-evidently-0.7/evidently_metrics_calculation.py`](05-monitoring/post-evidently-0.7/evidently_metrics_calculation.py); `SPACE` in [`cohorts/2022/02-experiment-tracking/homework/register_model.py`](cohorts/2022/02-experiment-tracking/homework/register_model.py); `categorical` in [`cohorts/2022/04-deployment/homework/batch.py`](cohorts/2022/04-deployment/homework/batch.py).

These containers belong to a Python process. Inspect which are constant fixtures and which are mutated. Mutable process state needs an explicit shared-storage or synchronization strategy before multiple workers can provide consistent behavior.

## 9. How would another engineer reproduce your walkthrough?

Start from the repository root:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r 02-experiment-tracking/requirements.txt
```

These commands follow repository manifests; environment setup and command results still need to be checked on the target machine.

## 10. What does automation verify, and what does it not prove?

Inspect [`.github/workflows/cd-deploy.yml`](.github/workflows/cd-deploy.yml), [`.github/workflows/ci-tests.yml`](.github/workflows/ci-tests.yml) for triggers, permissions, and job commands. I would name the checks that those definitions run and show the latest run separately. A workflow definition alone does not establish a successful deployment, security review, or production SLO.

## 11. How would you present this project in a Forward Deployed Engineer interview?

Start with the user and operational problem described in [`README.md`](README.md). Explain one constraint that changes the implementation, show the linked code or example, and walk through a success case and a failure case. Agree on a measurable acceptance criterion before expanding the solution, and leave a handoff with data boundaries and rollback ownership. Any proposed production or business metric should be identified as a target until measured.

## 12. What is the input-to-output contract of `train_best_model`?

In [`cohorts/2023/03-orchestration/prefect/3.5/orchestrate_s3.py`](cohorts/2023/03-orchestration/prefect/3.5/orchestrate_s3.py#L69), `train_best_model(X_train: scipy.sparse._csr.csr_matrix, X_val: scipy.sparse._csr.csr_matrix, y_train: np.ndarray, y_val: np.ndarray, dv: sklearn.feature_extraction.DictVectorizer)` receives the inputs. The function computes these intermediate values:

The implementation delegates or iterates directly; trace the calls in the source walkthrough.

Its result is defined by:

- `None`

## 13. Which Terraform modules compose the environment?

- `module.source_kinesis_stream` uses `./modules/kinesis` in [`06-best-practices/code/infrastructure/main.tf`](06-best-practices/code/infrastructure/main.tf).
- `module.output_kinesis_stream` uses `./modules/kinesis` in [`06-best-practices/code/infrastructure/main.tf`](06-best-practices/code/infrastructure/main.tf).
- `module.s3_bucket` uses `./modules/s3` in [`06-best-practices/code/infrastructure/main.tf`](06-best-practices/code/infrastructure/main.tf).
- `module.ecr_image` uses `./modules/ecr` in [`06-best-practices/code/infrastructure/main.tf`](06-best-practices/code/infrastructure/main.tf).
- `module.lambda_function` uses `./modules/lambda` in [`06-best-practices/code/infrastructure/main.tf`](06-best-practices/code/infrastructure/main.tf).

Review each module’s variable and output contracts. Different environment declarations may reuse a module with different inputs; state and provider configuration determine the actual deployment boundary.
