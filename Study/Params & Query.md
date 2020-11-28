## 파라미터와 쿼리



### params (파라미터)

먼저 params 를 통해 라우트에 특정 값을 넣는 방법에 대해서 알아보도록 하자.

전  강의했던 home과 test를 계속해서 사용하겠다.



src/App를 다음과 같은 코드로 수정한다.

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
              <Route path="/" component={Home} exact />
              <Route path="/test/:name" component={Test} />
            </BrowserRouter>
          </div>
        )
  }
}
```



위 코드에서 /test/:name 경로의 라우트를 추가했다.

위와 같이 url 에서 파라미터를 사용할 때는 : 뒤에 파라미터 이름을 지정해 준다.

위의 코드에서는 name이라는 파라미터가 생긴것이다.



name 파라미터를 표시하기 위해 test 컴포넌트를 수정해 보자



```react
// src/component/test.js

import React from 'react';

const test = ({match}) => {
    return (
        <div>
            <h3> This is {match.params.name} page</h3>
        </div>
    );
}

export default test;
```



코드의 5번째 줄에서 함수형 컴포넌트에 Props를 인자로 전달했다.

그리고 8번째 줄에서 Props로 전달받은 match 객체의 params.name을 이용하여 name 파라미터로 들어온 값을 표시하도록 했다

이제 우리는 'http://localhost:3000/test/test1' 경로로 들어가 보자

그럼 화면에는 This is test1 page 라고 표시될 것이다. 



### URL Query

params 를 이용해 라우트에 값을 지정한 것에 이어 URL query 를 이용하는 방법에 대해서 알아보도록 하자

url 에 들어온 쿼리스트링은 말그대로 string 형태의 데이터이다.

이를 객체로 변환하여 사용하려면 쿼리를 해석해야 한다.

쿼리를 파싱하는 방법에는 여러가지가 있겠지만, 우리는 query-string 이라는 라이브러리를 사용하자

```react
$ yarn add query-string
```



프로젝트의 루트 경로에서 위의 명령어를 입력하여 query-string 라이브러리를 추가해 줍시다.

그리고 test.js 컴포넌트를 다음과 같이 수정해 줍니다.

```react
// src/component/Test.js

import React from 'react';
import queryString from 'query-string';
 
const About = ({location, match}) => {
    const query = queryString.parse(location.search);
    console.log(query);
 
    return (
        <div>
            <h2>This is {match.params.name} page</h2>
        </div>
    );
};
 
export default Test;
```

코드의 네 번째 줄에서 query-string 을 호출했습니다.

query-string을 사용하는 방법은 queryString 객체의 parse 메소드를 이용하면 된다.

이를 통해 쿼리스트링을 객체 형태로 해석할 수 있다.

\* url 에 입력한 쿼리스트링의 값은 해당 컴포넌트가 location.search Props 로 전달 받는다.

어플레케이션에  'http://localhost:3000/test/test1?query=true' 경로로 접속해 보자.



그럼 화면에 This is test1 page가 뜰것이고 F12를 눌러 console창을 열어보면

query: "true" 라고 잘 해석되어 출력된 것을 알 수 있다.

