
# React router 없이 라우팅 하기
[React: Navigation Without React-Router](https://ncoughlin.com/posts/react-navigation-without-react-router/)


가보자고

<br>

### window.location

브라우저의 각 탭은 Window 를 나타내고, 각 window는 DOM을 가지고 있음

요것은 window 라는 자바스크립트 코드로 불러낼 수 있는 전역 변수임.

여러가지 속성들이 있고 그 중 하나가 window.location임

글고 또 중요한게 window.location.pathname 임

<br>

### window.location.pathname에 따라서 콘텐츠 보여주기

pathname 속성을 알 수 있으니까, pathname에 따라서 어떤 콘텐츠를 보여주거나 숨기면 됨

```jsx
import React, { useState } from "react"

import Accordion from "./components/Accordion"

const showAccordion = () => {
  if (window.location.pathname === "/") {
    return <Accordion />
  }
}

export default () => {
  return <div className="ui container">{showAccordion()}</div>
}

```
<br>

### 재사용 가능한 Route 컴포넌트 만들기

```jsx
const showComponent = (route, component) => {
  return window.location.pathname === route ? component : null
}

```

이런 식으로 만들 수도 있는데 이러면 컴포넌트를 하나씩 밖에 전달 못함.. 리액트는 여러개의 컴포넌트를 사용할 수 있는 방식을 선호함

<br>

```jsx
const Route = ({ path, children }) => {
  return window.location.pathname === path ? children : null
}

export default Route

```

요렇게 컴포넌트를 직접 props로 전달하지 않고 children을 사용햇음. Route 컴포넌트 하위에 써준 자식 컴포넌트를 모두 전달할 거임.. 그러면 하나의 route에 여러개의 컴포넌트를 보여줄 수도 있음

<br>

### 헤더 만들기

이제 각 페이지를 왔다 갔다 할 네비게이션이 필요함

헤더를 만들어 주겟음

```jsx
import React from "react";

const Header = () => {
  return (
    <div className="ui secondary pointing menu">
      <a href="/" className="item">
        Accordion
      </a>
      <a href="/color-select" className="item">
        Color Select
      </a>
      <a href="/translate" className="item">
        Translate
      </a>
      <a href="/search" className="item">
        Wiki Search
      </a>
      <a href="/all" className="item">
        All Widgets
      </a>
    </div>
  );
};

export default Header;

```

이렇게 헤더를 만들구

```jsx
import React from "react";

import Header from "./components/Header";
import Route from "./components/Route";
import ColorSelect from "./components/ColorSelect";
import Translate from "./components/Translate";
import Accordion from "./components/Accordion";
import Search from "./components/Search";

export default () => {
  return (
    <div className="ui container">
      <Header />
      <Route path="/">
        <Accordion />
      </Route>
      <Route path="/color-select">
        <ColorSelect />
      </Route>
      <Route path="/translate">
        <Translate />
      </Route>
      <Route path="/search">
        <Search />
      </Route>
      <Route path="/all">
        <Accordion />
        <ColorSelect />
        <Translate />
        <Search />
      </Route>
    </div>
  );
};

```

App.js에다가 붙여주면 되겟음

<br>

### 페이지 전체 리로드 막기

근데 이렇게만 하면 클릭할 때마다 페이지 전체가 다시 리로드 됨

(a 태그로 이동해서 그런거 같은데 왜 리로드되는지 찾아보기)

<br>

### Link 컴포넌트 만들기

일단 Link 컴포넌트라는 걸 만들거임

(근데 이걸 왜만들지?????? -> DRY를 위해서?)

props로는 보통 링크에서 필요한 걸 모두 넘겨줄거임

css 클래스, 이동할 주소, 그리고 링크 텍스트로 쓸 텍스트.


```jsx
import React from "react";

const Link = ({ className, href, children }) => {
  return (
    <a className={className} href={href}>
      {children}
    </a>
  );
};

export default Link;

```

만들었으면 헤더에 Link 컴포넌트를 적용하기

```jsx
import React from "react";

import Link from "./Link";

const Header = () => {
  return (
    <div className="ui secondary pointing menu">
      <Link href="/" className="item">
        Accordion
      </Link>
      <Link href="/color-select" className="item">
        Color Select
      </Link>
      <Link href="/translate" className="item">
        Translate
      </Link>
      <Link href="/search" className="item">
        Wiki Search
      </Link>
      <Link href="/all" className="item">
        All Widgets
      </Link>
    </div>
  );
};

export default Header;

```

<br>

### 페이지 리로드 막기

이제 페이지가 전체 새로고침 되는 걸 막을건데 Link 컴포넌트에 클릭이벤트 핸들러를 붙여줄거임

event.preventDefault() 로 클릭한 다음 아무것도 안하게 막기

```jsx
import React from "react";

const Link = ({ className, href, children }) => {
  // prevent full page reload
  const onClick = (event) => {
    event.preventDefault();
  };

  return (
    <a className={className} href={href} onClick={onClick}>
      {children}
    </a>
  );
};

export default Link;

```

리로드 막았으면 이제 상단 URL을 바꿔주고, 리로딩 안해도 콘텐츠가 바뀌게 해줄거임

<br>

### URL 바꾸기

상단 주소창에 나오는 URL을 안바꿔주고 그냥 컴포넌트만 쉭쉭 바꿔주면 사용자가 되게 불편함,,

왜냐면 즐겨찾기도 안됨. 특정 컴포넌트가 보이는 페이지를 즐겨찾기할 수가 없음,,

꼭 해야되는 건 아니지만 그래도 하는 게 좋음

(근데 href로 이동한거랑 url이 바뀌는 거랑은 다른건가??)

브라우저에는 URL을 바꾸는 메소드가 내장되어 있음

window.history.pushState()임.

요거를 클릭 이벤트 핸들러에 달아주면 되겟음

```jsx
import React from "react";

const Link = ({ className, href, children }) => {
  // prevent full page reload
  const onClick = (event) => {
    event.preventDefault();
    window.history.pushState({}, "", href)
  };

  return (
    <a className={className} href={href} onClick={onClick}>
      {children}
    </a>
  );
};

export default Link;

```

<br>

### URL 변경이랑 Route랑 연동하기

Link 클릭 -> url 변경 -> Route가 그걸 알고 컴포넌트 보여주기 -> 이걸 해야됨

이것도 브라우저 내장 메소드가 있음 `window.dispatchEvent()`임

리액트 내장 메소드도 있는데 `PopStateEvent()`임

```jsx
// Link.js

import React from "react";

const Link = ({ className, href, children }) => {

  const onClick = (event) => {
    // prevent full page reload
    event.preventDefault();
    // update url
    window.history.pushState({}, "", href);

    // Route들에게 URL 바뀌었다고 알려주기
    const navEvent = new PopStateEvent('popstate');
    window.dispatchEvent(navEvent);
  };

  return (
    <a className={className} href={href} onClick={onClick}>
      {children}
    </a>
  );
};

export default Link;

```

그런 다음 Route에서 받아줌

```jsx
// Route.js
import { useEffect } from 'react';

const Route = ({ path, children }) => {
    useEffect(() => {
        // define callback as separate function so it can be removed later with cleanup function
        // 콜백은 개별 함수로 작성한다. 이벤트 리스너를 삭제할 때 같이 삭제시킬 수 있도록
        const onLocationChange = () => {
            console.log('Location Change');
        }
        window.addEventListener('popstate', onLocationChange);
        // clean up event listener
        // 이벤트 리스너 삭제
        return () => {
            window.removeEventListener('popstate', onLocationChange)
        };
    }, [])

    return window.location.pathname === path
    ? children
    : null;
}

export default Route;

```

popstate라는 커스텀 이벤트를 만들고

Route에서 popstate의 이벤트 리스너를 설정햇음

URL이 바뀔때마다 onLocationChange 함수가 실행될거임

<br>

### Route 컴포넌트 저절로 리렌더링 시키기

이제 Route는 URL 변경을 감지할 수 잇게 되엇음

그리고 Route를 리렌더링할 수 있게 하는 상태를 만들거임,,(?)

컴포넌트는 상태값이 변경되면 자동으로 리렌더링한다는 걸 기억하셈

그래서 우리는 URL이 변경될 때마다 상태값을 바꿔줄거고 그러면 자동으로 리렌더링 되겠지?

```jsx
import { useEffect, useState } from 'react';

const Route = ({ path, children }) => {
    // state to track URL and force component to re-render on change
    const [currentPath, setCurrentPath] = useState(window.location.pathname);

    useEffect(() => {
        // define callback as separate function so it can be removed later with cleanup function
        const onLocationChange = () => {
            // update path state to current window URL
            // window URL이 바뀌면 state를 바뀌줌
            setCurrentPath(window.location.pathname);
        }

        // listen for popstate event
        window.addEventListener('popstate', onLocationChange);

        // clean up event listener
        return () => {
            window.removeEventListener('popstate', onLocationChange)
        };
    }, [])

    return currentPath === path
    ? children
    : null;
}

export default Route;

```