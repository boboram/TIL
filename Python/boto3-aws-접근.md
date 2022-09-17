
# [s3 접근](https://velog.io/@bona/Python-boto3-s3)

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

