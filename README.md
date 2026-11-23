# Customer Churn Prediction with Amazon SageMaker

A training-and-deployment exercise from the AWS Training course **Practical Data Science with Amazon SageMaker**. The notebook follows the course lab and is shared as a learning record, not as a production system.

## What it covers

- Exploring a mobile operator's churn data (3,333 customers; UCI dataset cited in Larose, *Discovering Knowledge in Data*).
- Training XGBoost with SageMaker's built-in algorithm, data staged in S3.
- Hosting the model on a SageMaker real-time endpoint and evaluating it on a held-out test set.
- Automatic model tuning: 12 training jobs over `eta` and `min_child_weight`; best validation error 0.063.
- Choosing the decision threshold by cost rather than accuracy.

## Results (held-out test set, 334 customers)

| Cutoff | Churners caught | False alarms |
| --- | --- | --- |
| 0.5 (default) | 37 of 48 | 3 |
| 0.3 | 41 of 48 | 7 |

With the lab's assumed costs (a missed churner costs 500, an incentive costs 100), total cost is lowest at a cutoff of about 0.37. The point of the exercise: the right threshold depends on what each kind of error costs the business.

## Not included

No pipeline orchestration, Lambda functions, model monitoring or CI. Endpoints were deleted after the exercise.

## Run it

Open `xgboost_customer_churn_bootcamp_AWS.ipynb` in SageMaker Studio or a notebook instance with an execution role that can read and write an S3 bucket. Delete the endpoint afterwards to stop charges.
