
# s3 접근 
```
import os
from dotenv import load_dotenv
import boto3
import json 

load_dotenv()

s3_client = boto3.client('s3')
```

## s3 file donwload 및 json 변환 
```
f = BytesIO()
s3_client.download_fileobj(os.environ.get('AWS_BUCKET'), "file_path", f)

print(json.loads(f.getvalue())) # json dumps 예시를 위해 
```

## s3 file upload 
```
try:
    s3_client.put_object(Bucket=os.environ.get('AWS_BUCKET'), Key="file_path", Body=body)
    return True
except:
    return False
```
- options
  - `Bucket` : s3 bucket name 
  - `Key` : file name or file path
  - `Body` : 업로드할 데이터 

# cloudFront 접근 
```
import os
from dotenv import load_dotenv
import boto3
import json 
import time

load_dotenv()

cf = boto3.client('cloudfront')
```

## cloudfront invalidation(무효화처리)
```
paths = [ "file path" ] 

try:
    response = cf.create_invalidation(
        DistributionId="클라우드프론트아이디",
        InvalidationBatch={
            'Paths': {
                'Quantity': len(paths),
                'Items': paths
            },
            'CallerReference': str(time.time()).replace(".", "")
        }
    )
    return True
except:

    return False
```
- 옵션 
  - `DistributionId` : 클라우드프론트 고유아이디 
  - `Quantity` : 무효화할 경로 갯수 
  - `Items` : 경로 배열 
  - `CallerReference` : 중복호출되지 않도록 고유한 값을 넣어야함 

