## Rendering lists
> 리스트 렌더링

You will rely on JavaScript features like [`for` loop]() and the [array `map()` function]() to render lists of components.
> `for` 반복문과 배열 `map()` 함수를 이용하여 컴포넌트 리스트를 렌더링할 수 있습니다.  

For example, let's say you have an array of products:
> 예를 들어, 배열로 products가 있다면:

```tsx
const products = [
  { title: 'Cabbage', id: 1 },
  { title: 'Garlic', id: 2 },
  { title: 'Apple', id: 3 },
];
```

Inside your component, use the `map()` function to transform an array of products into an array of `<li>` items:
> 컴포넌트에서 `map()` 함수를 사용하여 배열 products의 요소들을 `<li>`로 변환할 수 있습니다:

```tsx
const listItems = products.map(product => 
  <li key={product.id}>
    {product.title}
  </li>
);

return (
  <ul>{listItems}</ul>
);
```

Notice how `<li>` has `key` attribute.
> `<li>`가 `key` 속성을 어떻게 가지고 있는지 알아봅시다.

For each item in a list, you should pass a string or a number that uniquely identifies that item among its siblings. Usually, a key should be coming from your data, such as a database ID. React uses your keys to know what happened if you later insert, delete, or reorder the items.
> 리스트의 각 아이템에 대해 고유한 식별할 수 있는 문자열이나 숫자를 형제에게 전달해주어야 합니다. 대체로 데이터베이스 ID와 같은 키 값은 데이터에서 제공받아야 합니다. 삽입, 삭제 또는 정렬할 때 React는 key 값들로부터 어떠한 상황이 일어나는지 알 수 있습니다.

```tsx
const products = [
  { title: 'Cabbage', isFruit: false, id: 1 },
  { title: 'Garlic', isFruit: false, id: 2 },
  { title: 'Apple', isFruit: true, id: 3 },
];

export default function ShoppingList() {
  const listItems = products.map(product => 
    <li
      key={product.id}
      style={{
        color: product.isFruit ? 'magenta' : 'darkgreen'
      }}
    >
      {product.title}
    </li>
  );

  return (
    <ul>{listItems}</ul>
  );
}
```

<img src="https://user-images.githubusercontent.com/42595869/228600734-76fc61f3-4fca-40ea-bd8e-f5e8ad2e9bd1.png" width="800" height="auto">