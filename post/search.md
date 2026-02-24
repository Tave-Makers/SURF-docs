# 게시글 검색

## 게시글 검색

{% swagger method="get" path="/v1/user/search/posts" baseUrl="" summary="게시글 검색" %}
{% swagger-description %}
게시글을 제목과 본문 기준으로 검색합니다. 최근 검색어가 자동으로 저장됩니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="query" name="param" type="String" required="true" %}
검색어
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="Integer" required="false" %}
페이지 번호 (기본값: 0)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="size" type="Integer" required="false" %}
페이지 크기 (기본값: 20)
{% endswagger-parameter %}

{% swagger-response status="200" description="검색 성공" %}
```json
{
  "code": 200,
  "message": "검색이 성공적으로 완료되었습니다.",
  "data": {
    "content": [
      {
        "postId": 5,
        "title": "검색된 게시글",
        "content": "검색어가 포함된 내용...",
        "pinned": false,
        "postedAt": "2025-10-03T10:00:00",
        "thumbnailImageUrl": "https://s3.../thumb.jpg",
        "boardId": 1,
        "categoryId": 2,
        "scrappedByMe": false,
        "scrapCount": 3,
        "likedByMe": false,
        "likeCount": 2,
        "commentCount": 1,
        "nickname": "사용자",
        "isReserved": false,
        "viewCount": 45
      }
    ],
    "hasNext": false
  }
}
```
{% endswagger-response %}

{% swagger-response status="400" description="검색어 누락" %}
```json
{
  "code": 400,
  "message": "검색어를 입력해주세요",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}

---

## 최근 검색어 조회

{% swagger method="get" path="/v1/user/search/recent" baseUrl="" summary="최근 검색어 10개 조회" %}
{% swagger-description %}
현재 사용자의 최근 검색어 10개를 조회합니다 (최신순).
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "최근 검색어 목록이 성공적으로 조회되었습니다.",
  "data": ["검색어1", "검색어2", "검색어3"]
}
```
{% endswagger-response %}
{% endswagger %}

---

## 최근 검색어 전체 삭제

{% swagger method="delete" path="/v1/user/search/recent" baseUrl="" summary="최근 검색어 전체 삭제" %}
{% swagger-description %}
현재 사용자의 모든 최근 검색어를 삭제합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-response status="204" description="삭제 성공" %}
```json
{
  "code": 204,
  "message": "최근 검색어가 성공적으로 삭제되었습니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}

---

## 최근 검색어 단건 삭제

{% swagger method="delete" path="/v1/user/search/recent/{keyword}" baseUrl="" summary="최근 검색어 단건 삭제" %}
{% swagger-description %}
특정 최근 검색어 하나를 삭제합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="keyword" type="String" required="true" %}
삭제할 검색어
{% endswagger-parameter %}

{% swagger-response status="204" description="삭제 성공" %}
```json
{
  "code": 204,
  "message": "최근 검색어 한 개가 성공적으로 삭제되었습니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}
