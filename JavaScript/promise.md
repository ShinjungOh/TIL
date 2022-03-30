# Promise

## 소개

### Callback Hell

- id가 'btn'인 button을 클릭하면 서버에 users 리스트를 가져오는 요청을 하고,
- 성공하면 list의 세번째 user의 정보를 다시 요청하여
- 성공하면 user의 profileImage url값을 가져다가 image 태그로 표현하고,
- 이 image를 클릭하면 해당 이미지를 제거.

```js
const script= document.createElement('script')
script.src= 'https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.min.js'
document.body.appendChild(script)

document.body.innerHTML += '<button id="btn">클릭</button>'
document.getElementById('btn').addEventListener('click', function (e) {
  $.ajax({
    method: 'GET',
    url: 'https://api.github.com/users?since=1000',
    success: function (data) {
      var target = data[2]
      $.ajax({
        method: 'GET',
        url: 'https://api.github.com/user/' + target.id,
        success: function (data) {
          var _id = 'img' + data.id
          document.body.innerHTML += '<img id="' + _id + '" src="' + data.avatar_url + '"/>'
          document.getElementById(_id).addEventListener('click', function (e) {
            this.remove()
          })
        },
        error: function (err) {
          console.error(err)
        }
      })
    },
    error: function (err) {
      console.error(err)
    }
  })
})
```

<br>

### Promise

```js
document.body.innerHTML = '<button id="btn">클릭</button>'
document.getElementById('btn').addEventListener('click', function (e) {
    fetch('https://api.github.com/users?since=1000')
    .then(function (res) { return res.json() })
    .then(function (res) {
        var target = res[2]
        return fetch('https://api.github.com/user/' + target.id)
    })
    .then(function (res) { return res.json() })
    .then(function (res) {
        var _id = 'img' + res.id
        document.body.innerHTML += '<img id="' + _id + '" src="' + res.avatar_url + '"/>'
        document.getElementById(_id).addEventListener('click', function (e) {
            this.remove()
        })
    })
    .catch(function (err) {
        console.error(err)
    })
})
```
* 간결하고 가독성이 높아짐

<br>

### Promise를 반환하면서 JSON parsing을 자동으로 해주는 library (axios) 활용시

```js
const script= document.createElement('script')
script.src= 'https://cdnjs.cloudflare.com/ajax/libs/axios/0.18.0/axios.min.js'
document.body.appendChild(script)

document.body.innerHTML += '<button id="btn">클릭</button>'
document.getElementById('btn').addEventListener('click', function (e) {
    axios.get('https://api.github.com/users?since=1000')
    .then(function (res) {
        var target = res.data[2]
        return axios.get('https://api.github.com/user/' + target.id)
    })
    .then(function (res) {
        var _id = 'img' + res.data.id
        document.body.innerHTML += '<img id="' + _id + '" src="' + res.data.avatar_url + '"/>'
        document.getElementById(_id).addEventListener('click', function (e) {
            this.remove()
        })
    })
    .catch(function (err) {
        console.error(err)
    })
})
```
<br>

## 상세

### Promise Status

- unnsettled (미확정) 상태: pending. thenable하지 않다. (비동기 처리가 끝나기 전)
- settled (확정) 상태: resolved. thenable한 상태.
   - fulfilled (성공)
   - rejected (실패)

```js
const promiseTest = param => new Promise((resolve, reject) => {
	setTimeout(() => {
		if (param) {
			resolve("해결 완료")
		} else {
			reject(Error("실패!!"))
		}
	}, 1000)
})

const testRun = param => promiseTest(param)
  .then(text => { console.log(text) })
  .catch(error => { console.error(error) })

const a = testRun(true)
const b = testRun(false)
```
* 비동기 처리를 할 수 있게 해줌
* resolved는 확정상태 자체 또는 성공 표시 둘 중 하나로 쓰이기 때문에, 문맥에 따라서 파악해야 한다. 

<br>
