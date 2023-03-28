## Writing markup with JSX
> JSX 스타일로 마크업 작성하기

The markup syntax you've seen above is called _JSX_. It is optional, but most React projects use JSX for its convenience. All of the [tools we recommend for local development](https://react.dev/learn/installation) support JSX out of the box.
> 마크업 문법은 *JSX*로 불립니다. 선택 사항이지만 많은 React 프로젝트들은 편리하기 때문에 JSX을 사용합니다. 개발에 추천하는 모든 툴은 JSX 문법을 지원합니다.  
 
JSX is stricter than HTML. You have to close tags like `<br />`. Your component also can't return multiple JSX tags. You have to wrap them info a shared parent, like a `<div>...</div>` or an empty `<>...</>` wrapper:
> JSX 문법은 HTML보다 엄격합니다. `<br />`와 같이 태그를 닫아야합니다. 또한, 컴포넌트는 여러개의 JSX 태그를 반환할 수 없습니다. `<div>...</div>` 또는 `<>...</>`와 같이 공유하고 있는 부모 태그로 감싸줘야합니다:

```tsx
function AboutPage() {
  return (
    <>
      <h1>About</h1>
      <p>Hello there.<br />How do you do?</p>
    </>
  );
}
```

If you have a lot of HTML to port to JSX, you can use an [online converter](https://transform.tools/html-to-jsx).
> 만약 JSX 문법에 연결할 HTML이 많을 경우, 온라인 변환 툴을 사용할 수 있습니다.