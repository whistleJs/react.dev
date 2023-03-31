## Inspecting the starter code
> 스타터 코드 살펴보기

In CodeSandbox you'll see three main sections:
> CodeSandbox에서 3개의 섹션을 볼 수 있습니다:

<img src="https://user-images.githubusercontent.com/42595869/229102101-292d83f4-7328-491b-b949-4e4416f0433a.png" width="400" height="auto">

1. The _Files_ section with a list of files like `App.js`, `index.js`, `styles.css` and a folder called `public`
> *Files* 섹션에선 `App.js`, `index.js`, `styles.css` 파일 목록과 `public` 폴더가 있습니다.

2. The _code editor_ where you'll see the source code of your selected file
> *code editor*에는 선택한 파일의 코드를 볼 수 있습니다.

3. The _browser_ section where you'll see how the code you've written will be displayed
> *browser* 섹션에는 작성한 코드가 어떻게 보여지는지 확인할 수 있습니다.

The `App.js` file should be selected in the _Files_ section. The contents of that file in the _code editor_ should be:
> *Files* 섹션에서 `App.js` 파일은 선택되어 있습니다. *code editor*에는 선택된 파일의 내용이 보여지고 있습니다.

```tsx
export default function Square() {
  return <button className="square">X</button>;
}
```

The _browser_ section should be displaying a square with a X in it like this:
> *browser* 섹션에는 아래와 같이 사각형 안에 X가 표시되고 있습니다:

<img src="https://user-images.githubusercontent.com/42595869/229103299-73983b94-0d84-48f7-9a89-4515a615e8c8.png" width="100" height="auto">

Now let's have a look at the files in the starter code.
> 이제 스타터 코드의 파일을 살펴보도록 하겠습니다.

### `App.js`

The code in `App.js` creates a _component_. In React, a component is a piece of reusable code that represents a part of a user interface. Components are used to render, manage, and update the UI elements in your application. Let's look at the component line by line to see what's going on:
> `App.js` 코드에서 *컴포넌트*를 만들었습니다. React에서 컴포넌트는 사용자 인터페이스의 일부를 나타내는 재사용 가능한 코드입니다. 앱에서 컴포넌트는 UI 요소들을 그리고, 관리하고 업데이트하는 데 사용됩니다. 컴포넌트 코드의 한 줄씩 살펴보며 어떤 일이 벌어지는지 알아보겠습니다:  

```tsx
export default function Square() {
...
```

The first line defines a function called `Square`. The `export` JavaScript keyword makes this function accessible outside of this file. The `deafult` keyword tells other files using your code that it's the main function in your file.
> 첫번째 줄에서 `Square`로 불리는 함수를 정의했습니다. JavaScript 키워드 `export`는 해당 함수를 다른 파일에서도 접근이 가능하게 만들어줍니다. `default` 키워드는 다른 파일에서 불러올 때 해당 함수를 해당 파일에서 메인 함수임을 알려줍니다.

```tsx
...
  return <button className="square">X</button>
...
```

The second line returns a button. The `return` JavaScript keyword means whatever comes after is returned as a value to the caller of the function. `<button>` is a _JSX_ element. A JSX element is a combination of JavaScript code and HTML tags that describes what you'd like to display. `className="square"` is a button property or _prop_ that tells CSS how to style the button. `X` is the text displayed inside of the button and `</button>` closes the JSX element to indicate that any following content shouldn't be placed inside the button.
> 두번째 줄은 버튼을 반환하고 있습니다. JavaScript 키워드 `return`은 무엇이든 해당 함수를 호출한 곳으로 값을 반환한다는 의미입니다. `<button>`은 *JSX* 요소입니다. JSX 요소는 JavaScript 코드와 표시할 내용을 설명할 HTML 태그가 결합되어 있습니다. `className="square"`은 CSS에 해당 버튼의 스타일을 어떻게 지정할지 전해주는 속성이거나 *prop*입니다. `X`는 버튼 안에 표시되는 텍스트이고 `</button>`은 JSX 요소를 닫아 다음 내용이 버튼 안에 있으면 안된다는 것을 나타냅니다.  

### `styles.css`

Click on the file labeled `styles.css` in the _Files_ section of CodeSandbox. This file defines the styles for you React app. The first two CSS _selectors_ (`*` and `body`) define the style of large parts of your app while the `.square` selector defines the style of any component where the `className` property is set to `square`. In your code, that would match the button from your Square component in the `App.js` file.
> CodeSandbox의 *Files* 섹션에서 `styles.css` 라벨을 클릭하세요. 이 파일은 React 앱의 스타일을 정의했습니다. 첫번째로 2개의 CSS *selectors* (`*`와 `body`)는 앱의 큰 부분 스타일을 정의하는 반면 `.square` 선택자는 `className` 속성에 `square` 값을 설정한 어떠한 컴포넌트에 스타일을 정의했습니다. 코드에서, `App.js` 파일에 있는 Square 컴포넌트의 버튼과 일치하고 있습니다.  


### `index.js`

Click on the file labeled `index.js` in the _Files_ section of CodeSandbox. You won't be editing this file during the tutorial but it is the bridge between the component you created in the `App.js` file and the web browser.
> CodeSandbox의 *Files* 섹션에서 `index.js` 라벨을 클릭하세요. 튜토리얼이 진행되는 동안 이 파일을 편집하진 않습니다만 `App.js` 파일에 생성된 컴포넌트와 웹 브라우저 사이의 다리 역할을 해줍니다.  

```tsx
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';
import './styles.css';

import App from './App';
```

Lines 1-5 brings all the necessary pieces together:
> 1-5번째 줄은 필요한 부분들을 묶어줍니다:

- React
> React

- React's library to talk to web browsers (React DOM)
> 웹 브라우저와 통신할 수 있는 React의 라이브러리 (React DOM)

- the styles for your component
> 컴포넌트를 위한 스타일

- the component you created in `App.js`
> `App.js`에서 생성된 컴포넌트

The remainder of the file brings all the pieces together and injects the final product into `index.html` in the `public` folder.
> 파일의 나머지 부분들은 모아서 `public` 폴더에 있는 `index.html`에 주입하면 됩니다.