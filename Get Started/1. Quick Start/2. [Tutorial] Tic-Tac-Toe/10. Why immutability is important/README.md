## Why immutability is important
> 왜 불변성은 중요할까

Note how in `handleClick`, you call `.slice()` to create a copy of the `squares` array instead of modifying the existing array. To explain why, we need to discuss immutability and why immutability is important to learn.
> `handleClick`에서 기존 배열을 수정하는 대신 `squares` 배열을 `.slice()`로 복사하는 방법에 주목해봅시다. 이유를 설명하려면 불변성과 불변성이 왜 중요한지 알아야 합니다.  

There are generally two approaches to changing data. The first approach is to _mutate_ the data by directly changing the data's values. The second approach is to replace the data with a new copy which has the desired changes. Here is what it would look like if you mutated the `squares` array:
> 일반적으로 데이터를 변경하는 방법에는 2가지 방법이 있습니다. 첫번째 방법은 데이터의 값을 직접 변경하는 방법입니다. 두번째 방법은 원하는 데이터를 변경하여 새로운 복사본으로 교체하는 것입니다. 다음은 `squares` 배열을 변경한 후의 모습입니다:  

```ts
const squares = [null, null, null, null, null, null, null, null, null];
squares[0] = 'X';
// Now `squares` is ["X", null, null, null, null, null, null, null, null];
```

And here is what it would look like if you changed data without mutating the `squares` array:
> 그리고 `squares` 배열을 변경하지 않는 경우의 모습입니다.

```ts
const squares = [null, null, null, null, null, null, null, null, null];
const nextSquares = ['X', null, null, null, null, null, null, null, null];
// Now `squares` is unchanged, but `nextSquares` first element is 'X' rather than `null`
```

The result is the same but by not mutating (changing the underly data) directly, you gain serveral benefits.
> 결과는 같지만 직접 변경하지 않으면(기본 데이터 변경) 여러 가지 이점을 얻을 수 있습니다.  

Immutability makes complex features much easier to implement. Later in this tutorial, you will implement a "time travel" feature that lets you review the game's history and "jump back" to past moves. This functionality isn't specific to games - an ability to undo and redo certain actions is a common requirement for apps. Avoiding direct data mutation lets you keep previous versions of the data intact, and reuse them later.
> 불변성을 통해 복잡한 기능들을 쉽게 구현할 수 있습니다. 이 튜토리얼 이후, 게임의 기록을 확인할 수 있는 "time travel"과 과거로 돌아가는 "jump back" 기능을 구현할 것입니다. 이 기능은 게임에만 해당하지 않습니다 - 특정 작업을 실행 취소하고 다시 실행하는 기능은 앱의 일반적인 요구 사항입니다. 직접 데이터를 변경하는 것을 피하면 이전 버전의 데이터를 그대로 유지하고 나중에 다시 사용할 수 있습니다.  

There is also another benefit of immutability. By default, all child components re-render automatically when the state of a parent component changes. This includes even the child components that weren't affected by the change. Although re-rendering is not by itself noticeable to the user (you shouldn't actively try to avoid it!), you might want to skip re-rendering a part of the tree that clearly wasn't affected by it for performance reasons. Immutability makes it very cheap for components to compare whether their data has changed or not. You can learn more about how React chooses when to re-render a component in [the `memo` API reference](https://react.dev/reference/react/memo).
> 불변성의 또 다른 이점이 있습니다. 기본적으로 모든 하위 컴포넌트는 부모 컴포넌트의 state가 변경될 때 자동적으로 다시 렌더링합니다. 여기에는 변경 사항의 영향을 받지 않는 하위 컴포넌트도 포함됩니다. 다시 렌더링하는 자체는 사용자가 알 수는 없지만(적극적으로 피하려고 해서는 안됩니다!), 성능상의 이유로 트리에 영향받지 않는 부분을 다시 렌더링하는건 건너뛰는 것이 좋습니다. 불변성을 사용하면 컴포넌트의 데이터 변경 여부를 비교할 수 있습니다. React가 컴포넌트를 다시 렌더링할 시기를 선택하는 방법에 대한 자세한 내용은 **the `memo` API reference**에서 확인할 수 있습니다.