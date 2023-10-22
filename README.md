# 📚 스프링부트 - 주식 배당금 API 서비스

## 🌟 소개
> 크롤링을 통해 주식 데이터를 가져와 배당금을 알아보는 프로젝트입니다.

## 💻 기술 스택

- Java 11
- Spring Boot 2.7.14
- Spring Boot Data JPA
- Spring Boot Security
- Jsoup
- Jwt
- H2
- Git

## 💡 주요 기능

- 야후 파이낸셜 사이트 스크래핑으로 배당금 데이터 가져오기
- 서버 부하를 줄이기 위한 캐시 서버 구성하기
- 로그인시 JWT Access Token 발행하기
- 자동 완성 기능 추가하기

## 🗂 API 명세서

### 배당금

#### 특정 회사 배당금 조회

`GET` 요청을 사용해서 특정 회사의 배당금을 조회할 수 있습니다.

##### Path parameters

> /finance/dividend/{companyName}

| Path          | Type     | Description |
|---------------|----------|-------------|
| `companyName` | `String` | 회사명         |

##### Response fields

| Path          | Type            | Description |
|---------------|-----------------|-------------|
| `companyName` | `String`        | 회사명         |
| `dividend`    | `List`          | 배당금 관련      |
| `date`        | `LocalDateTime` | 배당금 일자      |
| `price`       | `String`        | 배당금         |

##### Example response

``` http request
HTTP/1.1 200 
Content-Type: application/json
Transfer-Encoding: chunked
Date: Fri, 25 Aug 2023 11:38:57 GMT
Keep-Alive: timeout=60
Connection: keep-alive

{
  "companyName": "테스트 회사",
  "dividend": [
    {
      "date": "2023.01.01"
      "price": "2.00"
    }
  ]
}
```

#### 배당금 검색 자동완성

`GET` 요청을 사용해서 검색할 회사명을 자동완성할 수 있습니다.

##### Path parameters

> /company/autocomplete?keyword={keyword}

| Path      | Type     | Description |
|-----------|----------|-------------|
| `keyword` | `String` | 키워드         |

##### Response fields

| Path     | Type   | Description |
|----------|--------|-------------|
| `result` | `List` | 결과          |

##### Example response

``` http request
HTTP/1.1 200 
Content-Type: application/json
Transfer-Encoding: chunked
Date: Fri, 25 Aug 2023 11:38:57 GMT
Keep-Alive: timeout=60
Connection: keep-alive

{
  "result": ["O", "OAS"]
}
```

#### 회사 리스트 조회

`GET` 요청을 사용해서 회사 리스트를 조회할 수 있습니다.

##### Path parameters

> /company

##### Response fields

| Path          | Type     | Description |
|---------------|----------|-------------|
| `result`      | `List`   | 결과          |
| `companyName` | `String` | 회사명         |
| `ticker`      | `String` | 종목          |

##### Example response

``` http request
HTTP/1.1 200 
Content-Type: application/json
Transfer-Encoding: chunked
Date: Fri, 25 Aug 2023 11:38:57 GMT
Keep-Alive: timeout=60
Connection: keep-alive

{
  "result": [
    {
      "companyName": "Bitcoin",
      "ticker": "BTC"
    }
  ]
}
```

### 관리자

#### 종목 저장

`POST` 요청을 사용해서 종목을 저장할 수 있습니다.

#### Request fields

| Path     | Type     | Description |
|----------|----------|-------------|
| `ticker` | `String` | 종목          |

#### Example request

``` http request
POST http://localhost:8080/company
Content-Type: application/json

{
  "ticker": "BTC"
}
```

#### Response fields

| Path          | Type     | Description |
|---------------|----------|-------------|
| `ticker`      | `String` | 종목          |
| `companyName` | `String` | 회사명         |

#### Example response

``` http request
HTTP/1.1 200 
Content-Type: application/json
Transfer-Encoding: chunked
Date: Fri, 25 Aug 2023 11:33:34 GMT
Keep-Alive: timeout=60
Connection: keep-alive

{
  "ticker": "BTC",
  "companyName": "Bitcoin"
}
```

#### 종목 삭제

`DELETE` 요청을 사용해서 해당 종목을 삭제할 수 있습니다.

##### Path parameters

> /company?ticker={ticker}

| Path     | Type     | Description |
|----------|----------|-------------|
| `ticker` | `String` | 종목          |

#### 회원

- 회원가입
- 로그인
- 로그아웃
