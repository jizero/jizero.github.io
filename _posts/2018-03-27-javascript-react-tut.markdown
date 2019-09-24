---
layout: post
title:  "[react] 틱택토 게임 만들기"
date:   2019-04-30 10:00
author: jizero
tags:	[javascript,'react','esnext']
img:  201909/tt.png # Add image post (optional)
---


## 시작하며
리액트 튜토리얼 사이트에 기재된 틱택토 게임을 번역및 재구성한 내용입니다.
[https://reactjs.org/tutorial/tutorial.html](https://reactjs.org/tutorial/tutorial.html)


## 틱택토 게임이란
[https://namu.wiki/w/틱택토](https://namu.wiki/w/%ED%8B%B1%ED%83%9D%ED%86%A0)

## 공부 할것
1. component
2. props state
3. keys
4. ES6코드 분석
5. 게임 정리
6. 응용해보기

# Component

컴포넌트를 만들때는 React.Component 클래스를 상속하여 만듭니다.

<img src="/assets/img/201909/tic0.png" />

    
    class Square extends React.Component {
      render() {
        return (
          <button className="square">
          </button>
        );
      }
    }
    
    
    class Board extends React.Component {
      render() {
        const status = 'Next player: X';
        return (
          <div>  
          </div>
        );
      }
    }
    
    class Game extends React.Component {
      render() {
        return (
          <div className="game">
          </div>
        );
      }
    }
    
    // ========================================
    
    ReactDOM.render(
      <Game />,
      document.getElementById('root')
    );
    

함수형 컴포넌트

React는 render 메서드만으로 구성된 Square와 같은 컴포넌트 타입을 위해 함수형 컴포넌트라 불리는 간단한 문법을 지원합니다. React.Component를 확장한 클래스를 정의하는 것보다 간단하게 props를 가져오고 랜더링 해야할 것을 반환하는 함수를 작성하는 것이 좋다.

    function Square(props) {
      return (
        <button className="square" onClick={props.onClick}>
          {props.value}
        </button>
      );
    }
    

- 게임에 적용해보기

<img src="/assets/img/201909/tic2.png" />

[https://codepen.io/gaearon/pen/oWWQNa?editors=0010](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)

[https://reactjs.org/tutorial/tutorial.html#function-components](https://reactjs.org/tutorial/tutorial.html#function-components)

[https://codesandbox.io/s/8zwr65y98](https://codesandbox.io/s/8zwr65y98)

# Props

---

[https://medium.com/@umioh1109/react-es6-class-constructor에서의-super-9d53ba0611d9](https://medium.com/@umioh1109/react-es6-class-constructor%EC%97%90%EC%84%9C%EC%9D%98-super-9d53ba0611d9)

 

- 게임에 적용해보기

[https://reactjs.org/tutorial/tutorial.html#passing-data-through-props](https://reactjs.org/tutorial/tutorial.html#passing-data-through-props)

[https://codepen.io/gaearon/pen/aWWQOG?editors=0010](https://codepen.io/gaearon/pen/aWWQOG?editors=0010)

# State

---

컴포넌트에서 관리하는 상태 값으로 유동적인 데이터를 다룰 때, state 를 사용한다. state는 변경이 가능하고 변경할 때는 setState메서드를 사용해 상태를 변경한다. setState는 비동기로 동작하며 동작완료에 대한 콜백을 설정할 수 있다.

    class Button extends React.Component {
      constructor() {
        super();
        this.state = {
          count: 0
        };
      }
    
      updateCount = () => {
        this.setState({ count: this.state.count + 1 });
      }
    
      render() {
        return (
          <button onClick={this.updateCount}>
            Clicked {this.state.count} times
          </button>
        );
      }
    }

[https://codesandbox.io/](https://codesandbox.io/)

[https://reactjs.org/tutorial/tutorial.html#why-immutability-is-important](https://reactjs.org/tutorial/tutorial.html#why-immutability-is-important)

- 게임에 적용해보기

[](https://www.notion.so/ef6feac14ddf4743bb5bf3ab9f1bdbd3#cc7fa5b0fa604ec1855df5dd7d91f94d)

[https://reactjs.org/tutorial/tutorial.html#making-an-interactive-component](https://reactjs.org/tutorial/tutorial.html#making-an-interactive-component)

[https://codepen.io/gaearon/pen/VbbVLg?editors=0010](https://codepen.io/gaearon/pen/VbbVLg?editors=0010)

# Key

---

React.js의 Virtual DOM 구현의 내에서도 유저가 인지할 수 있는 Key

### **key must by unique**

위 경고로 알 수 있듯이 key는 해당 리스트에서 반드시 유니크한 값으로 지정할 필요가 있습니다. 예를 들어 사용자 목록을 출력한다면 사용자의 ID가 key로 사용될 수 있습니다. 배열의 index를 key로 지정하는 것은 사실 큰 의미가 없습니다.

    
          return (
            <li key={move}>
              <button onClick={() => this.jumpTo(move)}>{desc}</button>
            </li>
          )

- 게임에 적용해보기

[https://reactjs.org/tutorial/tutorial.html#showing-the-past-moves](https://reactjs.org/tutorial/tutorial.html#showing-the-past-moves)

# es6

---

승자찾기

const [a, b, c] = lines[i];

    function calculateWinner(squares) {
    const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
    ];
    for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
    return squares[a];
    }
    }
    return null;
    }

[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

- 게임에 적용해보기

[https://reactjs.org/tutorial/tutorial.html#declaring-a-winner](https://reactjs.org/tutorial/tutorial.html#declaring-a-winner)

[https://codepen.io/gaearon/pen/LyyXgK?editors=0010](https://codepen.io/gaearon/pen/LyyXgK?editors=0010)

이동 기록하기 - 화살표함수

    const moves = history.map((step, move) => {
          const desc = move ?
            'Go to move #' + move :
            'Go to game start';
          return (
            <li><button onClick={() => this.jumpTo(move)}>{desc}</button></li>);
        });

    var array1 = [1, 4, 9, 16];
    
    // pass a function to map
    const map1 = array1.map(x => x * 2);
    
    console.log(map1);
    // expected output: Array [2, 8, 18, 32]

[https://es6console.com/](https://es6console.com/)

- 게임에 적용해보기

[https://reactjs.org/tutorial/tutorial.html#lifting-state-up-again](https://reactjs.org/tutorial/tutorial.html#lifting-state-up-again)

# 틱택토게임 정리

---

기본컴퍼넌트 만들기

이벤트 핸들러 

클릭시 플레이어 추가하기

승자알려주기

히스토리추가하기

# 응용하기

---

calculateWinner 부분을 수정하여 빙고가완성된 칸에 색을 칠해보자

[https://codepen.io/gaearon/pen/gWWZgR?editors=0010](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)