Cloud Bowl Sample - Python
---------------------------------

To make changes, edit the `main.py` file.

It's recommended to run everything in a virtual environment. You can find a
guide how to set this up [here](https://docs.python.org/3/library/venv.html)

Run Locally (Dev):

```python
pip install -r requirements.txt
python3 main.py
```

Deploy to Cloud Run:

[![Run on Google Cloud](https://deploy.cloud.run/button.svg)](https://deploy.cloud.run)


**Deploy Microservice on Cloud Run**
--------------------------------------
gcloud run deploy $SAMPLE-bot \
  --project=$PROJECT_ID \
  --region=$REGION \
  --allow-unauthenticated \
  --source=.
  
  **Verify the microservice**
  -------------------------------
  export SVC_URL=$(gcloud run services describe $SAMPLE-bot \
  --project=$PROJECT_ID \
  --platform=managed \
  --region=$REGION \
  --format="value(status.url)")


curl -d '{
  "_links": {
    "self": {
      "href": "https://foo.com"
    }
  },
  "arena": {
    "dims": [4,3],
    "state": {
      "https://foo.com": {
        "x": 0,
        "y": 0,
        "direction": "N",
        "wasHit": false,
        "score": 0
      }
    }
  }
}' -H "Content-Type: application/json" -X POST -w "\n" \
  $SVC_URL
