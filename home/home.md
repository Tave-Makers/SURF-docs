# 홈 화면 조회

{% swagger method="get" path="/v1/user/home" baseUrl="" summary="홈 화면 데이터 렌더링" %}
{% swagger-description %}
홈 화면에 필요한 배너, 문구, 공지 등의 데이터를 조회합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "[홈 화면] 데이터가 성공적으로 조회되었습니다.",
  "data": {
    "banners": [
      {
        "id": 1,
        "imageUrl": "https://s3.../banner1.jpg",
        "linkUrl": "https://tavesurf.site/event",
        "displayOrder": 1
      }
    ],
    "mainText": "TAVE와 함께 성장하세요!",
    "recentPosts": [...]
  }
}
```
{% endswagger-response %}
{% endswagger %}
