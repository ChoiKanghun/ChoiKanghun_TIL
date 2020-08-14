# Hooks



훅은 리액트의 비교적 최신의, 편리한 기능이다. state, component에 대해 많은 것이 훅에 의해 대체될 정도로.  

결론적으로 말하면 react hook 은 function component 에서 state를 가질 수 있게 해주는 것이다.   

더불어 리액트 훅을 통해 무언가를 만든다면 didMount, render 같은 것들을 안해도 된다는 뜻이다. (!)  

모든 것이 하나의 function이 되니까. 





예를 들어 다음과 같은 (기존의) 코드가 있다 하자. 





```jsx
class App extends Component {
  state = {
    count: 0
  };

	modify = n => {
    this.setState({
      count: n
    });
  }
  
  render() {
    const { count } = this.state;
    return (
    	<>
      	<div>{count}</div>
      	<button onClick={()=>this.modify(count + 1)}> +1 </button>
      </>
    )
  }
}
```





위와 같은 함수를 훅스로 바꾼다면?! 

다음과 같은 형태가 된다. 





```jsx
const App = () => {
  const [count, setCount] = useState(0);
  return (
  	<>
    	{count}
    	<button onClick={() => setCount(count + 1)}> +1 </button>
    </>
  )
}
```





아직은 훅스에 대해 익숙하지는 않지만 코드가 정말 간결해졌다 ! 

위 코드를 정말 간단하게 설명하자면 useState 가 리액트 state 매니지먼트 밑으로 들어가서 훅을 가져오는 거다.

Hooks에는 useState 외에도 여러 가지가 있다. useState부터 천천히 알아보자. 





# List of Hooks



Hooks에서 크게 알아둬야 할 것으로는 세 가지 개념이 있다. 

`useState`, `useEffect`, `useRef` 

가 그것이다. 





해당 개념들을 배워보고, 해당 개념들을 사용하여 어떻게 활용하는지도 살펴보자. 

아래의 순서를 따를 것이다. (체크 박스가 활용.) 





#### useState

- [ ] useInput
  - input 역할을 함.
- [ ] useTabs
  - 웹사이트에 메뉴 또는 무엇이든 간에 tab을 사용하기 쉽게 만들어줌.

#### useEffect, useRef

- [ ] usePageLeave
  - 사용자가 페이지를 떠날 때 함수를 실행.
- [ ] useClick
  - element를 클릭하는 시점에 실행.
- [ ] useFadeIn
  - 어떤 element든 상관없이 애니메이션을 element 안으로 서서히 사라지게 만듦.
- [ ] useFullScreen
  - useFullScreen은 어떤 element든 풀스크린으로 만들거나 일반화면으로 돌아가게 할 수 있음.
- [ ] useHover
  - 어떤 요소에 마우스를 올렸을 때 이벤트 발생
- [ ] useNetwork
  - Online인지 Offline인지 감지.
- [ ] useNotification
  - notification API를 사용할 때 유저에게 알림을 보내줌.
- [ ] useScroll
  - 스크롤을 사용할 때를 감지.
- [ ] usePreventLeave
  - 유저가 변경사항을 저장하지 않고 페이지를 벗어나길 원할 때 확인.
- [ ] useConfirm
  - usePreventLeave와 비슷. 어떤 함수든 적용할 수 있다는 특징.
- [ ] useAxios
  - axios를 위한 wrapper





# CodeSandBox





코드를 만지기 위해 지금까지 VS Code를 사용했지만, 이번 Hooks 과정을 정리할 때에는 CodeSandbox를 사용하려고 한다. CodeSandBox는 test용 사이트를 만들 수 있는 꽤 좋은 웹사이트이다. 

https://codesandbox.io/index2





0805_1.jpg





codesandbox에서 react를 하나 만들면 위와 같은 화면이 뜬다. 그리고 command(control) + s 를 누르면 url에 이상한 문구가 추가되는데, 이것을 일단 바꿔주자. 왼쪽 바에서 상자모양을 클릭하고, 연필모양을 눌러 'Nooks' 정도로 고쳐준다.







# useState

useState를 사용하기 위해서는 react로부터 import 부터 해주어야 한다. 

import React from "react" 라고 적어왔던 부분을 

`import React, { useState } from "react";` 로 고쳐 사용하면 된다. 





useState는 다음과 같은 형태를 가지며, 두 가지 값을 기본적으로 가진다. 

`const [item, setItem]  = useState(1)` 

`[ ]` 안에 들어가는 첫 번째 값은 state 필드이다. 두 번째는 그것의 값을 설정하는 함수 이름. 

