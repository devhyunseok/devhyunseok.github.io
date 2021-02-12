---
date: "2019-10-08T13:00:00.121Z"
title:  "[React] Redux, React-Redux"
slug: "[React] Redux, React-Redux"
author: Hyunseok
template: "post"
category: "Frontend"
description: ""
tags:
- "Frontend"

---

## Redux, React-Redux

리액트로 개발을 하면서 컴포넌트를 조합하다보면,
**`컴포넌트간에 상하관계가 트리형태로 구성`**이 됩니다.

![image.png](/assets/frontend/redux-tree-001.png)

**컴포넌트가 중첩되어갈 수록 Tree가 깊어지고, 
컴포넌트간 데이터 전달에 문제가 발생합니다.**

이 과정에서 많은 콜백이 중첩되고 반복적인 코드가 생성되게 됩니다.

![image.png](/assets/frontend/redux-tree-002.png)

이러한 컴포넌트간 데이터 전달을 위해 **`Redux라는 상태관리 라이브러리`**를 사용할 수 있습니다.

**Redux**는 컴포넌트 트리 바깥에 하나의 **중앙 저장소**를 두어
**어플리케이션 전역의 데이터를 관리하는 라이브러리**입니다.

## Flux

Redux를 이야기하기전에 먼저 Flux 패턴을 알아야합니다.

Flux 패턴은 페이스북에서 발표한 단방향 데이터 처리 아키텍처로 
MVC 모델의 복잡성을 개선하기 위해 나왔습니다.

![image.png](/assets/frontend/flux-mvc.png)

위의 이미지와 같이 Model과 View 사이에 양방향 통신이 이루어지는 MVC는 
프로젝트가 커질수록 **모델과 뷰 사이의 복잡성이 증가**하는 단점이 있었습니다.

![image.png](/assets/frontend/flux.png)

이를 개선한 Flux 패턴의 경우 양방향 통신으로 생기는 복잡도를 **단방향 통신**으로 바꾸어 상태값이 변경되었을때 **View가 자동적으로 갱신**되게 구성하였습니다.

데이터 흐름의 순서대로 살펴보면

1. **Action 객체를 통해 행위와 데이터를 전달**합니다.
2. Dispatcher는 요청된 **Action으로 어떠한 Store를 갱신할지 결정**합니다.
3. Store에서는 어플리케이션의 **이전 상태 데이터와 현재 상태 데이터를 병합하고 상태를 갱신**합니다.
4. Store에서 갱신된 데이터는 **View로 전달되어 화면에 반영**됩니다.

## Redux

**`Redux는 Flux 아키텍처를 기반으로한 구현체입니다.`**

![image.png](/assets/frontend/redux.png)

**Flux**에서는 어플리케이션 하나에 **여러 스토리지**를 가질 수 있지만,
**Redux**에서는 **하나의 스토리지로 제한**하였습니다.

대신, 다수의 Reducer를 두어 **상태 변경 로직은 Reducer로 위임**,
실제 상태 값이 결합 되는 부분은 Store에서 이루어지고 
해당 코드는 라이브러리에서 처리하여 코드 구현을 단순화 하였습니다.

## React, Redux Todo App

