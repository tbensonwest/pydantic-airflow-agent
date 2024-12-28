# Pydantic Airflow Agent

## Description

This project provides a way to seamlessly integrate Pydantic models into your Apache Airflow workflows. By leveraging Pydantic's data validation and serialization capabilities, this agent simplifies the process of defining and validating data used in your Airflow DAGs, ensuring data quality and reducing errors.

## Installation

To install and run this project, you will need to have Python and Poetry installed.

1. Clone the repository:
   ```bash
   git clone https://github.com/tbizzlewiz/pydantic-airflow-agent
   cd pydantic-airflow-agent
   ```

2. Install the project dependencies using Poetry:
   ```bash
   poetry install
   ```

## Usage

Here's an example of how to use the Pydantic Airflow Agent in your Airflow DAGs:

```python
from airflow import DAG
from airflow.operators.python import PythonOperator
from datetime import datetime
from pydantic import BaseModel

class MyConfig(BaseModel):
    param1: str
    param2: int

def my_task(config: MyConfig):
    print(f"Parameter 1: {config.param1}")
    print(f"Parameter 2: {config.param2}")

with DAG(
    dag_id="pydantic_example",
    start_date=datetime(2023, 1, 1),
    schedule_interval=None,
    catchup=False,
) as dag:
    run_my_task = PythonOperator(
        task_id="run_my_task",
        python_callable=my_task,
        op_kwargs={"config": MyConfig(param1="hello", param2=123)}
    )
```

In this example, `MyConfig` is a Pydantic model that defines the expected parameters for the `my_task` function. The `PythonOperator` automatically validates the `op_kwargs` against the `MyConfig` model.

## Contributing

Contributions to this project are welcome. Please follow these steps:

1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Make your changes and ensure they pass all tests.
4. Submit a pull request.

## License

[Specify the project license here, e.g., MIT License]. Consider adding a license file to the repository.
