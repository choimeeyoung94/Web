#### element
- 리액트 애플리케이션을 구성하는 가장 작은 단위
- React.createElement()를 사용해서 element를 만든다


#### 랜더링
- 컴포넌트가 반환하는 UI 요소를 기반으로 사용자 화면을 구성하거나 갱신하는 과정을 의미한다
- ReactDOM 은 Element 와 그 자식 Element 를 이전의 Element 와 비교하고 변경된 부분만 업데이트 한다
- ReactDOM.createRoot().render() 메소드를 사용하여 브라우저에 대상을 랜더링 해준다

#### JSX
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

#### props
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

#### props drilling
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

#### key
- 브라우저에 리스트 렌더링 할때 각 항목을 식별하기 위해 key를 사용한다
- 리스트의 각 항목에 key가 없으면 어떤 요소가 변경, 추가, 삭제되었는지 정확히 파악하기 어렵다
- 각 리스트의 key는 고유한 값이어야 한다
예시코드
- item들을 식별하기 위해 배열의 인덱스가 key값으로 사용되었다
```
  const ListItemComp = ({item}) => {
    return (
      <li>
          {
            item
          }
      </li>
    )
  }
  {
    const Listcomp = ({items}) => {
      return (
        <ul>
          {
            items.map((item, i) =>  <ListItemComp item={item} key={i}/>)
          }
        </ul>
      )
    }

    const names = ["Alice", "Jessica", "Tommy", "John", "Eric"];
    ReactDOM.createRoot(document.getElementById('root2')).render(<Listcomp items={names}/>);
  }


```

#### event
- 사용자가 웹 브라우저에서 DOM 요소와 상호작용할 때 발생하는 사건을 의미한다
- 리액트 이벤트는 브라우저의 기본 이벤트를 감싸는 합성 이벤트이다

#### event 핸들러
- 이벤트 핸들러는 이벤트 발생 시 실행할 코드를 작성해 놓은 함수이다

1. 콜백함수를 이용하여 이벤트 핸들러를 직접 작성하는 방법
```
const EventComp1 = () => {
      return (
        <button onClick={() => alert('EventComp1')}>버튼1</button>
      )
    }

    ReactDOM.createRoot(document.getElementById('root1')).render(<EventComp1/>);


```

2. 이벤트 핸들러를 별도로 작성해서 onClick 속성으로 전달하는 방법
- onClickHandler를 컴포넌트 내부에서 직접 정의
- 이 컴포넌트는 고정된 동작만 할 수 있다
- 외부에서 onClick 동작을 변경할 수 없어서 재사용성이 낮다
```
 const EventComp2 = () => {
      
      const onClickHandler = (e) => {
        alert('EventComp2');
      }

      return (
        <button onClick={onClickHandler}>버튼2</button>
      )
    }

    ReactDOM.createRoot(document.getElementById('root2')).render(<EventComp2/>);
```

3. 이벤트 핸들러를 컴포넌트로 전달하는 방법
- onClickHandler를 컴포넌트 외부에서 정의하고 props로 전달하는 방식
- 컴포넌트는 버튼 UI만 제공하고 버튼의 동작은 외부에서 결정된다
- 이벤트 핸들러의 재사용성이 높아지고 여러 상황에 맞춰 다양한 핸들러를 전달할 수 있다다
```
const EventComp3 = ({onClickHandler}) => {

      return (
        <button onClick={onClickHandler}>버튼3</button>
      )
    }

    // 이벤트 핸들러
    const onClickHandler = (e) => {
      alert('EventComp3');
    }


    ReactDOM.createRoot(document.getElementById('root3')).render(<EventComp3 onClickHandler={onClickHandler}/>);
```

#### state
- state는 컴포넌트 내부에서 관리되는 동적인 데이터를 의미한다

### 컴포넌트
- 특정 기능이나 UI를 담당하는 독립적인 코드블록

### 클래스형 컴포넌트에서 state를 선언 및 초기화 하는 방법
- 클래스형 컴포넌트에서는 state를 객체 형태로 선언한다
```
  class Spin1 extends React.Component {
      ...

      // state의 선언 및 초기화
      state = {
        number: 0,
      }

      ...
    }




```

- 생성자를 이용해서 state 선언 및 초기화
- 생성자에서 this.state로 초기화한다
- state의 값을 변경할 때는 this.setState() 메소드를 사용한다
- setState() 메소드를 호출하면 리액트가 변경을 감지해서 컴포넌트를 리렌더링 해준다

```
class Spin2 extends React.Component {

    // 생성자를 이용한 state 선언및 초기화
    constructor(props) {
      super(props); // React.Component
      this.state = {
        number: 0,
      };
    }

    ...
  }
```

- 증가 버튼을 클릭하면 increaseHandler 함수의 this.setState() 메소드가 호출되어 이전 상태 값을 1 증가시킨 후 브라우저에 리랜더링 된다
- - 객체 안에 number key값이 1 증가된다
- 감소 버튼을 클릭하면 decreaseHandler 함수의 this.setState() 메소드가 호출되어 이전 상태 값을 1 감소시킨 후 브라우저에 리랜더링 해준다
- - 객체 안에 number key값이 1 감소된다
```
 class Spin2 extends React.Component {

    // 생성자를 이용한 state 선언및 초기화
    constructor(props) {
      super(props); // React.Component
      this.state = {
        number: 0,
      };
    }

    // 증가용 이벤트 핸들러
    increaseHandler = () => {
      this.setState((prevState) => {
        return {
          number: prevState.number + 1
        }
      })
    }

    decreaseHandler = () => {
      this.setState((prevState) => {
        return {
          number: prevState.number - 1
        }
      })
    }
    
    render() {
      const { number } = this.state;
      return (
        <>
          <h1 style={{ color: number === 0 ? 'black' : number > 0 ? 'red' : 'blue'}}>{number}</h1>
          <button onClick={this.increaseHandler}>▲</button>
          <button onClick={this.decreaseHandler}>▽</button>
        </>
      )
    }
  ```

#### 라이프사이클
- 컴포넌트가 생성되고 화면에 나타났다가 제거되기까지의 전체 과정을 말한다

### 라이프사이클 3단계
1. Mounting(마운트) : 컴포넌트가 생성되어 DOM에 삽입될 때
2. Updating (업데이트) : props나 state가 변경되어 다시 렌더링될 때
3. Unmounting (언마운트) : 컴포넌트가 DOM에서 제거될때


