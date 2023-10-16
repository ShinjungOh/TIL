# API 호출 함수 분리하기

## 기존

```tsx
 const handleClickSignUp = async () => {
    try {
        const responseSignUp = await http.post<{ user: { user_token: string; name: string } }>('/user/signup', {
            email: user.email,
            password: user.password,
            name: user.name,
        });
        
        if (responseSignUp.data) {
            const accessToken = responseSignUp.data.user.user_token;
            const userProfile = {
                name: responseSignUp.data.user.name,
            };
            localStorage.setItem(ACCESS_TOKEN_KEY, accessToken);
            localStorage.setItem(USER_NAME_KEY, userProfile.name);
            navigate(PATH.CALENDAR);
        }
    } catch (e) {
        await axiosErrorAlert(e);
    }
};
```

<br><br>

## 분리하기

* api 폴더에 도메인별 디렉토리 생성
* 각 호출 함수명에는 'api-'를 붙임

```ts
// src/api/user/apiPostSignup.ts

import {UserType} from '@lib/types';
import {http} from '../http';

type ResponsePostSignup = {
    token: string;
    user: {
        type: number;
        name: string;
        email: string;
    };
};

type RequestPostSignup = {
    email: string;
    password: string;
    name: string;
};

export const apiPostSignup = (user: UserType) => {
    const data = {
        email: user.email,
        password: user.password,
        name: user.name,
    };

    return http.post<ResponsePostSignup, RequestPostSignup>('/user/signup', data);
};
```

<br><br>

## 사용하기

```tsx
import { apiPostSignup } from '../api/user';

const handleClickSignUp = async () => {
    try {
        const responseSignUp = await apiPostSignup(user);

        if (responseSignUp.success && responseSignUp.data) {
            const accessToken = responseSignUp.data.token;
            const userProfile = {
                name: responseSignUp.data.user.name,
            };
            localStorage.setItem(ACCESS_TOKEN_KEY, accessToken);
            localStorage.setItem(USER_NAME_KEY, userProfile.name);
            navigate(PATH.CALENDAR);
        }
    } catch (e) {
        await axiosErrorAlert(e);
    }
};
```

<br><br>

## 장점

* 변수명으로 API를 사용하는 함수인지 알 수 있음
* 코드가 간결해짐 
* 타입 에러를 방지 
