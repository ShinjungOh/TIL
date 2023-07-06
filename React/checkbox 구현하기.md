# React

## Checkbox 구현하기

* onChange 함수에서는 prev 보다 이벤트 객체의 값을 이용하는 것이 좋음 

```tsx
setIsChecked((prev) => !prev)
```

```tsx

export default function SignupPage () {
    const [isChecked, setIsChecked] = useState(false);
    
    const handleChangeCheckbox = (e: ChangeEvent<HTMLInputElement>) => {
        setIsChecked(e.target.checked);
    }
    
    return (
      <>
        <input 
            type="checkbox" 
            name="checkbox" 
            id="checkbox"
            value="약관동의"
            checked={isChecked}
            onchange={handleChangeCheckbox}
        />
        <label htmlFor="checkbox">
            [필수] 개인정보 수집 및 이용 동의
        </label>
      </>  
    );
}
```

<br><br>

## 스타일링

* accent-color : 체크 시 배경색
* ✔️ 아이콘의 색상은 배경색에 맞게 변함
  * purple의 경우 흰색 ✓
  * skyblue의 경우 검은색 ✔️

```tsx

const Checkbox = styled.input`
    accent-color: red;
`;
```

<br><br>

## 참고 사이트

> [accent-color](https://developer.mozilla.org/en-US/docs/Web/CSS/accent-color)