그리고 useState의 괄호 안에 들어가는 값은 첫 번째 필드(item)의 초기값이다. 

참고로 item과 setItem 모두 이름 변경이 가능하다. item은 말 그래도 그냥 원하는 변수명으로 고치면 되고, setItem은 item을 위한 것이라는 의미에서 통상 set변수명 과 같은 형태로 사용하는 것이다. 





만약 위와 같은 상황에서 item 하나만 사용할 거라면 다음과 같이 바꿔쓸 수도 있다. 

`const item = useState(1)[0]` 





아무튼 어떤 방식으로든 선언을 해주었다면 해당 함수 내에서는 우리가 선언한 변수들을 사용할 수 있다. 

다음과 같이 말이다. 





```jsx
function App() {
  const [item, setItem] = useState(1);
  return (
  	<div>
    	<h1>Hello { item }</h1>
    </div>
  )
}
```





그렇다면 setItem은 어떤 형식으로 사용할 수 있을까? 

이것 또한 예제를 통해 살펴보자. 

(Arrow function을 활용했다. ) 





```jsx
const App = () => {
  const [item, setItem] = useState(1);
  const incrementItem = () => setItem(item + 1);
  //item을 set하는데 무엇으로 set하냐면 괄호 안의 값으로 set한다.
  return (
   <div>
     	<h1>Hello {item}</h1>
    	<button onClick={incrementItem}>Increment</button>
    </div>
  )
}
```







여기서 우리가 알 수 있는 것은 hooks를 통해 function component 에서도 state를 사용할 수 있게됐다는 것. 

그리고 class component에서 state에 접근하기 위해 `this` 키워드를 사용하고, 또 render 함수에 넣어주는 불편함을 덜었다는 것이다. 





# UseInput





useInput은 input을 보다 효율적으로 사용하는 데에 활용할 수 있다. 

여러 가지 설명 방식을 생각해보았지만, 예제를 통해 배우는 것이 가장 빠르게 파악할 수 있는 방법이라고 생각해 먼저 예시를 들겠다. 





```jsx
import React, { useState } from "react";
import "./styles.css";

const useInput = initialValue => {
  const [value, setValue] = useState(initialValue);
  return { value };
};

const App = () => {
  const name = useInput("Mr.");
  return (
    <div>
      <h1>Hello</h1>
      <input placeholder="Name" value={name.value} />
      <input placeholder="Name2" {...name} />
    </div>
  );
};

export default App;

```





먼저 봐야 할 것은 App 내부이다. App 내부에서 name 에 useInput("초깃값") 을 대입했다. 초깃값은 "Mr." 이다. 

그리고 return 문 안에서 input의 value로 `name.value` 를 설정했다. 

(코드 4라인부터) 우리가 useInput이라는 함수의 인자로 초깃값을 설정하면 그 초깃값을 value에 넣으라고 설정했기 때문에 화면에는 다음과 같이 출력된다.  

참고로 useState와는 달리 useInput은 반드시 value라는 이름으로 설정해주어야 한다. 





0806_1





그런데 여기까지만 하면 Mr. 라고 되어 있는 input 박스에 무언가를 타이핑하려고 해도 아무것도 설정되지 않는다. 이를 위해 사용하는 것이 아직 사용하지 않은 setValue 이다. 

setValue를 onChange 에 대응시키려면 다음과 같이 적어주면 된다. 





```jsx
import React, { useState } from "react";
import "./styles.css";

const useInput = (initialValue) => {
  const [value, setValue] = useState(initialValue);
  const onChange = (event) => {
    const {
      target: {
        value
      }
    } = event;
// onChange로 바뀐 event array 내 target 내 값을 value에 할당.
    setValue(value);
  }
  return { value, onChange }; //반드시 리턴.
};

const App = () => {
  const maxLen = data => data.length < 10;
  const name = useInput("Mr.");
  return (
    <div>
      <h1>Hello</h1>
      <input placeholder="Name" {...name} />
    </div>
  );
};

export default App;

```





하나 설명하지 않은 게 있다면 `{...name}` 이다. 이렇게 적어주면 react는 name 내에 있는 것을 '알아서' 풀어준다 ! 그래서 일일이 value={~} onChange={~} 이렇게 지정해주는 것보단 {...name} 하나로 모든 것을 해결하는 게 훨씬 간편하다. 





## useInput 응용

useInput 을 이용한 input 박스에 정규표현식을 적용해보자. 

우리는 10글자 이상 넘어가지 않도록 정규표현식을 줄 것이다. 

코드로 짜면 다음과 같다. 





