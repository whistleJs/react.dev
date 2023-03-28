## Adding styles
> 스타일 추가하기

In React, you specify a CSS class with `className`. It works the same way as the HTML `class` attribute:
> React에서 `className`을 이용하여 CSS class를 명시할 수 있습니다. `className`은 HTML에서 `class` 속성과 같은 역할을 하고 있습니다:

```tsx
<img className="avatar" />
```

Then you write the CSS rules for it in a separate CSS file:
> 그러면 별도의 CSS 파일에서 CSS 규칙을 작성합니다:

```css
/* In your CSS */
.avatar {
  border-radius: 50%;
}
```

React does not prescribe how you add CSS files. In the simplest case, you'll add a `<link>` tag to your HTML. If you use a build tool or a framework, consult its documentation to learn how to add a CSS file to your project.
> React는 CSS 파일을 어떻게 생성할지 정해주고 있지 않습니다. 간단한 경우는, HTML에서 `<link>`를 추가할 수 있습니다. 만약 빌드 툴이나 프레임워크를 사용한다면 프로젝트에서 CSS 파일을 어떻게 생성할지 해당 문서를 참고하세요.
