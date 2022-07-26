# Next.js

## API 호출

> npm i axios

<br>

#### index.js

```javascript
export default Home = () => {
    const [list, setList] = useState([]);
    const API_URL =
        "http://makeup-api.herokuapp.com/api/v1/products.json?brand=maybelline";

    function getData() {
        Axios.get(API_URL)
            .then(res => {
                console.log(res.data);
                setList(res.data);
            });
    }

    useEffect(() => {  // 최초 1번만 호출
        getData();
    }, []);


    return (
        <div>
            <Head>
                <title>HOME</title>
            </Head>
            <ItemList list={list}/>
        </div>
    )
}
```

<br>

#### ItemList.js (src/component/ItemList.js)

```javascript

import {Grid} from "semantic-ui-react";

export default ItemList = ({list}) => {
    return (
        <div>
            list
            <Grid column={3}>
                <Grid.Row>
                    {list.map((item) => (
                        <Grid.Column>
                            <img src="item.image.link" alt={item.name}/>
                            <strong>{item.name}</strong>
                            <span>
                                {item.category} {item.product_type}
                            </span>
                            <strong>${item.price}</strong>
                        </Grid.Column>
                    ))}
                </Grid.Row>
            </Grid>
        </div>
    );
}
```

<br><br>

## Dynamic Routes

> https://nextjs.org/docs/routing/dynamic-routes

<br>

#### [id].js (pages/view/[id].js)

```javascript
import {useRouter} from 'next/router'

const Post = () => {
    const router = useRouter();
    const {id} = router.query

    return <p>Post: {id}</p>
}

export default Post;
```

<br><br>

## next/link

> https://nextjs.org/docs/api-reference/next/link

<br>

#### ItemList.js (src/component/ItemList.js)

* next/link 추가

```javascript
import {Grid} from "semantic-ui-react";
import Link from 'next/link';

export default ItemList = ({list}) => {
    return (
        <div>
            list
            <Grid column={3}>
                <Grid.Row>
                    {list.map((item) => (
                        <Grid.Column key={item.id}>
                            <Link href={`/view/${item.id}`}>
                                <a>
                                    <img src="item.image.link" alt={item.name}/>
                                    <strong>{item.name}</strong>
                                    <span>
                                        {item.category} {item.product_type}
                                    </span>
                                    <strong>${item.price}</strong>
                                </a>
                            </Link>
                        </Grid.Column>
                    ))}
                </Grid.Row>
            </Grid>
        </div>
    );
}
```

<br>

#### [id].js (pages/view/[id].js)

* 상세페이지 구현

```javascript
import {useRouter} from 'next/router'

const Post = () => {
    const router = useRouter();
    const {id} = router.query;

    const [item, setItem] = useState({});

    const API_URL = `http://makeup-api.herokuapp.com/api/v1/products/${id}.json`;

    function getData() {
        Axios.get(API_URL)
            .then(res => {
                console.log(res.data);
            });
    }

    useEffect(() => {
        if (id && id > 0) {
            getData();
        }
    }, [id]);


    return <Item item={item}/>
}

export default Post;
```

<br>

#### Item.js (src/component/Item.js)

* Item 컴포넌트 생성 후 [id].js에 import

```javascript
export default function Item({item}) {
    const {image_link, name, price, description} = item;

    return (
        <>
            <div>
                <img src={image_link} alt={name}/>
            </div>
            <div>
                <strong>{name}</strong>
                <strong>${price}</strong>
            </div>
            <Button>구매하기</Button>
            <div>
                <p>{description}</p>
            </div>
        </>
    );
}
```