```jsx
import React, { useState } from "react";
import "./styles.css";

const useInput = (initialValue, validatorFunc) => {
  const [value, setValue] = useState(initialValue);
  const onChange = (event) => {
    const {
      target: {
        value
      }
    } = event;
    let updateOrNot =  true;
    if (typeof validatorFunc === "function") {
      updateOrNot = validatorFunc(value);
    }
    if (updateOrNot)
      setValue(value);
  }
  return { value, onChange };
};

const App = () => {
  const maxLen = data => data.length < 10;
  const name = useInput("Mr.", maxLen);
  return (
    <div>
      <h1>Hello</h1>
      <input placeholder="Name" {...name} />
    </div>
  );
};

export default App;
```





useInput이 인자로 함수 하나를 더 받도록 만든다. 그리고 그 함수에 우리가 넣은 값이 만약 10글자가 넘어간다면 setValue 하지 않도록 만들어줬다. 

천천히 코드를 보면 무슨 말인지 이해가 갈 것이다. 필자도 이해하는 데 꽤 시간이 걸렸으니 조급하게 생각하지 말고 코드를 잘 살펴보자. 





# useTabs



useTabs는 array data, 그러니까 json 데이터를 받아 tab 및 content를 노출시키는 데에 활용할 수 있다. 

예를 들어 다음과 같은 data가 있다고 하자. 





```javascript
const data = [
  {
    tab: "tab1",
    content: "I'm the content of tab1"
  },
  {
    tab: "tab2",
    content: "I'm the content of tab2"
  }
];
```





그리고 App function에서는 다음과 같이 map을 그리고 있다. 





```jsx
const App = () => {
  return (
    <div>
      {data.map((t) => (
				<button>
          {t.tab}
        </button>
      ))}
    </div>
  );
};
```





javascript의 map이 무엇인지 안다면 화면에 button 두 개가 있고 그 안에 tab1 이라는 글자가 박혀있겠구나 하고 상상이 될 것이다. 

여기서 우리가 하고 싶은 것은 버튼을 누르면, 화면에 관련 content가 출력되는 것이다. 이를 위해 기본적인 useTabs의 틀을 짜보겠다. 





```jsx
import React, { useState } from "react";
import "./styles.css";

const data = [
  {
    tab: "tab1",
    content: "I'm the content of tab1"
  },
  {
    tab: "tab2",
    content: "I'm the content of tab2"
  }
];

const useTabs = (initIndex, tabArr) => {
  const [currentIndex, setCurrentIndex] 
  = useState(initIndex);

  return { 
    currentItem: tabArr[currentIndex]
  };
};

const App = () => {
  const { currentItem } = useTabs(0, data);
  return (
    <div>
      {data.map((t) => (
        <button>
          {t.tab}
        </button>
      ))}
      <div>
        {currentItem.content}
      </div>
    </div>
  );
};

export default App;

```





조금 나눠서 살펴보자. 





```jsx
const useTabs = (initIndex, tabArr) => {
  const [currentIndex, setCurrentIndex] 
  = useState(initIndex);

  return { 
    currentItem: tabArr[currentIndex]
  };
};
```





useTabs는 initIndex로 무어나를 받아 을 받아 currentIndex에 넣는다. 

tabArr 이라는 이름으로 받아 온 data의 currentIndex, 예를 들어 data[0] 이 현재 return 문 내의 currentItem으로 설정된다. 





```jsx
const App = () => {
  const { currentItem } = useTabs(0, data);
  return (
    <div>
      {data.map((t) => (
        <button>
          {t.tab}
        </button>
      ))}
      <div>
        {currentItem.content}
      </div>
    </div>
  );
};
```





그러면 App에서는 이 useTabs의 리턴 값을 currentItem 이라는 state에 넣고, 렌더링 하는 데에 사용할 것이다. 





우리가 의도하는 것은 tab1을 누르면 content1이 나오고, tab2를 누르면 content2가 나오는 것이다. 이를 위해 필요한 설정은 useTabs의 리턴 값으로 changeItem 이라는 필드를 추가적으로 주는 것. 그리고 그 필드의 값을 setCurrentIndex로 설정하는 것이다. 무슨 말인지 코드를 통해살펴보자. 





```jsx
import React, { useState } from "react";
import "./styles.css";

const data = [
  {
    tab: "tab1",
    content: "I'm the content of tab1"
  },
  {
    tab: "tab2",
    content: "I'm the content of tab2"
  }
];

const useTabs = (initIndex, tabArr) => {
  const [currentIndex, setCurrentIndex] 
  = useState(initIndex);

  return { 
    currentItem: tabArr[currentIndex], 
    changeItem: setCurrentIndex //바뀐 부분
  };
};

const App = () => {
  const { currentItem, changeItem } = useTabs(0, data);
  return (
    <div>
      {data.map((t, i) => ( //index 추가
        <button
          onClick={() => {
            changeItem(i);
          }} //바뀐 부분.
        >
          {t.tab}
        </button>
      ))}
      <div>{currentItem.content}</div>
    </div>
  );
};

export default App;

```





