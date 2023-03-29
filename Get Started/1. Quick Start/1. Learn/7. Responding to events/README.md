## Responding to events
> 이벤트에 대한 응답

You can also respond to events by declaring _event handler_ functions inside your components:
> 또한 컴포넌트에서 *event handler* 함수를 선언하여 이벤트에 대한 응답을 받을 수 있습니다.

```tsx
function MyButton() {
  function handleClick() {
    alert('You clicked me!');
  }

  return (
    <button onClick={handleClick}>
      Click me
    </button>
  );
}
```

Notice how `onClick={handleClick}` has no parentheses at the end! Do not _call_ the event handler function: you only need to _pass it down_. React will call your event handler when the user clicks the button.
> `onClick={handleClick}` 에서 마지막에 괄호가 없는 것을 주의하세요! 이벤트 핸들러 함수 호출하지 않음: 오직 전달만 하면 됩니다. React는 사용자가 버튼을 클릭했을 때 이벤트 핸들러를 호출할 것입니다.
