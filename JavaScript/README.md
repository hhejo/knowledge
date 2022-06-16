# [자바스크립트 기초 강의 (ES5+)](https://www.youtube.com/watch?v=wcsVjmHrUQg&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2)



## Array

### 1. Declaration

```javascript
const arr1 = new Array();
const arr2 = [];
```

### 2. Length

```javascript
arr.length
```

### 3. Loop

```javascript
for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}
/////////////////////////////////////////////////////////////////////
for (let item of arr) {
    console.log(item);
}
/////////////////////////////////////////////////////////////////////
arr.forEach((item, index, array) => console.log(item, index, array));
```

### 4. Add, Delete, Copy

```javascript
arr.push(1);
arr.pop();
arr.unshift(); // 앞에 push
arr.shift(); // 앞에 pop
arr.splice(1); // 인덱스 1부터 전부 pop
arr.splice(1, 2); // 인덱스 1부터 2개 pop
arr.splice(1, 1, 'a', 'b'); // 인덱스 1부터 1개 pop, 이후 그 자리부터 'a', 'b' push
arr = arr1.concat(arr2); // arr1에 arr2 붙임
```

### 5. Search

```javascript
arr.indexOf('a'); // 없으면 -1
arr.includes('hi'); // 있는지 확인
arr.lastIndexOf(); // 뒤에서부터 확인
```

























---





hoisting : var, function declaration

callback function

synchronous callback

asynchronous callback

callback hell



promise : js object for asynchronous operation

state, producer, consumer

state : pending -> fulfilled or rejected

producer vs consumer

1. producer

```javascript
// when new Promise is created, the executor runs automatically.
const promise = new Promise((resolve, reject) => {
    // doing some heavy work (network, read files)
    console.log('doing something...');
    setTimeout(() => {
        // resolve('ellie');
        reject(new Error('no network'));
    }, 2000);
});
```

Promise 생성시 생성자에 executor 함수 전달 (resolve, reject)

resolve : 성공시 실행 함수

reject : 실패시 실행 함수

2. consumers

-> then, catch, finally

```javascript
// 정상적으로 수행되었을 때, 생성할 때 줬던 resolve 콜백 함수에서 전달된 값이 value로 전달
promise
  .then((value) => {
    console.log(value); // ellie
  })
  .catch(error => {
    console.log(error);
  });
  .finally(() => {
      console.log('finally');
  });
```

then은 Promise 객체 리턴

finally는 무조건 성공 여부 상관없이 호출



3. Promise chaining

```javascript
const fetchNumber = new Promise((resolve, reject) => {
    setTimeout(() => resolve(1), 1000);
});

fetchNumber
  .then(num => num * 2)
  .then(num => num * 3)
  .then(num => {
      // 새로운 Promise 리턴
      return new Promise((resolve, reject) => {
          setTimeout(() => resolve(num - 1), 1000);
      });
  })
  .then(num => console.log(num));
```



4. error handling

```javascript
const getHen = () => 
    new Promise((resolve, reject) => {
        setTimeout(() => resolve('🐓'), 1000);
    });
const getEgg = hen => 
    new Promise((resolve, reject) => {
        setTimeout(() => resolve(`${hen} => 🥚`), 1000);
    });
const cook = egg => 
    new Promise((resolve, reject) => {
        setTimeout(() => resolve(`${egg} => 🍳`), 1000);
    });

getHen()
  .then(hen => getEgg(hen)) // .then(getEgg) // 받아오는 값이 하나이면 생략 가능
  .then(egg => cook(egg)) // .then(cook)
  .then(meal => console.log(meal)); // 🐓 => 🥚 => 🍳 // .then(console.log)
// getHen().then(getEgg).then(cook).then(console.log); // prettier가 바꾸기 때문에 아래와 같이 변경해줌
getHen() // <- 주석 하나 붙이면 이렇게 작성 가능
  .then(getEgg)
  .then(cook)
  .then(console.log);
```



```javascript
const getHen = () => 
    new Promise((resolve, reject) => {
        setTimeout(() => resolve('🐓'), 1000);
    });
const getEgg = hen => 
    new Promise((resolve, reject) => {
        setTimeout(() => reject(new Error(`error! ${hen} => 🥚`)), 1000); // 에러 발생
    });
const cook = egg => 
    new Promise((resolve, reject) => {
        setTimeout(() => resolve(`${egg} => 🍳`), 1000);
    });

getHen() //
  .then(getEgg)
  .then(cook)
  .then(console.log)
  .catch(console.log); // Error: error! 🐓 => 🥚


getHen() //
  .then(getEgg)
  .catch(error => {
    return '🍔';
  })
  .then(cook)
  .then(console.log) // 🍔 => 🍳
  .catch(console.log); // Error: error! 🐓 => 🥚
```



5. callback hell -> promise





async, await

syntatic sugar

1. async

```javascript
function fetchUser() {
    // do network request in 10 secs...
    return new Promise((resolve, reject) => {
        return 'ellie';
    });
}

const user = fetchUser();
console.log(user); // Promise가 pending 상태로 출력 (resolve도, reject도 호출하지 않았기 때문)
```

```javascript
function fetchUser() {
    // do network request in 10 secs...
    return new Promise((resolve, reject) => {
        resolve('ellie');
    });
}

const user = fetchUser();
user.then(console.log); // fulfilled 상태
console.log(user);
```

async 사용하면?

```javascript
async function fetchUser() {
    // do network request in 10 secs...
	return 'ellie';
}

const user = fetchUser();
user.then(console.log); // fulfilled 상태
console.log(user);
```

Promise를 간편하게 쓸 수 있음



2. await

```javascript
function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple() {
    await delay(3000);
    return 'apple';
}

async function getBanana() {
    await delay(3000);
    return 'banana';
}
/*
function getBanana() {
    return delay(3000)
    .then(() => 'banana');
}
*/

function pickFruits() {
    return getApple()
    .then(apple => {
        return getBanana()
        .then(banana => `${apple} + ${banana}`);
    });
}

pickFruits().then(console.log); // apple + banana
```



```javascript
function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple() {
    await delay(3000);
    throw 'error'; // 에러 던지면 try catch로 받음
    return 'apple';
}

async function getBanana() {
    await delay(3000);
    return 'banana';
}

async function pickFruits() {
    const apple = await getApple();
    const banana = await getBanana();
    

    /*
    try {
        const apple = await getApple();
        const banana = await getBanana();
    } catch() {
        //
    }
    */
    return `${apple} + ${banana}`;
}

pickFruits().then(console.log); // apple + banana
```



await 병렬처리

```javascript
function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple() {
    await delay(3000);
    return 'apple';
}

async function getBanana() {
    await delay(3000);
    return 'banana';
}

async function pickFruits() {
    const applePromise = getApple(); //
    const bananaPromise = getBanana(); //
    const apple = await applePromise; //
    const banana = await bananaPromise; //
    return `${apple} + ${banana}`; // 1초만에 병렬 실행 (사과, 바나나를 1초만에 동시에 따옴)
}

pickFruits().then(console.log); // apple + banana
```



3. useful promise

```javascript
function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple() {
    await delay(2000);
    return 'apple';
}

async function getBanana() {
    await delay(1000);
    return 'banana';
}

// useful Promise APIs
function pickAllFruits() {
    return Promise.all([getApple(), getBanana()])
    .then(fruits => fruits.join(' + '));
}
pickAllFruits().then(console.log); // apple + banana

// 둘 중 아무거나 먼저 따는 과일 가져오기
function pickOnlyOne() {
    return Promise.race([getApple(), getBanana()]);
}
pickOnlyOne().then(console.log);
```



