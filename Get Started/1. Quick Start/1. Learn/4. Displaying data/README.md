## Displaying data
> 데이터 표시하기

JSX lets you put markup into JavaScript.
> JSX 문법을 사용하면 JavaScript에 마크업을 사용할 수 있습니다.

Curly braces let you "escape back" into JavaScript so that you can embed some variable from your code and display it to the user. For example, this will display `user.name`:
> 중괄호를 사용하여 변수를 삽입하여 사용자에게 표시할 수 있도록 "escape back" 할 수 있습니다. 예를 들어, `user.name`을 표시한다면:

```tsx
return (
  <h1>
    {user.name}
  </h1>
);
```

You can also "escape into JavaScript" from JSX attributes, but you have to use curly braces _instead of_ quotes.
> 또한, JSX 속성으로부터 "escape into JavaScript" 할 수 있지만, 따옴표 *대신* 중괄호를 사용해야합니다.

For example, `className="avatar"` passed the `"avatar"` string as the CSS class, but `src={user.imageUrl}` reads the JavaScript `user.imageUrl` variable value, and then passes that value as the `src` attribute:
> 예를 들어, `className="avatar"`는 `"avatar"` 문자열 형태의 CSS class이지만, `src={user.imageUrl}`은 JavaScript에서 `user.imageUrl`의 변수 값을 `src` 속성에 적용합니다:

```tsx
return (
  <img
    className="avatar"
    src={user.imageUrl}
  />
);
```

You can put more complex expressions inside the JSX curly braces too, for example, string concatenation:  
> 중괄호 안에 복잡한 표현식을 적용할 수도 있습니다. 예를 들어, 문자열 연결이 있습니다:

```tsx
const user = {
  name: 'Hedy Lamarr',
  imageUrl: 'https://i.imgur.com/yX0vd0Ss.jpg',
  imageSize: 90
};

export default function Profile() {
  return (
    <>
      <h1>{user.name}</h1>
      <img
        className="avatar"
        src={user.imageUrl}
        alt={'Photo of ' + user.name}
        style={{
          width: user.imageSize,
          height: user.imageSize
        }}
      />
    </>
  );
}
```

<img src="https://user-images.githubusercontent.com/42595869/228308567-82a80890-49cb-43b8-8868-efc7203f104c.png" width="800" height="auto">

In the above example, `style={{}}` is not a special syntax, but a regular `{}` object inside the `style={ }` JSX curly braces. You can use the `style` attribute when your styles depend on JavaScript variables.
> 위 예제에서, `style={{}}`은 특별한 문법이 아니라, `style={ }` 중괄호 안에 객체를 적용한 겁니다. 스타일이 JavaScript 변수에 선언될 때 `style` 속성을 사용할 수 있습니다.
