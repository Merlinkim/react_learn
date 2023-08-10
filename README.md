# react_learn
리액트는 나에게 무언가 제품을 이쁘게 만들기 위한 툴일 뿐 이것에 대하여 깊게 이해하기에는 
시간적 리소스가 적으므로 어찌해야 "쉽고" "간편하고" "빠르게" 사용 할것인가 에 대한 리포입니다.
<hr>
<br>
<h3>리액트를 시작하는 법</h3>
<ol>
  <li>download node.js for control the react</li>
  <li>npx create-react-app {file_route}</li>
  <li>npm start</li>
</ol>
그러면 리액트 서버 시작 됨
<br>
<br>
<ul>
<li>compoent</li>
compoent는 react의 구성의 최소 요소라고 생각하면 편할것이다.
<br>
<li>props</li>
어떠한 값을 컴포넌트에게 전달할때 사용됨.

<li>state</li>
상태관리를 위한 함수내부의 객체.
</ul>
그렇다면 props는 denfine parameter라고 생각하고 state는 React의 상태관리 객체라고 생각하자.<br>
<hr>
props의 사용법<br>

```JSX
function Defi(props){
  return(
    <div>
      <h2>{props.title}</h2>
      {props.context}
    </div>
  )
}
function App(){
  return(
    <Defi title='hello' context='my react'></Defi>
  )
}
```
위의 내용에서는 Defi라는 컨포넌트에 props를 사용하도록 지정하였고 App에서 title를 'hello' context를 'my react'f라고 지정한 것이다.<br>
<hr>
state의 사용법<br>

```JSX
function Defi(props){
  return(
    <div>
      <h2>{props.title}</h2>
      {props.context}
    </div>
  )
}
function App(){
  const [mode,setMode]=useState('hello');
  return(
    let contents=null;
    if (mode == 'react' ){
      contents=<Defi title='hello' context='my react'></Defi>
    }else if (mode === 'python'){
    contents=<Defi title='hello' context='my python'></Defi>
    <ul>
      <li onChangeMode={()=>{setMode('python');}}><a href='/python'>python</li>
      <li onChangeMode={()=>{setMode('React');}}><a href='/react'>React</li>
    </ul>
    {contents}
    }
  )
}
```
위의 내용을 봐보면 li태그에 들어있는 a를 누르게 되면 state의 정보가 변경되면서 contents가 변경되는 구조이다<br>
<hr>
<br>
기초 CRUD
