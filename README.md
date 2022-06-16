# Knowledge



Algorithm, Data Structure

JavaScript

React.js









# React.js



### JavaScript

1. `let`, `const`

2. Arrow Functions

   - ```javascript
     function callMe(name) {
         console.log(name);
     }
     ////////////////////////////////
     const callMe = function(name) {
         console.log(name);
     };
     ////////////////////////////////
     const callMe = (name) => {
         console.log(name);
     };
     ////////////////////////////////
     const callMe = () => {
         console.log('Max!');
     };
     ////////////////////////////////
     const callMe = name => {
         console.log(name);
     };
     ////////////////////////////////
     ////////////////////////////////
     const returnMe = name => {
         return name;
     }
     ////////////////////////////////
     const returnMe = name => name;
     ```

3. `export`, `import`

   - ```javascript
     export default ...; // default
     export const someData = ...; // named
     ```

   - ```javascript
     import someNameOfYourChoice from './file.js';
     import { someData } from './file.js';
     ```

4. `class`

   - ```javascript
     class Person {
         constructor() {
             this.name = 'what';
         }
     }
     const person = new Person();
     console.log(person.name);
     ////////////////////////////////
     class Person {
         name = 'what';
         printMyName() {
             console.log(this.name);
         }
     }
     ////////////////////////////////
     class Person {
         name = 'what';
         printMyName = () => {
             console.log(this.name);
         }
     }
     ////////////////////////////////
     class Human {
         species = 'human';
     }
     class Person extends Human {
         name = 'what';
         printMyName = () => {
             console.log(this.name);
         }
     }
     ```

5. `...`

   - ```javascript
     const oldArray = [1, 2, 3];
     const newArray = [...oldArray, 4, 5]; // [1, 2, 3, 4, 5]
     const oldObject = {
         name: 'name';
     }
     const newObject = {
         ...oldObject,
         age: 20
     } // { name: 'name', age: 20 }
     ```

6. Destructuring

   - ```javascript
     const array = [1, 2, 3];
     const [a, b] = array; // a: 1, b: 2
     const myObj = {
         name: 'myName',
         age: 20
     }
     const { name } = myObj; // name: myName
     ```



React는 선언적 (Declarative Approach)



### Components

- React 앱의 최소 단위
- props(부모->자식)를 입력 받아 state(내부에서 값 변경)에 따라 DOM Node를 출력하는 함수
- 항상 대문자로 시작
- UI를 재사용 가능한 개별적인 여러 조각으로 나누고, 각 조각을 개별적으로 살펴볼 수 있음
- JavaScript 함수와 유사 (함수형 컴포넌트)

1. 함수형 컴포넌트 (Stateless Functional Component)
2. 클래스형 컴포넌트 (Class Component)



### JSX

- JavaScript를 확장한 문법 (React와 함께 사용하는 것을 권장)
- React element를 생성
- 중괄호로 감싸 JSX 안에 사용 가능 (JavaScript 표현식)
- JSX도 표현식이므로 if, for loop 안에 사용 가능
- HTML 태그의 attribute에 중괄호를 사용해 JavaScript 표현식 삽입 가능
- `className`으로 class 삽입 가능
- Babel은 JSX를 `React.createElement()` 호출로 컴파일하기 때문에 객체를 표현
- 브라우저는 JSX 코드를 지원하지 않기 때문에 변환됨



## React app 생성

`npx create-react-app my-app`

`cd my-app`

`npm start` (`npm run start`)



### 명령형 (Imperative)

- 무엇을 **어떻게** 할 것

- 과정에 집중해 원하는 결과를 얻으려 함

- JavaScript는 명령형

- ```javascript
  const pa = document.createElement("p");
  pa.textContent = "This is also visible";
  document.getElementById("root").append(pa); // 무엇을 하는지 단계별로 정확히 지시
  ```

### 선언형

