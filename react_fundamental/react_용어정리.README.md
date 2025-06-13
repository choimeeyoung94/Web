element
- 리액트 애플리케이션을 구성하는 가장 작은 단위

React.createElement()를 사용해서 element를 만든다

ReactDOM.createRoot().render()를 사용해서 브라우저에 대상을 랜더링 해준다

랜더링
- ReactDOM 은 Element 와 그 자식 Element 를 이전의 Element 와 비교하고 변경된 부분만 업데이트 한다

JSX:
- React에서 UI를 정의하기 위해 사용하는 자바스크립트 확장 문법
- JSX 내부에서 {}를 사용하여 자바스크립트 변수, 연산, 함수 호출 주석 등을 넣을 수 있다
- 삼항 연산자, 논리 연산자 등을 사용해 조건에 따라 다른 내용을 렌더링 할 수 있다
React.Fragment
- 여러 요소를 그룹화 할때 사용하는 특수한 컴포넌트
컴포넌트
- 특정 기능이나 UI를 담당하는 독립적인 코드 블록
클래스형 컴포넌트
- React.Component를 상속 받아서 작성
```
  class ClassComp extends React.Component {
    
    render() {
      return <h1>Hello Class Component</h1>
    }
  }
  
```

함수형 컴포넌트
```
  const FunctionComp = () => {
    return (
        <>
          <div>Hello Function Component</div>
          <div>Nice to meet you</div>
        </>
          )
  }

```

props
- 리액트에서 컴포넌트 간에 데이터를 전달할 때 사용하는 객체
- 부모 컴포넌트가 자식 컴포넌트에게 데이터나 설정값을 넘겨줄때 사용된다
```
const NameCard1 = (props) => {
    return (
     <h1>
      <div>이름 {props.name}</div> 
      <div>연락처 {props.phone}</div> 
     </h1>
    )
}

 ReactDOM.createRoot(document.getElementById('root1')).render(
    <NameCard1 name={name} phone={phone}/>
 );
  

```

props drilling
- 하위 컴포넌트에 값을 연속해서 전달하는 방식
- React에서 상위 컴포넌트가 하위 컴포넌트로 데이터를 전달할 때 중간 컴포넌트들이 필요하지 않지만 props를 계속 전달해야 하는 상황
```
 const FinalComp = ({data}) => {
    return (
      <>
        <h1>I'm FinalComp</h1>
        <h1>{data}</h1>
      </>
    )
  }
  
  const ThirdComp = ({data}) => {
    return (
      <>
        <h1>I'm ThirdComp</h1>
        <FinalComp data={data}/>
      </>
    )
  }
  const SecondComp = ({data}) => {
    return (
      <>
        <h1>I'm SecondComp</h1>
        <ThirdComp data={data}/>
      </>
    )
  }
  
  const FirstComp = ({data}) => {
    return (
      <>
        <h1>I'm FirstComp</h1>
        <SecondComp data={data}/>
      </>
    )
  }
  const App = () => {
    const data = "Who needs me?"
    return (
      <>
        <FirstComp data={data}/>  
      </>
    )
  }
  
  ReactDOM.createRoot(document.getElementById('root2')).render(<App/>);
```

props children
- 컴포넌트를 호출할 때 전달한 내부 요소를 의미
```
  const GiftCard1 = (props) => {
    return (
      <>
        <h1>{props.children}</h1>
      </>
    )
  }
  const GiftCard2 = (props) => {
    const {children} = props;
    return (
      <h1>{children}</h1>
    )
  }

  const GiftCard3 = ({children}) => {
    return (
      <h1>{children}</h1>
    )
  }

ReactDOM.createRoot(document.getElementById('root3')).render([
  <GiftCard1>3만원</GiftCard1>, // props.children은 컴포넌트 태그 사이에 감싸진 내용을 참조할 수 있게 해주는 prop이다
  <GiftCard2>5만원</GiftCard2>,
  <GiftCard3><em>10만원</em></GiftCard3>,
]);
```

children
- 컴포넌트 안에 직접 넣은 내용 전체를 가리킨다
  const GiftCard1 = (props) => { //어떻게 돼지????
    return (
      <>
        <h1>{props.children}</h1>
      </>
    )
  }
  const GiftCard2 = (props) => {
    const {children} = props;
    return (
      <h1>{children}</h1>
    )
  }

  const GiftCard3 = ({children}) => {
    return (
      <h1>{children}</h1>
    )
  }

ReactDOM.createRoot(document.getElementById('root3')).render([
  <GiftCard1>3만원</GiftCard1>, // props.children은 컴포넌트 태그 사이에 감싸진 내용을 참조할 수 있게 해주는 prop이다
  <GiftCard2>5만원</GiftCard2>,
  <GiftCard3><em>10만원</em></GiftCard3>,
]);
```


