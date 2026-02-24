# 홈 배너 관리

## 배너 목록 조회

{% swagger method="get" path="/v1/admin/home/banners" baseUrl="" summary="배너 목록 조회 (관리자)" %}
{% swagger-description %}
홈 배너 목록을 조회합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "[홈 배너]가 성공적으로 조회되었습니다.",
  "data": [
    {
      "id": 1,
      "imageUrl": "https://s3.../banner1.jpg",
      "linkUrl": "https://tavesurf.site/event",
      "displayOrder": 1
    }
  ]
}
```
{% endswagger-response %}
{% endswagger %}

---

## 배너 생성

{% swagger method="post" path="/v1/admin/home/banners" baseUrl="" summary="배너 생성 (관리자)" %}
{% swagger-description %}
새로운 홈 배너를 생성합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="imageUrl" type="String" required="true" %}
배너 이미지 URL (최대 1000자)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="linkUrl" type="String" required="false" %}
배너 클릭 시 이동 URL
{% endswagger-parameter %}

{% swagger-response status="201" description="생성 성공" %}
```json
{
  "code": 201,
  "message": "[홈 배너]가 성공적으로 생성되었습니다.",
  "data": {
    "id": 2,
    "imageUrl": "https://s3.../banner2.jpg",
    "linkUrl": null,
    "displayOrder": 2
  }
}
```
{% endswagger-response %}
{% endswagger %}

---

## 배너 수정

{% swagger method="put" path="/v1/admin/home/banners/{bannerId}" baseUrl="" summary="배너 수정 (관리자)" %}
{% swagger-description %}
특정 배너를 수정합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="bannerId" type="Long" required="true" %}
배너 ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="imageUrl" type="String" required="true" %}
배너 이미지 URL
{% endswagger-parameter %}

{% swagger-parameter in="body" name="linkUrl" type="String" required="false" %}
배너 클릭 시 이동 URL
{% endswagger-parameter %}

{% swagger-response status="200" description="수정 성공" %}
```json
{
  "code": 200,
  "message": "[홈 배너]가 성공적으로 수정되었습니다.",
  "data": null
}
```
{% endswagger-response %}

{% swagger-response status="404" description="배너 없음" %}
```json
{
  "code": 404,
  "message": "존재하지 않는 [홈 배너]입니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}

---

## 배너 삭제

{% swagger method="delete" path="/v1/admin/home/banners/{bannerId}" baseUrl="" summary="배너 삭제 (관리자)" %}
{% swagger-description %}
특정 배너를 삭제합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="bannerId" type="Long" required="true" %}
배너 ID
{% endswagger-parameter %}

{% swagger-response status="204" description="삭제 성공" %}
{% endswagger-response %}
{% endswagger %}

---

## 배너 순서 변경

{% swagger method="put" path="/v1/admin/home/banners/reorder" baseUrl="" summary="배너 순서 변경 (관리자)" %}
{% swagger-description %}
배너 순서를 변경합니다. 모든 배너 ID를 원하는 순서대로 배열로 전달해야 합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="bannerIds" type="Array" required="true" %}
배너 ID 배열 (순서대로)
{% endswagger-parameter %}

{% swagger-response status="200" description="순서 변경 성공" %}
```json
{
  "code": 200,
  "message": "[홈 배너] 순서가 성공적으로 변경되었습니다.",
  "data": null
}
```
{% endswagger-response %}

{% swagger-response status="400" description="배너 목록 불일치" %}
```json
{
  "code": 400,
  "message": "모든 [홈 배너]를 입력해야 합니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}