- **무엇을** 할 것
- 결과에만 집중하고 과정에 대해서는 추상화를 통해 깊게 알려 하지 않음
- 가독성이 좋고 예측이 쉬움



```react
// index.js
import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css"; // css를 import로 가져옴
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <App /> // App (self-closing tag)
  </React.StrictMode>
);
```

```react
// App.js
import React from "react"; // 없어도 상관 없음 (없어도 자동으로 변환)

const App = () => {
  return (
    <div className="App"> // className으로 클래스 지정
      <h2>Let's get started!</h2>
    </div>
  );
};

export default App;
```

`return`할 때 하나의 컴포넌트만 리턴



### 합성 (Composition)

상속 대신 합성을 사용하여 컴포넌트 간에 코드를 재사용하는 것이 좋음

`props.children`을 사용해서 자식 엘리먼트를 출력에 그대로 전달 (wrapper로만 사용)

```react
import React from "react";
import "./Card.css";

const Card = (props) => { // Card라는 wrapper
  const classes = "card " + props.className; // wrapper의 클래스 추가
  return <div className={classes}>{props.children}</div>; // 클래스 추가 후 props.children으로 바로 전달
};

export default Card;
```



### props

- 속성을 나타내는 데이터
- 컴포넌트에 전달하는 값
- 컴포넌트의 자체 props를 수정하면 안 됨 (반드시 순수 함수처럼 동작해야 함)



옛날 버전 React

```react
/*
return (
  <div>
    <h2>Let's get started!</h2>
    <Expenses items={expenses} />
  </div>
);
*/

import React from 'react';
// ...
return React.createElement('div', {}, 
  React.createElement('h2', {}, "Let's get started!"),
  React.createElement(Expenses, {items: expenses})
);
```



---



### Event

중괄호 안에 함수 전달

```react
const clickHandler = (event) => console.log(event.target.value);
//
<button onClick={clickHandler}></button>
////////////////////////////////////////////////////
<input type="text" onChange={titleChangeHandler} />
```

컴포넌트 -> 컴포넌트에도 전달 가능

```react
<ExpenseForm onSaveExpenseData={saveExpenseDataHandler} />
```



### useState

`useState(초기값)`

- 2개 리턴 (값, 값 변경 함수)

```react
import React, { useState } from "react";
// ...
const ExpenseItem = (props) => {
  const [title, setTitle] = useState(props.title); // 초기값 넣어줌. 무조건 2개 리턴

  const clickHandler = () => {
    setTitle("Updated!"); // title을 직접 변경하지 않고 setTitle을 이용
    console.log(title); // 업데이트 되지 않은 title이 출력 !!! <- 비동기 때문인데 나중에 알아보기
  };
  console.log("ExpenseItem evaluated by React");

  return (
    <Card className="expense-item">
      <ExpenseDate date={props.date} />
      <div className="expense-item__description">
        <h2>{props.title}</h2>
        <div className="expense-item__price">${props.amount}</div>
      </div>
      {/* <button onClick={clickHandler}>Change Title</button> */}
    </Card>
  );
};
```



`useState`를 사용하지 않으면?

```react
import React, { useState } from "react";
// ...
const ExpenseItem = (props) => {
  let title = props.title; // props로 title을 부모에게 받음

  const clickHandler = () => {
    title = "updated!";
    console.log(title); // title은 분명 updated!로 변경되어 콘솔에는 출력되지만, 화면에는 변경되지 않음
  };

  return (
    <Card className="expense-item">
      <ExpenseDate date={props.date} />
      <div className="expense-item__description">
        {/* <h2>{title}</h2> */}
        <h2>{title}</h2> {/* 변경되지 않음... (콘솔에서는 변경됨) */}
        <div className="expense-item__price">${props.amount}</div>
      </div>
      <button onClick={clickHandler}>Change Title</button>
    </Card>
  );
};
```

React의 렌더링 방식 때문 (JSX의 작동 방식).. 이래서 State를 사용



