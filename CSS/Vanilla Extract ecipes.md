# Vanilla-extract

## recipes

### 개념

다양한 변형(multi-variant) 스타일을 만드는 type-safe 런타임 API  
나머지 vanilla-extract와 마찬가지로 모든 스타일은 빌드 시 생성

* [Stitches](https://stitches.dev/)에서 많은 영감을 받음
  * CSS-in-JS near-zero runtime
  * SSR
  * multi-variant 지원
  * ⚠️ 2023년 부터, Stitches 사이트는 더 이상 관리되지 않음 

<br>

### 설치

```bash
npm install @vanilla-extract/recipes
```

다중 변형 스타일 함수를 생성해서, 런타임이나 `.css.ts.` 파일에서 정적으로 사용할 수 있음  
옵션으로 base 스타일, variants, compoundVariants, defaultVariants를 허용

<br>

### 예시 

```ts
export const button = recipe({
  base: { // ✅
    borderRadius: 6
  },

  variants: { // ✅
    color: {
      neutral: { background: 'whitesmoke' },
      brand: { background: 'blueviolet' },
      accent: { background: 'slateblue' }
    },
    size: {
      small: { padding: 12 },
      medium: { padding: 16 },
      large: { padding: 24 }
    },
    rounded: {
      true: { borderRadius: 999 }
    }
  },

  // 여러 변형(multiple variants)이 동시에 설정될 때 적용
  compoundVariants: [ // ✅
    {
      variants: {
        color: 'neutral',
        size: 'large'
      },
      style: {
        background: 'ghostwhite'
      }
    }
  ],

  defaultVariants: { // ✅
    color: 'accent',
    size: 'medium'
  }
});
```

<br><br>

## RecipeVariants

레시피의 타입 인터페이스를 활용하는 유틸리티  
인터페이스의 일부로 `레시피 값`을 허용해야 하는 함수나 컴포넌트 props를 입력할 때 유용

```ts
import { recipe, RecipeVariants } from '@vanilla-extract/recipes';

export const button = recipe({
  variants: {
    color: {
      neutral: { background: 'whitesmoke' },
      brand: { background: 'blueviolet' },
      accent: { background: 'slateblue' }
    },
    size: {
      small: { padding: 12 },
      medium: { padding: 16 },
      large: { padding: 24 }
    }
  }
});

// Get the type
// 다음과 같은 타입을 얻음
export type ButtonVariants = RecipeVariants<typeof button>;

// the above will result in a type equivalent to:
// 위의 코드는 다음과 같은 타입을 생성할 것
export type ButtonVariants = {
  color?: 'neutral' | 'brand' | 'accent';
  size?: 'small' | 'medium' | 'large';
};
```

<br><br>

## 참고 사이트

> https://vanilla-extract.style/documentation/packages/recipes/
