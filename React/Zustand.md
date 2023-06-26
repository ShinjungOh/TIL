# Zustand 

## 개념

> A small, fast, and scalable bearbones state management solution.
> Zustand has a comfy API based on hooks. 
> It isn't boilerplatey or opinionated, but has enough convention to be explicit and flux-like.

작고 빠르며 확장 가능한 상태 관리 솔루션   
훅(hook) 기반의 편안한 API  
boilerplate가 필요하지는 않지만 명시적이고 **flux** 패턴을 따르는 충분한 컨벤션이 존재 

<br><br>

## 장점

* 매우 가벼움 (리덕스의 60%, 리코일의 20분의 1)
* 사용법이 간단함
* npm 다운로드 추이가 점차 상승 중 

<br><br>

## 사용 방법

### 1. 설치

```bash
# NPM
npm install zustand

# Yarn
yarn add zustand
```

<br>

### 2. 스토어 생성

store는 hook이 되며 원시형, 객체, 함수 등 무엇이든 넣을 수 있음  
함수 `set`은 상태를 머지

💡 **상태**와 **액션**을 저장

```tsx
import { create } from 'zustand'

const useStore = create((set) => ({
bears: 0,
increasePopulation: () => set((state) => ({ bears: state.bears + 1 })),
removeAllBears: () => set({ bears: 0 }),
}))
```

<br>

### 3. 컴포넌트 바인딩

컴포넌트에서 import 해서 사용하면 됨  
provider가 없어도 어디에서나 hook을 사용 가능  
상태를 선택하면 해당 상태가 변경될 때 해당 컴포넌트가 다시 렌더링됨 

```tsx
function BearCounter() {
    const bears = useStore((state) => state.bears)
    return <h1>{bears} around here...</h1>
}

function Controls() {
    const increasePopulation = useStore((state) => state.increasePopulation)
    return <button onClick={increasePopulation}>one up</button>
}
```