리액트 훅은 컴포넌트 함수에서 직접 호출되어야 함 (바깥에다가 `useState` 같은 것 사용할 수 없음)



`onChange`가 `onInput`보다 모든 유형에 대해 변화를 잡을 수 있어 좋음



### useState 여러 개

여러 State를 위해 `useState`를 여러 번 쓸 수 있지만, 한 번에 뭉쳐 쓸 수도 있음 (나중에 더 알아보기)

1. `useState`를 여러 번 쓰기

   ```react
   // ExpenseForm.js
   import React, { useState } from "react";
   
   import "./ExpenseForm.css";
   
   const ExpenseForm = (props) => {
     const [enteredTitle, setEnteredTitle] = useState("");
     const [enteredAmount, setEnteredAmount] = useState("");
     const [enteredDate, setEnteredDate] = useState("");
   
     const titleChangeHandler = (event) => {
       setEnteredTitle(event.target.value);
     };
     const amountChangeHandler = (event) => {
       setEnteredAmount(event.target.value);
     };
     const dateChangeHandler = (event) => {
       setEnteredDate(event.target.value);
     };
   
     const submitHandler = (event) => {
       event.preventDefault();
   
       const expenseData = {
         title: enteredTitle,
         amount: enteredAmount,
         date: new Date(enteredDate),
       };
   
       props.onSaveExpenseData(expenseData); // 부모에게 전달
       setEnteredTitle("");
       setEnteredAmount("");
       setEnteredDate("");
     };
   
     return (
       // submit 버튼 대신 여기에 이벤트 연결
       <form onSubmit={submitHandler}>
         <div className="new-expense__controls">
           <div className="new-expense__control">
             <label>Title</label>
             <input type="text" value={enteredTitle} onChange={titleChangeHandler} />
           </div>
           <div className="new-expense__control">
             <label>Amount</label>
             <input type="number" value={enteredAmount} onChange={amountChangeHandler} />
           </div>
           <div className="new-expense__control">
             <label>Date</label>
             <input type="date" value={enteredDate} onChange={dateChangeHandler} />
           </div>
         </div>
         <div className="new-expense__actions">
           <button type="submit">Add Expense</button>
           {/* submit 버튼. 여기에 직접 이벤트 달지 않았음 */}
         </div>
       </form>
     );
   };
   
   export default ExpenseForm;
   ```

2. `useState`를 한 번에 쓰기 (잘못된 방식, 올바른 방식 확인)

   ```react
   // ExpenseForm.js
   import React, { useState } from "react";
   
   import "./ExpenseForm.css";
   
   const ExpenseForm = (props) => {
     // 객체를 이용해 작성
     const [userInput, setUserInput] = useState({
       enteredTitle: "",
       enteredAmount: "",
       enteredDate: "",
     });
   
     const titleChangeHandler = (event) => {
       // // 잘못된 방식
       // setUserInput({
       //   ...userInput,
       //   enteredTitle: event.target.value,
       // });
       // 올바른 방식
       setUserInput((prevState) => {
         return { ...prevState, enteredTitle: event.target.value };
       });
     };
   
     const amountChangeHandler = (event) => {
       // setUserInput({
       //   ...userInput,
       //   enteredAmount: event.target.value,
       // });
       setUserInput((prevState) => {
         return { ...prevState, enteredAmount: event.target.value };
       });
     };
   
     const dateChangeHandler = (event) => {
       // setUserInput({
       //   ...userInput,
       //   enteredDate: event.target.value,
       // });
       setUserInput((prevState) => {
         return { ...prevState, enteredDate: event.target.value };
       });
     };
   
     const submitHandler = (event) => {
       event.preventDefault();
   
       // ...
     };
   
     return (
       <form onSubmit={submitHandler}>
         <div className="new-expense__controls">
           <div className="new-expense__control">
             <label>Title</label>
             <input type="text" value={enteredTitle} onChange={titleChangeHandler} />
           </div>
           <div className="new-expense__control">
             <label>Amount</label>
             <input type="number" value={enteredAmount} onChange={amountChangeHandler} />
           </div>
           <div className="new-expense__control">
             <label>Date</label>
             <input type="date" value={enteredDate} onChange={dateChangeHandler} />
           </div>
         </div>
         <div className="new-expense__actions">
           <button type="submit">Add Expense</button>{" "}
         </div>
       </form>
     );
   };
   
   export default ExpenseForm;
   ```