위의 코드에서 주목해야 하는 것은 changeItem이다. changeItem으로 받아온 녀석은 useTabs의 setCurrentIndex이며, setCurrentIndex 는 currentIndex라는 state를 설정하여 다시 화면에 렌더링한다. 







# useEffect





useEffect는 componentDidMount, componentWillUnmount 그리고 componentWillUpdate 와 비슷하다. useEffect에 대해 다음 예시를 살펴보면서 알아보자. 





```jsx
const App = () => {
  const sayHello = () => console.log("Helloooo");
  const [numberA, setNumberA] = useState(0);
  const [numberB, setNumberB] = useState(0);
  useEffect(sayHello);
  
  return (
  	<div>
    	<div>Hello</div>
      <button onClick={() => setNumberA(numberA+1)}>{numberA}</button>
      <button onClick={() => setNumberB(numberB+1)}>{numberB}</button>
    </div>
  )
}
```





먼저 useEffect는 componentDidMount + componentDidUpdate 와 같이 렌더링 작업이 끝난 후에 이벤트가 발생한다. 그래서 위의 코드에서 setNumberA이든 setNumberB이든 둘 중 하나가 실행될 때마다 useEffect가 호출되어 콘솔에 "Helloooo" 가 출력된다. 





useEffect는 특정 값이 변하느냐 아니냐에 따라 이벤트가 발생하도록 지정해줄 수도 있다. 무슨 말이나면 다음의 코드에서 



```jsx
const App = () => {
  const sayHello = () => console.log("Helloooo");
  const [numberA, setNumberA] = useState(0);
  const [numberB, setNumberB] = useState(0);
  useEffect(sayHello, [numberA]); //달라진 부분
  
  return (
  	<div>
    	<div>Hello</div>
      <button onClick={() => setNumberA(numberA+1)}>{numberA}</button>
      <button onClick={() => setNumberB(numberB+1)}>{numberB}</button>
    </div>
  )
}
```





useEffect의 두 번째 인자로 `[ ]` 를 써주고 그 안에 특정 값을 집어 넣으면 그 값이 변할 때만 이벤트가 발생한다. 





그렇다면 `[ ]` 만 써놓으면 어떻게 될까? 아무것도 일어나지 않을까? 아니면 업데이트가 될 때마다 이벤트가 설정될까?





정답은 `둘 다 아니다.` 이다. 무언가가 업데이트 될 때마다 아무런 이벤트도 발생하지 않는 것은 맞다. 하지만 useEffect는 componentDidMount의 역할도 하기 때문에, 최초의 한 번은 실행되는 것이다. 비유하자면 `do-while` 문의 `do` 역할을 한다고 생각하면 된다. 





useEffect에서 하나 더 추가적으로 설명하자면 useEffect는 함수를 리턴한다는 것이다. 그리고 그것이 componentWillUnmount의 역할을 하는데, 이것에 대해서는 useEffect를 활용해보면서 설명하도록 하겠다. 





# useRef



공식문서에는 useRef를 다음과 같이 설명해놓았다 : 

```
useRef는 .current 프로퍼티로 전달된 인자(`initialValue`)로 초기화된 변경 가능한 ref 객체를 반환합니다. 반환된 객체는 컴포넌트의 전 생애주기를 통해 유지될 것입니다.

- https://ko.reactjs.org/docs/hooks-reference.html
```





그런데 이게 무슨 말인지 이해하는 게 좀 직관적이지 않다고 판단했다. 그래서 내가 이해한 것을 토대로 풀어서 설명을 하자면 useRef는 렌더링 시에(Return 문 안에서) 변수를 어떤 태그 안에 할당하고, 그 변수에 `.current` 속성에 값을 전달하여 이벤트를 발생시키는 것이라고 생각한다. 





예제 또한 공식문서의 것으로 예를 들어 보겠다. 





```jsx
function TextInputWithFocusButton() {
  const inputEl = useRef(null);
  const onButtonClick = () => {
    // `current` points to the mounted text input element
    inputEl.current.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
  
- https://ko.reactjs.org/docs/hooks-reference.html
```





주의해야 할 점도 있다. 공식문서에서는 useRef의 값이 가변적이긴 해도 그것의 값이 변한다고 해서 리렌더링을 발생시키는 것이 아님에 주의하라고 되어 있다. 





