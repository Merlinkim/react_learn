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
      <h2 onClick={(event)=>{
        event.preventDefault();
        event.onChangeMode();
      }}>{props.title}</h2>
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
      <li onChangeMode={()=>{
        event.preventDefault();
        setMode('python');
      }}><a href='/python'>python</li>
      <li onChangeMode={()=>{
        event.preventDefault();
        setMode('React');
    }}><a href='/react'>React</li>
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

Create
무언가를 생성할려면 입력받아서 DB로 넘겨준다 혹은 입력받은 데이터를 리스트 혹은 array형태의 무언가에 담아두었다가 불러낼수 있어야한다.
```JSX
import logo from './logo.svg';
import './App.css';
import {useState} from 'react';

function Header(props){
  return (
    <header>
      <h1><a href="/" onClick={(event)=>{
        event.preventDefault();
        props.onChangeMode();
      }}>{props.title}</a></h1>
    </header>
      );
}

function Nav(props){
  const lis = []
  for(let i = 0;i < props.topics.length; i++){
    let t = props.topics[i]
    lis.push(
      <li key={t.id}>
      <a id={t.id} href={'/read/'+t.id} onClick={event=>{
        event.preventDefault();
        props.onChangeMode(Number(event.target.id));
      }}>{t.title}</a>
      </li>
      ) 
  }
  return(
      <nav>
        <ol>
          {lis}
        </ol>
      </nav>
    )
}

function Article(props){
  return(
      <article>
        <h2>{props.title}</h2>
        {props.body}
      </article>
  )
}

function Create(props){
  return(
    <article>
      <h2>Create</h2>
      <form onSubmit={event=>{
        event.preventDefault();
        const title = event.target.title.value;
        const body = event.target.body.value;
        props.onCreate(title,body);
      }}>
        <p><input type='text' name='title' placeholder='title'/></p>
        <p><textarea name='body' placeholder="body"></textarea></p>
        <p><input type="submit" value="Create"></input></p>
      </form>
    </article>
  )
}
function App() {
  const [mode,setMode]=useState('WELCOME');

  const [id,setId]=useState(null);
  const [nextId,setNextId]=useState(4);

  const [topics,setTopics] = useState([
      {id:1, title:'html',body:'html is ....'},
      {id:2, title:'css',body:'css is ....'},
      {id:3, title:'js',body:'js is ....'}
    ]);
  let content = null;
  if (mode === 'WELCOME'){
    content=<Article title="Welcome" body='Hello WEB'></Article>
  }else if (mode === 'read'){
    let title,body = null;
    for(let i=0; i<topics.length; i++){
      if(topics[i].id === id){
        title=topics[i].title;
        body=topics[i].body;
      }
    }
    content=<Article title={title} body={body}></Article>
  }else if (mode === 'CREATE') {
    content = <Create onCreate={(_title,_body)=>{
      const newTopic = {id:nextId, title:_title,body:_body};
      const newTopics = [...topics];
      newTopics.push(newTopic);
      setTopics(newTopics);
      setMode('READ');
      setId(nextId);
      setNextId(nextId+1);
    }}></Create>
  }
  return (
    <div>
      <Header title='WEB' onChangeMode={
        ()=>{
          setMode('WELCOME');
        }
      }></Header>
      <Nav topics={topics} onChangeMode={(_id)=>{
        setMode('read');
        setId(_id);
      }}></Nav>
      {content}
      <ul>
        <li><a href='/ceate' onClick={event=>{
          event.preventDefault();
          setMode('create');
        }}>create</a></li>
      </ul>
    </div>
  );
}

export default App;
```
<h3>코드 순서 설명</h3>
<ol>
  <li>App부분 App의 Create부분을 보면 mode를 state를 통해서 create로 바꾸게 된다면 Create compoent가 발생하게 된다..</li>
  <li>create compoent에서 sumbit event가 발생되면 event.target.title.value값과 event.target.body.value를 title과 body에 각각 저장하였다.</li>
  <li>다시 App부분의 Create를 보면 submit event로 저장된 title,body그리고 nextId state를 통해서 newTopic에다가 딕셔너리 형태로 저장하였다.</li>
  <li>원본데이터를 복제하여 복제된 원본데이터에 추가사항을 push해여 추가해주었다.</li>
  <li>Topics state에다가 복제된 원본 데이터를 원본데이터와 교체해주었다</li>
  <li>그리고 나서 현재의 아이디 값을 저장하기 위하여 setId state를 호출하여 nextId를 저장하였다</li>
  <li>다음 ID값을 위하여 setNextId state를 호출하여 nextId에 +1를하며 저장하였다</li>
</ol>
<br>
<h3>값을 복제하여 push한 이유<h3>
만약에 값을 복제하지 않고 state를 호출하여 객체 혹은 배열을 수정하여 함수를 호출하게 되면 HTML이 재렌더링 되지 않기 때문이다.