### Two way binding (양방향 바인딩)

```react
// ExpenseForm.js
import React, { useState } from "react";

import "./ExpenseForm.css";

const ExpenseForm = (props) => {
  const [enteredTitle, setEnteredTitle] = useState("");
  // ...

  const titleChangeHandler = (event) => {
    setEnteredTitle(event.target.value);
  };
  // ...

  const submitHandler = (event) => {
    event.preventDefault();

    const expenseData = {
      title: enteredTitle,
      amount: enteredAmount,
      date: new Date(enteredDate),
    };

    props.onSaveExpenseData(expenseData); // 부모에게 전달
    setEnteredTitle("");
    setEnteredAmount("");
    setEnteredDate("");
  };

  return (
    <form onSubmit={submitHandler}>
      <div className="new-expense__controls">
        <div className="new-expense__control">
          <label>Title</label>
          {/* value에 state 변수를 작성해 양방향 바인딩 */}
          <input type="text" value={enteredTitle} onChange={titleChangeHandler} />
        </div>
        {/* ... */}
      </div>
      <div className="new-expense__actions">
        <button type="submit">Add Expense</button>
      </div>
    </form>
  );
};

export default ExpenseForm;
```



### Lifting State Up

- 자식 컴포넌트에서 부모 컴포넌트로 값 전달

예시 (ExpenseForm -> NewExpense)

```react
// ExpenseForm.js
import React, { useState } from "react";

import "./ExpenseForm.css";

// props로 부모에게 받음
const ExpenseForm = (props) => {
  const [enteredTitle, setEnteredTitle] = useState("");
  const [enteredAmount, setEnteredAmount] = useState("");
  const [enteredDate, setEnteredDate] = useState("");

  const titleChangeHandler = (event) => {
    setEnteredTitle(event.target.value);
  };
  const amountChangeHandler = (event) => {
    setEnteredAmount(event.target.value);
  };
  const dateChangeHandler = (event) => {
    setEnteredDate(event.target.value);
  };

  const submitHandler = (event) => {
    event.preventDefault();
    // 데이터 생성
    const expenseData = {
      title: enteredTitle,
      amount: enteredAmount,
      date: new Date(enteredDate),
    };
    props.onSaveExpenseData(expenseData); // 부모의 함수에 담아 생성한 데이터 전달
    setEnteredTitle("");
    setEnteredAmount("");
    setEnteredDate("");
  };

  return (
    <form onSubmit={submitHandler}>
      <div className="new-expense__controls">
        <div className="new-expense__control">
          <label>Title</label>
          <input type="text" value={enteredTitle} onChange={titleChangeHandler} />
        </div>
        <div className="new-expense__control">
          <label>Amount</label>
          <input type="number" value={enteredAmount} onChange={amountChangeHandler} />
        </div>
        <div className="new-expense__control">
          <label>Date</label>
          <input type="date" value={enteredDate} onChange={dateChangeHandler} />
        </div>
      </div>
      <div className="new-expense__actions">
        <button type="submit">Add Expense</button>
      </div>
    </form>
  );
};

export default ExpenseForm;
```

