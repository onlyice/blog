---
title: "LLM 辅助记笔记"
date: 2023-12-07T23:12:32+08:00
draft: false
---

在最近对 ChatGPT 和 GitHub Copilot 的使用中，我越发觉得 LLM 非常适合用来辅助做笔记。

## 一个例子

我在学习一个知识点：在 React 中，如何将一个组件（而不是用其生成的节点）作为 prop 传给另外一个组件。

这个能力可以使组件更动态化。比如在下面的例子中，想通过传入参数来决定 title 是被一个 `<h2>`、`<h3>` 甚至是被非 HTML tag 的组件包裹：

```tsx
type Props = {
  title: string;
  children: React.ReactNode;
}

const Post = ({ title, children }: Props) => {
  return (
    <div>
      <h1>{title}</h1>
      {children}
    </div>
  );
}
```

我尝试问了下 ChatGPT。Prompt 为「在 React 中，如何将一个组件（而不是用其生成的节点）作为 prop 传给另外一个组件？」ChatGPT 的回答不尽如人意：

> 在 React 中，你可以将一个组件作为 prop 传递给另一个组件。这通常被称为"组件组合"或"组件嵌套"。以下是一个简单的例子：
> 
> 假设你有两个组件，ParentComponent 和 ChildComponent。你想将 ChildComponent 作为 prop 传递给 ParentComponent。你可以在 ParentComponent 中通过 JSX 将 ChildComponent 插入。下面是一个示例：
> 
> ```jsx
> import React from 'react';
> 
> // ChildComponent 是一个简单的函数组件
> const ChildComponent = () => {
>   return <div>我是子组件</div>;
> };
> 
> // ParentComponent 接受一个名为 child 的 prop，其中包含要传递的组件
> const ParentComponent = (props) => {
>   return (
>     <div>
>       <p>我是父组件</p>
>       {props.child} {/* 在这里插入 ChildComponent */}
>     </div>
>   );
> };
> 
> // 在另一个组件或应用中，你可以使用 ParentComponent，并将 ChildComponent 作为 prop 传递
> const App = () => {
>   return (
>     <div>
>       <ParentComponent child={<ChildComponent />} />
>     </div>
>   );
> };
> 
> export default App;
> ```
> 
> 在这个例子中，ParentComponent 接受一个名为 `child` 的 prop，并通过 `{props.child}` 将其插入到渲染的 JSX 中。在 App 组件中，你可以通过传递 `<ChildComponent />` 作为 `child` prop 的值，将 ChildComponent 传递给 ParentComponent。
> 
> 请注意，这只是一种方式，你可以根据具体的需求选择不同的方法。在实际开发中，你可能会遇到更复杂的情况，例如使用 render props 或 children prop 等模式。

可以说 ChatGPT 并没有理解我的意思。但由于这种技术问题本来就很难被清晰描述，于是我换了一个方法。我在 IDE 中将文章开头的 `<Post>` 组件代码敲入，然后向 GitHub Copilot Chat 提问：

> Post 组件希望可以接受一个新 prop，用来指定 title 应该用什么组件包裹（而不是固定为 `<h1>`）。请改造代码。

GitHub Copilot Chat 给出的回复非常赞：

> 你可以通过将标题组件作为一个 prop 传递给 `Post` 组件来实现这个需求。这个 prop 可以是任何有效的 React 组件，包括 HTML 元素和自定义组件。以下是如何实现的示例：
> 
> ```tsx
> import React from 'react';
> 
> type Props = {
>   title: string;
>   children: React.ReactNode;
>   TitleComponent: React.ComponentType<{ children: React.ReactNode }>; // 新增的 prop
> }
> 
> const Post = ({ title, children, TitleComponent }: Props) => {
>   return (
>     <div>
>       <TitleComponent>{title}</TitleComponent>  // 使用 TitleComponent 替代原来的 h1
>       {children}
>     </div>
>   );
> }
> ```
> 
> 在这个例子中，`TitleComponent` 是一个新的 prop，它接受一个 React 组件。然后，这个组件被用来渲染标题。你可以像这样使用 `Post` 组件：
> 
> ```tsx
> <Post title="Hello, world!" TitleComponent={props => <h2 {...props} />} >
>   Welcome to my blog!
> </Post>
> ```
> 
> 在这个例子中，标题将被渲染为 `<h2>` 元素，而不是 `<h1>`。

**这些内容被我直接复制进自己的笔记中。**

## LLM 是怎样帮到做笔记？

首先需要理清的最重要问题是：做这个笔记的目的是什么？

对我来说是：

1. 通过记笔记过程，梳理清楚知识点，加深理解
2. 当未来的自己需要使用同一个知识时，这个笔记应该能往我快速捡起来用

对于第 1 点，LLM 在这个 case 中也帮到我。在给 `TitleComponent` 做 TS 类型标注时，我只知道可以用 `React.FC`（函数式组件），并不知道有 `React.ComponentType`。LLM 帮我完善了理解。

对于第 2 点，LLM 给出的内容非常精练、好理解，使得未来我回顾这个笔记时非常容易上手。

另外的收益是，ChatGPT 或 GitHub Copilot 回答技术问题时，它往往会直接构造出代码示例来。如果是手写笔记，构造代码示例还是会花费一些时间。LLM 帮忙节省了时间。
