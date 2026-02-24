# PreSigned URL 생성

{% swagger method="post" path="/v1/user/presigned-url" baseUrl="" summary="S3 PreSigned URL 생성" %}
{% swagger-description %}
AWS S3에 파일을 업로드하기 위한 PreSigned URL을 생성합니다. URL 유효 시간은 2분입니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fileNames" type="Array" required="true" %}
업로드할 파일명 배열 (최소 1개)
{% endswagger-parameter %}

{% swagger-response status="200" description="생성 성공" %}
```json
{
  "code": 200,
  "message": "[PreSignedUrl]을 발급했습니다.",
  "data": [
    {
      "key": "original/550e8400-e29b-41d4-a716-446655440000/profile_image.jpg",
      "preSignedUrl": "https://bucket.s3.amazonaws.com/original/550e8400.../profile_image.jpg?X-Amz-Algorithm=...",
      "originalFileName": "profile_image.jpg"
    }
  ]
}
```
{% endswagger-response %}

{% swagger-response status="404" description="파일명 없음" %}
```json
{
  "code": 404,
  "message": "건네받은 [파일명]이 없습니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}

### Request Body 예시

```json
{
  "fileNames": ["profile_image.jpg", "post_image.png"]
}
```

### 파일 업로드 방법

PreSigned URL을 받은 후 클라이언트에서 직접 S3에 업로드합니다:

```bash
curl -X PUT \
  --data-binary @"profile_image.jpg" \
  -H "Content-Type: image/jpeg" \
  "{preSignedUrl}"
```

### S3 키 구조

```
original/{UUID}/{originalFileName}
```

- 각 파일마다 고유한 UUID가 생성되어 파일명 충돌을 방지합니다
- PreSigned URL의 유효 시간은 **2분**입니다

### Response 필드

| 필드 | 타입 | 설명 |
|------|------|------|
| key | String | S3 파일 키 (경로) |
| preSignedUrl | String | 파일 업로드용 PreSigned URL |
| originalFileName | String | 원본 파일명 |
