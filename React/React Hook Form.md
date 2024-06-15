# React

## React Hook Form

> ✨ Performant, flexible and extensible forms with easy-to-use validation.  
> 손쉽게 검증할 수 있는, 퍼포먼스가 뛰어나고, 유연하며 확장 가능한 폼


* 개발자 경험 (DX)
  * 폼을 구축할 때 개발자에게 원활한 경험을 제공하는 직관적이고 기능이 완비된 API
* HTML 표준
  * 기존 HTML 마크업을 활용하고, 제약 기반 검증 API로 폼을 검증 가능
* 초경량 패키지 크기
  * React Hook Form은 의존성이 없는 작은 라이브러리입니다
* 성능
  * 리렌더링 횟수를 최소화하고, 검증 계산을 최소화하며, 더 빠르게 마운팅
* 도입 가능성
  * 폼 상태는 본질적으로 로컬이므로 다른 의존성 없이 쉽게 도입 가능 
* 사용자 경험 (UX)
  * 최고의 사용자 경험을 제공하고 일관된 검증 전략을 제공하기 위해 노력

<br><br>

## 장점

### 더 적은 코드와 더 높은 성능

React Hook Form은 불필요한 리렌더링을 제거하면서 작성해야 할 코드의 양을 줄여줌 

### 리렌더링 분리

컴포넌트의 리렌더링을 분리할 수 있어 페이지나 앱의 성능이 향상됨

### Subscriptions, 구독 

전체 폼을 다시 렌더링하지 않고, 개별 입력과 폼 상태 업데이트에 구독할 수 있는 기능 제공

### 빠른 마운팅 

다른 라이브러리와 비교해서 React Hook Form을 사용할 때 컴포넌트 마운팅이 더 빠름  
[Formik](https://formik.org/docs/overview), [ReduxForm](https://redux-form.com/8.3.0/) 등과 비교했을 때 React Hook Form은 더 빠름   
React Hook Form이 렌더링을 방해하지 않기 때문

<br><br>

## 사용방법

### 설치

```
npm install react-hook-form
```

### 예시 코드  

```tsx
import { useForm, SubmitHandler } from "react-hook-form";

type Inputs = {
  example: string,
  exampleRequired: string,
};

export default function App() {
  const { register, handleSubmit, watch, formState: { errors } } = useForm<Inputs>();
  
  const onSubmit: SubmitHandler<Inputs> = data => console.log(data);

  console.log(watch("example")) // watch input value by passing the name of it

  return (
    /* "handleSubmit" will validate your inputs before invoking "onSubmit" */
    <form onSubmit={handleSubmit(onSubmit)}>
      {/* register your input into the hook by invoking the "register" function */}
      <input
        defaultValue="test"
          {...register("example", {
            required: "example is required", 
            pattern: {
              value: /^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,4}$/,
              message: "Invalid"
          }
      })} />
      {/* include validation with required or other standard HTML validation rules */}
      <input {...register("exampleRequired", { required: true })} />
      {/* errors will return when field validation fails  */}
      {errors.exampleRequired && <span>This field is required</span>}
      
      <input type="submit" />
    </form>
  );
}
```

### 구성 요소

* useForm: React Hook Form의 훅, 폼 상태와 검증 기능 제공
* register: 폼 필드를 등록하고 검증 규칙을 지정
* handleSubmit: 폼 제출을 처리하고 유효성 검사
* formState: 폼 상태를 포함해, 오류 상태(errors) 확인

### 검증 추가

* required: 필드의 필수 여부 지정
* pattern: 정규식을 사용해 입력 값의 패턴을 검증
* message: 검증 실패 시 표시할 메시지 

<br><br>

## 참고 사이트 

> https://www.react-hook-form.com/get-started/#Quickstart
