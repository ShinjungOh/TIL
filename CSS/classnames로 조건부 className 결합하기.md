# className

## classnames로 조건부 className 결합하기

> **classnames**  
> https://www.npmjs.com/package/classnames  
> https://github.com/JedWatson/classnames#readme

```
npm i classnames
```

조건부로 클래스가 달라져야할 때 합성해주는 라이브러리 (classnames, cx)

<br><br>

## 예시 

* 사용방법이 많음 - 공식 문서 참고 

### Case 1

```tsx
import cx from 'classnames';

export default function ActionButtons() {
    return (
        <div className={style.actionButtons}>
            <div className={cx(style.commentButton, {[style.commented]: commented})}/> // 1️⃣
            <div className={cx(style.repostButton, reposted && style.reposted)}/> // 2️⃣
            <div className={cx([style.heartButton, liked && style.liked])}/> // 3️⃣
        </div>
    )
}
```

<br>

### Case 2

```tsx
import cx from "classnames";

export default function PostImages({post}: Props) {
    if (post.Images.length === 1) {
        return (
            <Link
                href={`/${post.User.id}/status/${post.postId}/photo/${post.Images[0].imageId}`}
                className={cx(style.postImageSection, style.oneImage)} // ✅
            >
                <img src={post.Images[0]?.link} alt=""/>
            </Link>
        );
    }

    if (post.Images.length === 2) {
        return (
            <div className={cx(style.postImageSection, style.twoImage)}></div> // ✅
        );
    }

    if (post.Images.length === 3) {
        return (
            <div className={cx(style.postImageSection, style.threeImage)}></div> // ✅
        );
    }

    if (post.Images.length === 4) {
        return (
            <div className={cx(style.postImageSection, style.fourImage)}></div> // ✅
        );
    }

    return null;
}
```
