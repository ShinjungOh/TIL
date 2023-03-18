# 웹브라우저 캐시

## 로컬스토리지 이용 예시

1. 로그인 유지 
   * 세션 기반 방식
   * 토큰 기반 방식 - 토큰을 로컬 스토리지에 저장하고 서버에 전달해서 로그인 유지  
2. 캐싱 
   * 브라우저에 입력한 값, 설정값을 담아두고 자동완성에 활용 (UX 개선)  

<br><br>

## 로컬스토리지를 활용한 UX 개선

> 📌 UX를 개선하기 위해서 텍스트 창에 입력한 값을 로컬스토리지를 통해 **캐싱**하기

**💡 핵심 : 검색어를 입력하고 새로고침해도 값이 캐싱되어 나타남(로컬스토리지에 저장)**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        /* CSS */
        .button-62 {
            background: linear-gradient(to bottom right, #EF4765, #FF9A5A);
            border: 0;
            border-radius: 12px;
            color: #FFFFFF;
            cursor: pointer;
            display: inline-block;
            font-family: -apple-system, system-ui, "Segoe UI", Roboto,
            Helvetica, Arial, sans-serif;
            font-size: 16px;
            font-weight: 500;
            line-height: 2.5;
            outline: transparent;
            padding: 0 1rem;
            text-align: center;
            text-decoration: none;
            transition: box-shadow .2s ease-in-out;
            user-select: none;
            -webkit-user-select: none;
            touch-action: manipulation;
            white-space: nowrap;
        }

        .button-62:not([disabled]):focus {
            box-shadow: 0 0 .25rem rgba(0, 0, 0, 0.5), -.125rem -.125rem 1rem rgba(239, 71, 101, 0.5), .125rem .125rem 1rem rgba(255, 154, 90, 0.5);
        }

        .button-62:not([disabled]):hover {
            box-shadow: 0 0 .25rem rgba(0, 0, 0, 0.5), -.125rem -.125rem 1rem rgba(239, 71, 101, 0.5), .125rem .125rem 1rem rgba(255, 154, 90, 0.5);
        }

        #field {
            font-size: 27px;
        }

        body {
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 0 auto;
            height: 100vh;
        }
    </style>
</head>
<body>
<div>
    <input type="text" id="field"/>
    <input type="button" class="button-62" value="검색" id="save"/>
    <input type="button" class="button-62" value="조회" id="read"/>
    <input type="button" class="button-62" value="삭제" id="clear"/>
</div>
</body>
<script>
    window.onload = async () => { // 모든 자원(html, js 등)이 로드 되었을 때 실행 
        const field = document.getElementById("field"), 
                save = document.getElementById("save"), 
                read = document.getElementById("read"), 
                clear = document.getElementById("clear")
        save.addEventListener("click", e => localStorage.setItem("입력값", field.value)) // 입력값 저장
        read.addEventListener("click", e => alert(window.localStorage["입력값"])) // 저장된 값 표출 
        clear.addEventListener("click", e => { // 로컬스토리지 전체 삭제 
            window.localStorage.clear()
            field.value = ""
        })
        if (window.localStorage["입력값"]) {
            field.value = window.localStorage["입력값"]
        }
    }
</script>
</html>
```

<br><br>