```react
// NewExpense.js
import React from "react";

import ExpenseForm from "./ExpenseForm";
import "./NewExpense.css";

const NewExpense = (props) => {
  // 자식이 넘긴 데이터를 enteredExpenseData로 받음
  const saveExpenseDataHandler = (enteredExpenseData) => {
    // 데이터 생성
    const expenseData = {
      ...enteredExpenseData,
      id: Math.random().toString(),
    };
    props.onAddExpense(expenseData); // 부모 App.js의 함수를 이용해 생성 데이터 전달
  };

  return (
    <div className="new-expense">
      {/* 자식에게 데이터를 받기 위해 함수 전달 */}
      <ExpenseForm onSaveExpenseData={saveExpenseDataHandler} />
    </div>
  );
};

export default NewExpense;
```



`Presentational Component` v `Stateful Component`

`Stateless Component` v `Stateful Component`

`Dumb Component` v `Smart Component`



---



### .map()

### `key` props

- 아이템 추가하면 맨 위에 추가되는데, HTML에서는 맨 아래에 추가됐다고 표시됨 (근데 다시 업데이트로 위로 감)

- React는 모든 목록을 체크해서 업데이트 -> 버그 발생할 수 있고, 성능 저하됨
- `key`를 사용해서 해결 (map 메서드의 index를 줄 수도 있지만, 권장하지 않음)

```react
// ExpenseList.js
import React from "react";

import ExpenseItem from "./ExpenseItem";
import "./ExpensesList.css";

const ExpensesList = (props) => {
  // props.items가 하나도 없으면 <h2></h2> 리턴
  if (props.items.length === 0) {
    return <h2 className="expenses-list__fallback">Found no expenses.</h2>;
  }

  // 하나라도 있으면 <ExpenseItem /> 리턴
  return (
    <ul className="expenses-list">
      {/* .map() 메서드 */}
      {props.items.map((expense) => (
        <ExpenseItem
          key={expense.id}
          title={expense.title}
          amount={expense.amount}
          date={expense.date}
        />
      ))}
    </ul>
  );
};

export default ExpensesList;
```



### 자식에게 받은 값으로 배열에 업데이트

잘못된 방법, 올바른 방법 구분하기

```react
// App.js
import React, { useState } from "react";

import NewExpense from "./components/NewExpense/NewExpense";
import Expenses from "./components/Expenses/Expenses";

const DUMMY_EXPENSES = [
  // ...
  { id: "e2", title: "New TV", amount: 799.49, date: new Date(2021, 2, 12) },
  // ...
];

const App = () => {
  const [expenses, setExpenses] = useState(DUMMY_EXPENSES);

  const addExpenseHandler = (expense) => {
    // setExpenses([expense, ...expenses]); // 잘못된 방법
    // 올바른 방법
    setExpenses((prevExpenses) => {
      return [expense, ...prevExpenses];
    });
  };

  return (
    <div className="App">
      <NewExpense onAddExpense={addExpenseHandler} />
      <Expenses items={expenses} />
    </div>
  );
};

export default App;
```



### filter (조건 필터링)

- `&&` 연산자를 이용
- 조건을 만족할 때 렌더링할 JSX content를 `&&` 뒤에 배치
- 아예 컴포넌트화하는 것을 추천

```react
// Expenses.js
import React, { useState } from "react";

import ExpensesList from "./ExpensesList";
import ExpensesFilter from "./ExpensesFilter";
import ExpensesChart from "./ExpensesChart";
import Card from "../UI/Card";
import "./Expenses.css";

const Expenses = (props) => {
  const [filteredYear, setFilteredYear] = useState("2020");

  const filterChangeHandler = (selectedYear) => {
    setFilteredYear(selectedYear);
  };

  const filteredExpenses = props.items.filter((expense) => {
    return expense.date.getFullYear().toString() === filteredYear;
  });

  return (
    <div>
      <Card className="expenses">
        <ExpensesFilter
          selected={filteredYear}
          onChangeFilter={filterChangeHandler}
        />
        <ExpensesChart expenses={filteredExpenses} />
        {/* {expensesContent} */}
        <ExpensesList items={filteredExpenses} />
        {/* 조건 만족하면 렌더링할 JSX content가 && 뒤에 옴 */}
        {/* {filteredExpenses.length === 0 && <p>No expenses found.</p>}
        {filteredExpenses.length > 0 &&
          filteredExpenses.map((expense) => (
            <ExpenseItem
              key={expense.id}
              title={expense.title}
              amount={expense.amount}
              date={expense.date}
            />
          ))} */}

        {/* {filteredExpenses.length === 0 ? (
          <p>No expenses found.</p>
        ) : (
          filteredExpenses.map((expense) => (
            <ExpenseItem
              key={expense.id}
              title={expense.title}
              amount={expense.amount}
              date={expense.date}
            />
          ))
        )} */}
      </Card>
    </div>
  );
};

export default Expenses;

```



