# MLOps Zoomcamp

<!-- project-guide:start -->
## Project guide

[Project architecture](PROJECT_ARCHITECTURE.md) · [Interview questions and answers](INTERVIEW_QA.md)

Use the architecture document for the component diagram, implementation boundaries, and verification entry points. The interview guide includes source-backed answers and project walkthroughs.

### Implementation map

| Component | Responsibility |
| --- | --- |
| [`04-deployment/web-service-mlflow/predict.py`](04-deployment/web-service-mlflow/predict.py) | HTTP handlers: `ROUTE /predict` |
| [`04-deployment/web-service/predict.py`](04-deployment/web-service/predict.py) | HTTP handlers: `ROUTE /predict` |
| [`cohorts/2022/05-monitoring/homework/prediction_service/app.py`](cohorts/2022/05-monitoring/homework/prediction_service/app.py) | HTTP handlers: `ROUTE /`, `ROUTE /predict-duration` |
| [`cohorts/2023/03-orchestration/prefect/3.5/orchestrate_s3.py`](cohorts/2023/03-orchestration/prefect/3.5/orchestrate_s3.py) | Functions: `read_data`, `add_features`, `train_best_model`, `main_flow_s3` |
| [`cohorts/2023/03-orchestration/prefect/3.6/orchestrate_s3.py`](cohorts/2023/03-orchestration/prefect/3.6/orchestrate_s3.py) | Functions: `read_data`, `add_features`, `train_best_model`, `main_flow_s3` |
| [`cohorts/2023/02-experiment-tracking/homework-wandb/preprocess_data.py`](cohorts/2023/02-experiment-tracking/homework-wandb/preprocess_data.py) | Functions: `dump_pickle`, `read_dataframe`, `preprocess`, `run_data_prep` |
| [`cohorts/2023/03-orchestration/prefect/3.3/orchestrate.py`](cohorts/2023/03-orchestration/prefect/3.3/orchestrate.py) | Functions: `read_data`, `add_features`, `train_best_model`, `main_flow` |
| [`cohorts/2023/03-orchestration/prefect/3.3/orchestrate_pre_prefect.py`](cohorts/2023/03-orchestration/prefect/3.3/orchestrate_pre_prefect.py) | Functions: `read_data`, `add_features`, `train_best_model`, `main_flow` |
| [`cohorts/2023/03-orchestration/prefect/3.4/orchestrate.py`](cohorts/2023/03-orchestration/prefect/3.4/orchestrate.py) | Functions: `read_data`, `add_features`, `train_best_model`, `main_flow` |
| [`02-experiment-tracking/requirements.txt`](02-experiment-tracking/requirements.txt) | Implementation or supporting configuration |
| [`05-monitoring/requirements.txt`](05-monitoring/requirements.txt) | Implementation or supporting configuration |
| [`06-best-practices/code/infrastructure/main.tf`](06-best-practices/code/infrastructure/main.tf) | Terraform resource/module declarations |
| [`06-best-practices/code/infrastructure/modules/ecr/main.tf`](06-best-practices/code/infrastructure/modules/ecr/main.tf) | Terraform resource/module declarations |
| [`06-best-practices/code/infrastructure/modules/ecr/variables.tf`](06-best-practices/code/infrastructure/modules/ecr/variables.tf) | Terraform resource/module declarations |
| [`06-best-practices/code/infrastructure/modules/kinesis/main.tf`](06-best-practices/code/infrastructure/modules/kinesis/main.tf) | Terraform resource/module declarations |
| [`06-best-practices/code/infrastructure/modules/kinesis/variables.tf`](06-best-practices/code/infrastructure/modules/kinesis/variables.tf) | Terraform resource/module declarations |
| [`05-monitoring/dummy_metrics_calculation.py`](05-monitoring/dummy_metrics_calculation.py) | Functions: `prep_db`, `calculate_dummy_metrics_postgresql`, `main` |
| [`05-monitoring/evidently_metrics_calculation.py`](05-monitoring/evidently_metrics_calculation.py) | Functions: `prep_db`, `calculate_metrics_postgresql`, `batch_monitoring_backfill` |
| [`03-orchestration/code/duration-prediction.py`](03-orchestration/code/duration-prediction.py) | Functions: `read_dataframe`, `create_X`, `train_model`, `run` |
| [`04-deployment/batch/score.py`](04-deployment/batch/score.py) | Functions: `generate_uuids`, `read_dataframe`, `prepare_dictionaries`, `load_model`, `save_results`, `apply_model`, `get_paths` |
| [`04-deployment/batch/score_backfill.py`](04-deployment/batch/score_backfill.py) | Functions: `ride_duration_prediction_backfill` |
| [`04-deployment/batch/score_deploy.py`](04-deployment/batch/score_deploy.py) | Implementation or supporting configuration |

### Local setup and verification

