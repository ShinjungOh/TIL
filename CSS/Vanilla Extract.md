# Vanilla Extract

## Vanilla Extract 설치하기 

```
npm i @vanilla-extract/css
```

* Next.js에서 사용할 경우 [추가 설정](https://vanilla-extract.style/documentation/integrations/next/) 필요
* `css.ts` 확장자는 Vanilla Extract 파일
* Vanilla Extract는 TypeScript이기 때문에 오타 잡아줌 -> TS 장점 그대로 활용 가능
* Styled-Component와는 다르게 서버 사이드 렌더링이 잘됨 
  * 개발자도구 네트워크 탭에서 HTML에 CSS 흔적이 들어가 있으면 서버 사이드 렌더링이 잘 되는것

<br>

### globalStyle

글로벌 스타일 적용하면서 HTML에 대한 CSS 속성, 미디어 쿼리를 하나의 그룹으로 작성 가능 

```ts
globalStyle('html', {
 boxSizing: 'border-box',
    padding: 0,
    margin: 0,
    '@media': {
        '(prefers-color-scheme: dark)': {
            colorScheme: 'dark',
        }
    }
});
```

<br>

### 미디어쿼리안에 변수가 들어간 경우

```css
 /*기존 */

@media (prefers-color-scheme: dark) {
  :root {
    --foreground-rgb: 255, 255, 255;
    --background-start-rgb: 0, 0, 0;
    --background-end-rgb: 0, 0, 0;

    --primary-glow: radial-gradient(rgba(1, 65, 255, 0.4), rgba(1, 65, 255, 0));
    --secondary-glow: linear-gradient(
      to bottom right,
      rgba(1, 65, 255, 0),
      rgba(1, 65, 255, 0),
      rgba(1, 65, 255, 0.3)
    );

    --tile-start-rgb: 2, 13, 46;
    --tile-end-rgb: 2, 5, 19;
    --tile-border: conic-gradient(
      #ffffff80,
      #ffffff40,
      #ffffff30,
      #ffffff20,
      #ffffff10,
      #ffffff10,
      #ffffff80
    );
  }
}
```

```ts
// Vanilla Extract
globalStyle(':root', {
    '@media': {
        '(prefers-color-scheme: dark)': {
            vars: assignVars(global, darkGlobalTheme),
        }
    }
})
```

<br>

### createGlobalThemeContract

테마에 대한 이름들을 모아두는 것

```ts
export const global = createGlobalThemeContract({
    background: {
        color: 'bg-color'
    },
    foreground: {
        color: 'fg-color'
    },
});

createGlobalTheme(':root', global, {
    background: {
        color: 'rgb(255, 255, 255)'
    },
    foreground: {
        color: 'rgb(0, 0, 0)'
    },
});
```

![vanilla-extract-브라우저.png](..%2FImages%2Fvanilla-extract-%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80.png)

* `bg-color`, `fg-color`가 브라우저에서는 `--bg-color`, `--fg-color`로 변환  

<br>

### 객체식으로 실제 CSS 값 만들기

```ts
const darkGlobalTheme = {
    background: {
        color: 'rgb(0, 0, 0)'
    },
    foreground: {
        color: 'rgb(255, 255, 255)'
    },
}
```

<br>

### 적용하기 

```ts
globalStyle(':root', {
    '@media': {
        '(prefers-color-scheme: dark)': {
            vars: assignVars(global, darkGlobalTheme),
        }
    }
})
```

<br>

### 자식 요소 표현하기

`.left img` 대신 `leftImg`라는 **새로운 클래스 네임**을 만드는 것이 좋음    
=> 더 Vanilla Extract같은 방식
* 💡 자식 태그 사용하는걸 추천하지 않음
* 하나의 클래스로 만드는게 Vanilla Extract의 지향점

```ts
// 부모요소
export const left = style({
    display: 'flex',
    alignItems: 'center',
    '@media': {
        '(min-width: 1000px)': {
            flex: 1,
            justifyContent: 'center',
        }
    }
});

// 자식요소 표현하기 1
globalStyle(`${left} img`, {
    width: 55,
    height: 65,
    '@media': {
        '(min-width: 1000px)': {
            width: 450,
            height: 550,
        }
    },
});

// 자식요소 표현하기 2 - 새로운 클래스로 분리
export const leftImg = style({
    width: 55,
    height: 65,
    '@media': {
        '(min-width: 1000px)': {
            width: 450,
            height: 550,
        }
    },
});
```

<br>

### selectors

셀렉터는 타겟이 무조건 자기 자신이어야 함   
**자신이 타겟일 때만** 쓸 수 있기 때문에, 자신이 아니라 자신의 자식, 자손이 타겟일 때는 사용 불가

<br>

### 그룹화 

‘hover’는 합쳐서 쓸 수 있음 - 그룹화 가능 

```ts
export const actionButton = style({
    width: '100%',
    height: 50,
    borderRadius: 25,
    border: '1px solid white',
    backgroundColor: 'rgb(15, 20, 25)',
    color: 'white',
    fontSize: 17,
    ':disabled': {
        opacity: 0.5,
    },
    ':hover': {
        backgroundColor: 'rgb(39,44,48)',
    },
    selectors: {
        '&:disabled:hover': {
            backgroundColor: 'rgb(15, 20, 25)',
        },
    }
});
```

<br>

### import

```ts
import * as style from '@/app/(beforeLogin)/_component/login.css';
```

기존의 module.css 파일을 Vanilla Extract로 변경할 때는 import만 변경하면 나머지는 그대로 사용 가능

<br><br>

## 참고 사이트 

https://vanilla-extract.style/