### 조건부 렌더링

```react
// NewExpense.js
import React, { useState } from "react";

import ExpenseForm from "./ExpenseForm";
import "./NewExpense.css";

const NewExpense = (props) => {
  const [isEditing, setIsEditing] = useState(false);

  const saveExpenseDataHandler = (enteredExpenseData) => {
    const expenseData = {
      ...enteredExpenseData,
      id: Math.random().toString(),
    };
    props.onAddExpense(expenseData);
    setIsEditing(false);
  };

  const startEditingHandler = () => setIsEditing(true);

  const stopEditingHandler = () => setIsEditing(false);

  return (
    <div className="new-expense">
      {/* isEditing이 false */}
      {!isEditing && (
        <button onClick={startEditingHandler}>Add New Expense</button>
      )}
      {/* isEditing이 true */}
      {isEditing && (
        <ExpenseForm
          onSaveExpenseData={saveExpenseDataHandler}
          onCancel={stopEditingHandler}
        />
      )}
    </div>
  );
};

export default NewExpense;
```



### 간단한 숫자 변환

문자열 숫자 앞에 `+`를 붙임



---



## Conditional & Dynamic Styles

style을 태그에 주는 방법은 좋지 않음 (내용이 너무 길어짐)

동적으로 클래스를 지정할 수 있음

- `className={form-control ${!isValid ? 'invalid' : ''}}`



### Styled Components

`npm install --save styled-components`

```react
// Button.js
import styled from "styled-components";

const Button = styled.button`
  width: 100%;
  font: inherit;
  padding: 0.5rem 1.5rem;
  border: 1px solid #8b005d;
  color: white;
  background: #8b005d;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.26);
  cursor: pointer;

  @media (min-width: 768px) {
    width: auto;
  }

  &:focus {
    outline: none;
  }

  &:hover,
  &:active {
    background: #ac0e77;
    border-color: #ac0e77;
    box-shadow: 0 0 8px rgba(0, 0, 0, 0.26);
  }
`;

export default Button;
```

tagged template literal syntax

props 전달 가능

media query 적용 가능

`&`로 대체



### CSS Modules

```react
// CourseInput.js
import React, { useState } from "react";

import Button from "../../UI/Button/Button";

import styles from "./CourseInput.module.css";

const CourseInput = (props) => {
  const [enteredValue, setEnteredValue] = useState("");
  const [isValid, setIsValid] = useState(true);

  const goalInputChangeHandler = (event) => {
    if (event.target.value.trim().length > 0) {
      setIsValid(true);
    }
    setEnteredValue(event.target.value);
  };

  const formSubmitHandler = (event) => {
    event.preventDefault();
    if (enteredValue.trim().length === 0) {
      setIsValid(false);
      return;
    }
    props.onAddGoal(enteredValue);
  };

  return (
    <form onSubmit={formSubmitHandler}>
      <div
        className={`${styles["form-control"]} ${!isValid && styles.invalid}`}
      >
        <label>Course Goal</label>
        <input type="text" onChange={goalInputChangeHandler} />
      </div>
      <Button type="submit">Add Goal</Button>
    </form>
  );
};

export default CourseInput;
```

`import styles from "./???.module.css"`

`styles`는 객체



---





















