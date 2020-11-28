## Router

리액트는 **SPA (Single Page Application)** 방식으로써,

여러개의 페이지를 사용하며, 새로운 페이지를 로드하는 기존의 **MPA(Multi Page Application)** 방식과 달리

새로운 페이지를 로드하지 않고 하나의 페이지 안에서 필요한 데이터만 가져오는 형태를 가진다.



URL에서 path와 qurey string이란?

예를 들어 "http://junhostudy.com/search?page=3" 이라는 url이 있다고 하자

http:// 은 프로토콜을 의미한다.

프로토콜 다음의 junhostudy.com 은 도메인이라고 부르고

도메인 다음에 나오는 / 이후의 'search'를 path 라고 부르고

path 이후의 ? 다음에 나오는 'page=3' 같은 것들을 query string 이라고 부른다.

웹은 url의 path와 query string 을 이용하여 어떤 정보를 불러올지 결정한다.



### Router 사용하기

라우터를 쓰기 위해서는 react-router-dom을 설치해야한다.

```react
$ yarn add react-router-dom
```



그 다음 'src/App.js' 파일에 다음의 코드를 추가한다.

```react
// src/App.js

import { BrowserRouter, Route } from 'react-router-dom';
```



src 디렉토리 안으로 component 라는 디렉토를 만든 후 home.js 와 test.js 를 생성한다.

그런 후 home.js 와 test.js 에 각각의 코드를 추가로 입력한다.



+ home.js

```react
/* src/component/home.js */

import React from 'react';

const home = () => {
    return (
        <div>
            <h3> This is Junho's study </h3>
        </div>
    );
}

export default home;
```



test.js

```react
/* src/component/test.js */

import React from 'react';

const test = () => {
    return (
        <div>
            <h3> This is test page </h3>
        </div>
    );
}

export default test;
```



이제 이 코드를 App.js 경로로 들여온 후 생성한 파일들을 불러올 수 있는 코드를 추가합니다.

```react
/* src/App.js */
import React from 'react';
import './App.css';
import { BrowerRouter, Route} from 'react-router-dom';

import Home from './inc/home.js';
import Test from './inc/test.js';

class App extends Component{
    constructor(props){
        super(props)
        this.state = {
            
        }
    }
    render() {
        return(
          <div className='App'>
            <BrowserRouter>
              <Route path="/" component={Home} />
              <Route path="/test" component={Test} />
            </BrowserRouter>
          </div>
        )
  }
}
```



>①. React-Route 를 시작하는 코드입니다. **<Route> 코드는 반드시<BrowserRouter> 안에서 실행**되어야 합니다.
>
>
>
>②. Route 경로를 설정해주는 코드입니다. 
>
>
>
>③. Route의 속성 값으로 해당 경로의 url을 설정합니다.
>
>("/"는 제일 첫번째 경로의 값입니다.)
>
>
>
>④. 설정한 path의 경로로 이동했을 때 실행되는 컴포넌트를 설정합니다.  



코드를 적용한 후에 리액트를 실행하면

This is Junho's study가 뜰 것이다.

그런후 주소창에 "http://locahost:3000/test" 경로를 입력하면



This is Junho's study 밑에 This is test page 가 추가로 뜰것이다

그런데 route의 component는 분명 test.js 파일을 띄우고 싶은데

해당 경로에서 home.js 파일도 함께 실행된 결과가 나왔다.



그 이유는 **test.js**를 실행하는 "/test"의 경로 중 "/"가

**home.js**를 실행하는 "/"와 중복되기 때문이다.



이러한 중복을 막기 위해서 home.js route가 설정된 태그에 다음과 같은 코드로 바꾼다.

```react
/* src/App.js */

<Route path="/" component={Home} exact />
```



exact 속성은

해당 태그의 path 값이 **다른 경로와 중복되지 않고 완전한 경로로 사용**되게 한다.

즉, 순수하게 "/"의 경로로만 접근해야 설정된 component가 실행된다.