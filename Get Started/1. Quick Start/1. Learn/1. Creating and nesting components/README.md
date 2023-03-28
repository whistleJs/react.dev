## Creating and nesting components
> 컴포넌트 생성 및 중첩 컴포넌트

React apps are made out of _components_. A component is a piece of the UI that has its own logic and appearance. A component can be as small as a button, or as large as an entire page.
> React 앱들은 *컴포넌트들로* 이루어져있습니다. 컴포넌트는 고유한 로직과 형태를 가진 UI의 일부분입니다. 컴포넌트는 버튼처럼 작거나 전체 페이지만큼 클 수 있습니다.

React components are Javascript functions that return markup:
> React 컴포넌트들은 마크업을 반환하는 Javascript 함수입니다:

```tsx
function MyButton() {
  return (
    <button>I'm a button</button>
  );
}
```

Not that you've declared `MyButton`, you can nest it into another component:
> `MyButton`을 선언한 것이 아니라, 다른 컴포넌트에 중첩시킬 수 있습니다:

```tsx
export default function MyApp() {
  return (
    <div>
      <h1>Welcome to my app</h1>
      <MyButton />
    </div>
  );
}
```

Notice that `<MyButton />` starts with a capital letter. That's how you know it's a React component.  
React component names must always start with a capital letter, while HTML tags must be lowercase.
> `<MyButton />` 는 대문자로 시작합니다. 이렇게 React 컴포넌트라는 것을 알 수 있습니다.  
  HTML 태그들은 항상 소문자로 시작하기 때문에 React 컴포넌트 이름은 항상 대문자로 시작해야합니다.

Have a look at the result:
> 다음 결과를 봅시다.

```tsx
function MyButton() {
  return (
    <button>
      I'm a button
    </button>
  );
}

export default function MyApp() {
  return (
    <div>
      <h1>Welcome to my app</h1>
      <MyButton />
    </div>
  );
}
```

<img src="https://user-images.githubusercontent.com/42595869/228270537-0a7f13c2-ea79-4fe0-af58-ef53b65cf622.png" width="800" height="auto" />

The `export default` keywords specify the main component in the file. If you're not familiar with some piece of Javascript syntax, [MDN](https://developer.mozilla.org/en-US/docs/web/javascript/reference/statements/export) and [javascript.info](https://developer.mozilla.org/en-US/docs/web/javascript/reference/statements/export) have great references.
> `export default` 키워드들은 파일에서의 메인 컴포넌트를 명시합니다. 만약 Javascript 문법 일부가 익숙하지 않는 경우, MDN와 javascript.info에서 참고할 수 있습니다.