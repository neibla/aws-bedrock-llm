## Basic example of using AWS Bedrock with boto3

Requirements:
```sh
python -m pip install boto3==1.28.60 
```

Example usage: 
```python
import boto3
import json

client = boto3.client('bedrock-runtime')

message = "What is your purpose?"

prompt = f"Human: {message}\\nAssistant:"
args = {
  "prompt": prompt,
  "max_tokens_to_sample": 212,
  "temperature": 0,
  "top_k": 250,
  "top_p": 0.999,
  "stop_sequences": ["\\n\\nHuman:"],
  "anthropic_version": "bedrock-2023-05-31"
}

payload = {
  "modelId": "anthropic.claude-v2",
  "contentType": "application/json",
  "accept": "*/*",
  "body": json.dumps(args)
}

response = client.invoke_model(**payload)

body = response.get("body").read().decode('utf-8') 
content = json.loads(body)["completion"]

print(content)
```