From the repository root (the commands follow the checked-in manifests):

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r 02-experiment-tracking/requirements.txt
```

<!-- project-guide:end -->

<!-- repository-summary -->
Course materials and exercises for productionizing machine learning services through training, deployment, orchestration, and monitoring.
<!-- /repository-summary -->

<p align="center">
  <img width="80%" src="images/banner-2025.jpg" alt="MLOps Zoomcamp">
</p>

<h1 align="center">
    <strong>MLOps Zoomcamp: A Free 9-Week Course on Productionizing ML Services</strong>
</h1>

<p align="center">
MLOps (machine learning operations) is a must-know skill for many data professionals. Master the fundamentals of MLOps, from training and experimentation to deployment and monitoring.
</p>

<p align="center">
<a href="https://airtable.com/shrCb8y6eTbPKwSTL"><img src="https://user-images.githubusercontent.com/875246/185755203-17945fd1-6b64-46f2-8377-1011dcb1a444.png" height="50" /></a>
</p>

<p align="center">
<a href="https://datatalks.club/slack.html">Join Slack</a> •
<a href="https://app.slack.com/client/T01ATQK62F8/C01FABYF2RG">#course-mlops-zoomcamp Channel</a> •
<a href="https://t.me/dtc_courses">Telegram Announcements</a> •
<a href="https://www.youtube.com/playlist?list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK">Course Playlist</a> •
<a href="https://datatalks.club/faq/mlops-zoomcamp.html">FAQ</a> •
<a href="https://ctt.ac/fH67W">Tweet about the Course</a>
</p>

## How to Take MLOps Zoomcamp

### 2026 Cohort

* We don't plan to offer the course in 2026
* You can still take it self-paced
* [**Register Here**](https://airtable.com/shrCb8y6eTbPKwSTL) if you want to receive updates if we decide to run the course

### Self-Paced Learning
All course materials are freely available for independent study. Follow these steps:
1. Watch the course videos.
2. Join the [Slack community](https://datatalks.club/slack.html).
3. Refer to the [FAQ document](https://datatalks.club/faq/mlops-zoomcamp.html) for guidance.

## Syllabus
The course consists of structured modules, hands-on workshops, and a final project to reinforce your learning. Each module introduces core MLOps concepts and tools.

### Prerequisites
To get the most out of this course, you should have prior experience with:
- Python
- Docker
- Command line basics
- Machine learning (e.g., through [ML Zoomcamp](https://github.com/alexeygrigorev/mlbookcamp-code/tree/master/course-zoomcamp))
- 1+ year of programming experience

## Modules

### [Module 1: Introduction](01-intro)
- What is MLOps?
- MLOps maturity model
- NY Taxi dataset (our running example)
- Why MLOps is essential
- Course structure & environment setup
- Homework

### [Module 2: Experiment Tracking & Model Management](02-experiment-tracking)
- Introduction to experiment tracking
- MLflow basics
- Model saving and loading
- Model registry
- Hands-on MLflow exercises
- Homework

### [Module 3: Orchestration & ML Pipelines](03-orchestration)

- Workflow orchestration
- Homework

### [Module 4: Model Deployment](04-deployment)
- Deployment strategies: online (web, streaming) vs. offline (batch)
- Deploying with Flask (web service)
- Streaming deployment with AWS Kinesis & Lambda
- Batch scoring for offline processing
- Homework

### [Module 5: Model Monitoring](05-monitoring)
- Monitoring ML-based services
- Web service monitoring with Prometheus, Evidently, and Grafana
- Batch job monitoring with Prefect, MongoDB, and Evidently
- Homework

### [Module 6: Best Practices](06-best-practices)
- Unit and integration testing
- Linting, formatting, and pre-commit hooks
- CI/CD with GitHub Actions
- Infrastructure as Code (Terraform)
- Homework

### [Final Project](07-project/)
- End-to-end project integrating all course concepts

## Community & Support

### Getting Help on Slack

Join the [`#course-mlops-zoomcamp`](https://app.slack.com/client/T01ATQK62F8/C02R98X7DS9) channel on [DataTalks.Club Slack](https://datatalks.club/slack.html) for discussions, troubleshooting, and networking.

To keep discussions organized:
- Follow [our guidelines](asking-questions.md) when posting questions.
- Review the [community guidelines](https://datatalks.club/slack/guidelines.html).

## Instructors

- [Cristian Martinez](https://www.linkedin.com/in/cristian-javier-martinez-09bb7031/)
- [Alexey Grigorev](https://www.linkedin.com/in/agrigorev/)
- [Emeli Dral](https://www.linkedin.com/in/emelidral/)


## Sponsors & Supporters

Interested in supporting our community? Reach out to [alexey@datatalks.club](mailto:alexey@datatalks.club).

## About DataTalks.Club

<p align="center">
  <img width="40%" src="https://github.com/user-attachments/assets/1243a44a-84c8-458d-9439-aaf6f3a32d89" alt="DataTalks.Club">
</p>

<p align="center">
<a href="https://datatalks.club/">DataTalks.Club</a> is a global online community of data enthusiasts. It's a place to discuss data, learn, share knowledge, ask and answer questions, and support each other.
</p>

<p align="center">
<a href="https://datatalks.club/">Website</a> •
<a href="https://datatalks.club/slack.html">Join Slack Community</a> •
<a href="https://us19.campaign-archive.com/home/?u=0d7822ab98152f5afc118c176&id=97178021aa">Newsletter</a> •
<a href="http://lu.ma/dtc-events">Upcoming Events</a> •
<a href="https://www.youtube.com/@DataTalksClub/featured">YouTube</a> •
<a href="https://github.com/DataTalksClub">GitHub</a> •
<a href="https://www.linkedin.com/company/datatalks-club/">LinkedIn</a> •
<a href="https://twitter.com/DataTalksClub">Twitter</a>
</p>

All the activity at DataTalks.Club mainly happens on [Slack](https://datatalks.club/slack.html). We post updates there and discuss different aspects of data, career questions, and more.

At DataTalksClub, we organize online events, community activities, and free courses. You can learn more about what we do at [DataTalksClub Community Navigation](https://www.notion.so/DataTalksClub-Community-Navigation-bf070ad27ba44bf6bbc9222082f0e5a8?pvs=21).

## Documentation checks

Project architecture, interview guides, and local source links are checked automatically on pushes and pull requests. Run the same check locally:

```bash
python3 .github/scripts/validate_project_docs.py
```
