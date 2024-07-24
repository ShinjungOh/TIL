# React

## React Hook Form

> ✨ Performant, flexible and extensible forms with easy-to-use validation.  
> 손쉽게 검증할 수 있는, 퍼포먼스가 뛰어나고, 유연하며 확장 가능한 폼


* 개발자 경험 (DX)
  * 폼을 구축할 때 개발자에게 원활한 경험을 제공하는 직관적이고 기능이 완비된 API
* HTML 표준
  * 기존 HTML 마크업을 활용하고, 제약 기반 검증 API로 폼을 검증 가능
* 초경량 패키지 크기
  * React Hook Form은 의존성이 없는 작은 라이브러리
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

## 유효성 검사

### yup 사용하기 

React Hook Form 자체에 내장된 유효성 검사 기능을 사용하면 쉽게 사용자 입력값을 검증 가능 

```
npm install @hookform/resolvers yup
```

유효성 검사를 강화하고, 입력 필드에 따라 동적으로 오류 메시지를 표시     
yup 라이브러리를 사용하여 스키마 기반 유효성 검사를 수행

<br>

### yup으로 유효성 검사 스키마 정의

```tsx
import * as yup from 'yup';
import { yupResolver } from '@hookform/resolvers/yup';

type SignupInput = {
  email: string;
  password: string;
  passwordCheck: string;
  name: string;
  nickname: string;
};

const validationSchema = yup
        .object({
          email: yup.string().email('유효한 이메일 형식이 아닙니다.').required('이메일을 입력해주세요.'),
          password: yup
                  .string()
                  .min(8, '8글자 이상 입력해주세요.')
                  .matches(
                          /^(?=.*[A-Za-z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$/,
                          '한 개 이상의 영문자, 숫자, 특수문자를 포함해야 합니다.',
                  )
                  .required('비밀번호를 입력해주세요.'),
          passwordCheck: yup
                  .string()
                  .oneOf([yup.ref('password'), undefined], '비밀번호가 일치하지 않습니다.')
                  .required('비밀번호를 다시 입력해주세요.'),
          name: yup
                  .string()
                  .matches(/^[가-힣]{2,10}$/, '2글자 이상 10글자 이하의 한글만 가능합니다.')
                  .required('이름을 입력해주세요.'),
          nickname: yup
                  .string()
                  .matches(/^[가-힣]{2,10}$/, '2글자 이상 10글자 이하의 한글만 가능합니다.')
                  .required('닉네임을 입력해주세요.'),
        })
        .required();
```

<br>

### React Hook Form에 통합하기

```tsx
import { yupResolver } from '@hookform/resolvers/yup';

export const Signup = () => {
  const navigate = useNavigate();
  const {
    register,
    handleSubmit,
    watch,
    formState: { errors },
  } = useForm<SignupInput>({
    resolver: yupResolver(schema), // ✅
    mode: 'onChange', // 필드 값이 변경될 때마다 유효성 검사를 수행
  });
  
// ...
```

<br>

### Submit 버튼과 연동하기

#### 버튼의 disabled 속성을 이용하는 방법 

* useForm 훅의 formState와 isValid 속성을 사용해서 버튼의 비활성화 상태 관리하기
* isValid를 사용하면 **현재 폼의 모든 필드가 유효한지** 확인 가능 

```tsx
const {
  register,
  handleSubmit,
  formState: { errors, isValid }, // ✅isValid 추가
} = useForm<SignupInput>({
  resolver: yupResolver(validationSchema),
  mode: 'onChange',
});

// ...

 <BaseButton 
    type="submit" 
    theme="active" 
    fontColor={styleToken.color.white} 
    isDisabled={!isValid} // ✅
>
  회원가입
</BaseButton>
```


<br><br>

## 참고 사이트 

> https://www.react-hook-form.com/get-started/#Quickstart  
> https://react-hook-form.com/get-started#SchemaValidation