[Redux 홈페이지](https://deminoth.github.io/redux/basics/ExampleTodoList.html)에 나와있는 **TODO 앱**을 **`Typescript + React Hooks`**과 함께 조합하여 구현한 예시입니다.

해당 예제에서는 **Typescript**를 사용하였으며 Create-React-App을 이용하여 생성하는 명령어는 다음과 같습니다. (Node.js가 설치가 되어있어야 합니다.)
```
npx create-react-app [프로젝트명] --typescript 
```

우선 Create-React-App 으로 생성한 프로젝트에
Redux를 사용하기 위해 라이브러리를 추가해줍니다.
```
npm install —save redux react-redux
```

```
"dependencies": {
  "@types/jest": "24.0.18",
  "@types/node": "12.7.11",
  "@types/react": "16.9.5",
  "@types/react-dom": "16.9.1",
  "react": "16.10.2",
  "react-dom": "16.10.2",
  "react-redux": "7.1.1",
  "react-scripts": "3.2.0",
  "redux": "4.0.4",
  "typescript": "3.6.3"
}
```

---
**폴더 구조는 아래와 같습니다.**

![스크린샷 2019-10-07 오후 4.50.28.png](/assets/frontend/redux-folder-tree.png)

**리액트 컴포넌트의 경우 Components** 하위에 구성되어 있고
**리덕스 구현에 필요한 Actions, ActionTypes, Reducer의 경우 Modules**하위에 구성되어 있습니다.

* Actions, ActionTypes, Reducer를 각각의 파일로 분리하여 개발하는 예시가 많은 걸로 알고 있습니다.
* 개발을 하다보니 개인적으로 ActionType의 경우 Reducer와 Actions에서 주로 사용하게 되며, Reducer와 Action이 아닌 다른 곳에서는 ActionType을 직접 접근하지않고 Action을 이용하는게 맞다고 생각하여 세가지 파일을 하나의 파일로 구성하였습니다.
* 이러한 구조를 **`Ducks 패턴`**이라고 한다고 합니다.

---
우선 **index.tsx** 파일입니다.

### index.tsx
```
import React from 'react';
import {createStore} from 'redux';
import {Provider} from 'react-redux';
import ReactDOM from 'react-dom';
import App from './App';
import combineReducers from './combineReducers';

const store = createStore(combineReducers);

ReactDOM.render(
  <Provider store={store}>
    <App/>
  </Provider>,
  document.getElementById('root')
);
```

**react-redux**에서 제공하는 **Provider** 컴포넌트를 사용하여,
Store 객체를 명시적으로 컴포넌트로 넘겨주지 않아도 App 컴포넌트를 포함한 하위 컴포넌트에서 Store에 접근 할 수 있게 해주고 있습니다.

---
다음은 다수의 reducer 함수들을 Store에 넘길수 있게 하나의 reducer 함수로 만들어주는 **combineReducers.ts** 입니다.

### combineReducers.ts
```
import { combineReducers } from 'redux';
import todos from "./modules/todoModules";
import visibilityFilter from "./modules/filterModules";

const todoApp = combineReducers<any>({
  visibilityFilter: visibilityFilter,
  todos: todos
});

export default todoApp;
```

Flux 패턴이 서로 다른 상태를 관리하기 위해 여러 스토어를 두는 것처럼,
Redux에서는 **하나의 스토어에 다수의 Reducer를 두어 논리적으로 상태 분리**를 합니다.

---
다음은 어플리케이션의 중심인 App.tsx 파일입니다.

### App.tsx
```
import React, { Fragment } from 'react';
import {useDispatch, useSelector} from "react-redux";
import {addTodo, completeTodo} from "./modules/todoModules";
import {setVisibilityFilter} from "./modules/filterModules";
import TodoList from "./components/TodoList";
import Filter from "./components/Filter";
import {ITodo} from "./components/Todo";
import AddTodo from "./components/AddTodo";

function selectTodos(todos: [ITodo], filter: 'SHOW_ALL' | 'SHOW_COMPLETED' | 'SHOW_ACTIVE') {
  switch (filter) {
    case 'SHOW_COMPLETED':
      return todos.filter(todo => todo.completed);
    case 'SHOW_ACTIVE':
      return todos.filter(todo => !todo.completed);
    default:
      return todos;
  }
}

const App: React.FC = () => {
  const visibleTodos = useSelector((state: any) => selectTodos(state.todos, state.visibilityFilter));
  const visibilityFilter = useSelector((state: any) => state.visibilityFilter);
  const dispatch = useDispatch();

  return (
    <Fragment>
      <Filter
        filter={visibilityFilter}
        onFilterChange={nextFilter =>
          dispatch(setVisibilityFilter(nextFilter))
        }/>
      <AddTodo
        onAddClick={text =>
          dispatch(addTodo(text))
        }/>
      <TodoList
        todos={visibleTodos}
        onTodoClick={index =>
          dispatch(completeTodo(index))
        }/>
    </Fragment>
  );
};

export default App;
```

[Redux 홈페이지](https://deminoth.github.io/redux/basics/ExampleTodoList.html)에 나와있는 클래스 컴포넌트 형식보다는 **React 16.8에서 정식으로 추가 된 React-Hook**를 사용한 예시가 더 도움이 될 거라 생각하여 **React-Hook**을 사용하였습니다.

클래스 컴포넌트와 다른 점은 connect 함수를 사용하여,
Redux와 컴포넌트를 연결하는 부분을 **React-Hook**에서는 **`useSelector, useDispatch`**를 사용합니다.

**useSelector의 경우 스토어에서 상태값을 불러올때 사용하며,
useDispatch의 경우 스토어로 액션을 발생시킬때 사용합니다.**

---
다음으로 Reducer와 Action, ActionTypes가 정의 되어있는 modules 코드 입니다.

### todoModules.ts
```
/*
 * action types
 */
const ADD_TODO = 'ADD_TODO';
const COMPLETE_TODO = 'COMPLETE_TODO';

/*
 * action creators
 */
export function addTodo(text: string) {
  return { type: ADD_TODO, text };
}
export function completeTodo(index: number) {
  return { type: COMPLETE_TODO, index };
}

/*
 * reducer
 */
const todos = (state = [], action: any) => {
  switch (action.type) {
    case ADD_TODO:
      return [...state, {
        text: action.text,
        completed: false
      }];
    case COMPLETE_TODO:
      return [
        ...state.slice(0, action.index),
        Object.assign({}, state[action.index], {
          completed: true
        }),
        ...state.slice(action.index + 1)
      ];
    default:
      return state;
  }
};

export default todos;
```

### filterModules.ts
```
/*
 * action types
 */
const SET_VISIBILITY_FILTER = 'SET_VISIBILITY_FILTER';

/*
 * action creators
 */
export function setVisibilityFilter(filter: string) {
  return { type: SET_VISIBILITY_FILTER, filter };
}

export const VisibilityFilters = {
  SHOW_ALL: 'SHOW_ALL',
  SHOW_COMPLETED: 'SHOW_COMPLETED',
  SHOW_ACTIVE: 'SHOW_ACTIVE'
};

/*
 * reducer
 */
const visibilityFilter = (state = VisibilityFilters.SHOW_ALL, action: any) => {
  switch (action.type) {
    case SET_VISIBILITY_FILTER:
      console.log(action.filter);
      return action.filter;
    default:
      return state;
  }
};

export default visibilityFilter;
```

**`(1. Action)`** 미리 정의해 둔 Action을 컴포넌트에서 Dispatch 하면,
Reducer를 탐색하며 Action의 type이 맞는 부분을 찾습니다.

**`(2. Reducer)`** Reducer의 Action type이 일치한 부분이 실행되고 반환되는 값은 Store에 변경된 값이 반영됩니다. 

**`(3. Store)`** Store에서는 전달된 변경된 값을 반영하고, 
Store의 State는 Props의 형태로 React Component로 전달하며 
**`(4. UI)`** React는 상태값에 기반하여 화면을 다시 렌더링하게 됩니다. 

---
마지막으로 Components 하위에 있는 Todo App 컴포넌트 코드입니다.

### TodoList.tsx
```
import React from 'react';
import Todo, {ITodo} from './Todo';

export interface ITodoList {
  todos?: ITodo[],
  onTodoClick: (index: number) => void;
}

const TodoList = (props: ITodoList) => {
  const { todos, onTodoClick} = props;

  return (
    <ul>
      {todos && todos.map((todo, index) => (
        <Todo key={index} {...todo} onClick={() => onTodoClick(index)}/>
      ))}
    </ul>
  )
};

export default TodoList
```

### Todo.tsx
```
import React from 'react';

export interface ITodo {
  onClick: (e: React.MouseEvent<HTMLLIElement>) => void;
  completed: boolean;
  text: string;
}

const Todo = (props: ITodo) => {
  const { onClick, completed, text } = props;

  return (<li
    onClick={onClick}
    style={{
      textDecoration: completed ? 'line-through' : 'none'
    }}
  >
    {text}
  </li>)
};

export default Todo;
```

### Filter.tsx
```
import React from 'react';

interface IFilter {
  onFilterChange: (filter: string) => void,
  filter: 'SHOW_ALL' |
    'SHOW_COMPLETED' |
    'SHOW_ACTIVE'
}

const Filter = (props: IFilter) => {
  function renderFilter(filter: string, name: string) {
    if (filter === props.filter) {
      return name;
    }

    return (
      <a href='#' onClick={e => {
        e.preventDefault();
        props.onFilterChange(filter);
      }}>
        {name}
      </a>
    );
  }

  return (
    <p>
      Show:
      {' '}
      {renderFilter('SHOW_ALL', 'All')}
      {', '}
      {renderFilter('SHOW_COMPLETED', 'Completed')}
      {', '}
      {renderFilter('SHOW_ACTIVE', 'Active')}
      .
    </p>
  )
};

export default Filter
```

### AddTodo.tsx
```
import React, {useRef} from 'react';

interface IAddTodo {
  onAddClick: (text: string) => void;
}

const AddTodo = (props: IAddTodo) => {
  const { onAddClick } = props;
  const inputTextRef = useRef<HTMLInputElement>(null);

  function handleClick(e: React.MouseEvent<HTMLButtonElement>) {
    const inputText = inputTextRef.current;

    if(inputText) {
      const text = inputText.value.trim();
      onAddClick(text);
      inputText.value = '';
    }
  }

  return (
    <div>
      <input type='text' ref={inputTextRef} />
      <button onClick={(e) => handleClick(e)}>
        Add
      </button>
    </div>
  );
};

export default AddTodo;
```
