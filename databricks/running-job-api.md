# Running a job from the jobs API

Databricks jobs can be used to execute notebook worflows. These can be executed either through the databricks UI or through the jobs  API. Code was developed using this stackoverflow [post](https://stackoverflow.com/questions/56153505/calling-databricks-notebook-using-databricks-job-api-runs-submit-endpoint) and the [jobs API documentation](https://docs.databricks.com/dev-tools/api/latest/jobs.html). 

Given a dictionary of data like:
```
{'0': {'sepal length (cm)': 6.3,
  'sepal width (cm)': 2.8,
  'petal length (cm)': 5.1,
  'petal width (cm)': 1.5},
 '1': {'sepal length (cm)': 5.1,
  'sepal width (cm)': 3.7,
  'petal length (cm)': 1.5,
  'petal width (cm)': 0.4}}
  ```

It is possible to iterate through the data and provide the input values as paramaters to the databricks jobs through the `job_payload`. The run executed does not show up in the databricks jobs UI, so you need to retrieve the run URL using the API too.

```
# Import libs
import numpy as np
import requests
import json
import timeit
import json

# Set paramaters
job_id = 123
run_name = 'iris_test'
existing_cluster_id = 'cluster-123'
notebook_path = 'Users/user_name/notebook/'
token = 'access_token'

# where base params instance is set in the notebook 
for instance, values in data.items():
    print(f'Instance number {instance}')
    
    # Create job_payload for instance
    job_payload = {"job_id":job_id,"run_name":run_name,
    "existing_cluster_id":existing_cluster_id,
        "notebook_task":
            {"notebook_path":notebook_path,
            "base_parameters":{"instance":f'json.dumps(values)'}}}

    # Sending data to trigger the run 
    print('   ... sending data to job')
    resp = requests.post('https://company-workspace.cloud.databricks.com/api/2.1/jobs/runs/submit', json=job_payload,
    headers={'Authorization':f'Bearer {token}'})
    status = resp.status_code 
    print(f'Job post status: {status} and job info {resp.text})

    # Getting data back from the run 
    print(f' ... getting run info ')
    resp = requests.get('https://company-workspace.cloud.databricks.com/api/2.1/jobs/runs/get-output', json=job_payload,
    headers={'Authorization':f'Bearer {token}'})
    status = resp.status_code 
    url = json.loads(resp.text)['metadata']['run_page_url']
    print(f'Job post status: {status} and run page url info {resp.text})
```

This script will then print the jobs run URL which can be used to verify the prediction made by the model.


