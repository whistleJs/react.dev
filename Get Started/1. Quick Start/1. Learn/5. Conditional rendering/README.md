## Conditional rendering
> 조건부 렌더링

In React, there is no special syntax for writing conditions. Instead, you'll use the same techniques as you use when writing regular JavaScript code. For example, you can use an `if` statement to conditionally include JSX:
> 리액트에서 조건부를 사용할 때 특별한 문법은 없습니다. JavaScript 코드를 작성할 때 같은 기술을 사용하면 됩니다. 예를 들어, `if` 문을 사용하여 조건부를 표현할 수 있습니다.

```tsx
let content;
if (isLoggedIn) {
  content = <AdminPanel />;
} else {
  content = <LoginForm />;
}
return (
  <div>
    {content}
  </div>
);
```

If you prefer more compact code, you can use the [conditional `?` operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator). Unlike `if`, it works inside JSX:
> 더 짧은 코드를 원한다면, `?` 연산자를 사용하여 조건부를 표현할 수 있습니다. `if` 문과 달리 JSX 문법 안에서 작동합니다:

```tsx
<div>
  {isLoggedIn ? (
    <AdminPanel />
  ) : (
    <LoginForm />
  )}
</div>
```

When you don't need the `else` branch, you can also use a shorter [logical `&&` syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_AND#short-circuit_evaluation):
> `else` 문을 사용할 필요가 없을 때, `&&` 연산자를 사용하여 더 짧게 표현할 수 있습니다.

```tsx
<div>
  {isLoggedIn && <AdminPanel />}
</div>
```

All of these approaches also work for conditionally specifying attributes. If you're unfamiliar with some of this JavaScript syntax, you can start by always using `if...else`.
> 이러한 모든 접근법 또한 속성 값을 표현할 때도 사용할 수 있습니다. 해당 JavaScript 문법을 잘 모르는 경우 `if...else` 문을 사용해도 괜찮습니다.
