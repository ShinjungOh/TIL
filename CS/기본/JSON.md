# 데이터 포맷

## JSON

### JavaScript Object Notation

Javascript 객체 문법으로 구조화된 데이터를 표현하기 위한 표준 포맷  
데이터를 나타내는 포맷 중 하나   
자바스크립트와의 호환성이 좋음

<br>

```json
{
  "squadName": "Super hero squad",
  "formed": 2016,
  "active": true,
  "members": [
    {
      "name": "Eternal Flame",
      "age": 1000000,
      "secretIdentity": "Unknown",
      "powers": [
        "Immortality",
        "Heat Immunity",
        "Inferno"
      ]
    }
  ]
}
```
* 기본 데이터 타입인 문자열, 숫자, 배열, 불리언, 다른 객체, null 포함 가능

<br><br>

## 주의점

* key - value 만 담을 수 있음 
* "큰 따옴표만 사용"
* undefined 불가
* 메소드 불가

<br><br>

## 장점

* 텍스트로 구성되어, 사람과 컴퓨터 모두 읽고 쓰기 쉬움
* 프로그래밍 언어와 플랫폼에 독립적 -> 서로 다른 시스템 간 객체를 교환하기 용이 (언어가 달라도 소통 가능)
* api, config 파일에 활용
* 가벼움
