#### {} & {{}}

{}：用于将javascript表达式嵌入JSX中，可以使用javascript变量，函数，编写表达式等。

```jsx
const baseUrl = 'https://i.imgur.com/';
const person = {
  name: 'Gregorio Y. Zara',
  imageId: '7vQD0fP',
  imageSize: 's',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>  // 	直接引用person对象的字段
      <h1>{person.name}'s Todos</h1>
      <img
        className="avatar"
        src={baseUrl + person.imageId + person.imageSize + '.jpg'} //在大括号里可以拿着引用的字符串拼接字符串
        alt={person.name}
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}
```

{{}}：内层的大括号表示一个javascript对象，外层的大括号用于嵌入javascript表达式，它只是包在 JSX 大括号内的 JavaScript 对象。

> JSX value should be either an expression or a quoted JSX text

#### children prop

像`<Card><Avatar /></Card>` 这样的嵌套 JSX，`Avatar`将被视为 `Card` 组件的 `children` prop。

```jsx
function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}

export default function Profile() {
  return (
    <Card>
      <Avatar
        size={100}
        person={{ 
          name: 'Katsuko Saruhashi',
          imageId: 'YfeOqp2'
        }}
      />   // Avatar是Card的children prop
    </Card>
  );
}
```

#### Fragment

`<Fragment>` 通常使用 `<>...</>` 代替，允许你在不添加额外节点的情况下将子元素组合。当需要定义key，比如循环渲染多个元素的时候，只能使用`<Fragment>`。

```tsx
function Blog() {
  return posts.map(post =>
    <Fragment key={post.id}>
      <PostTitle title={post.title} />
      <PostBody body={post.body} />
    </Fragment>
  );
}
```

- 一个组件只能返回一个元素，可以使用<>...</>将多个元素组合起来作为一个元素。
- 可以组合多个元素分配给一个变量

```tsx
function CloseDialog() {
  const buttons = (
    <>
      <OKButton />
      <CancelButton />
    </>
  );
  return (
    <AlertDialog buttons={buttons}>
      Are you sure you want to leave this page?
    </AlertDialog>
  );
}
```

- 可以组合组件和文本

```tsx
function DateRangePicker({ start, end }) {
  return (
    <>
      From
      <DatePicker date={start} />
      to
      <DatePicker date={end} />
    </>
  );
}
```

#### 组件的纯粹

纯粹的组件：

- **只负责自己任务**，不会更改在该函数调用前就已存在的对象或变量。
- **输入相同，则输出相同**， 给定相同的输入，组件应该总是返回相同的 JSX



#### HOOK

让你的组件使用 React 功能的特殊函数。任何以`use`

- `useState`: 增加状态。它接收初始状态并返回一对值：当前状态，以及一个让你更新状态的设置函数。
- `useImmer(initialState)` is very similar to `useState`，会return tuple。

**只在顶层调用Hooks，在同一组件的每次渲染中，Hooks 都依托于一个稳定的调用顺序**。



#### 渲染和提交

在初次渲染时，会创建DOM节点或者在使用[`appendChild()`](https://developer.mozilla.org/docs/Web/API/Node/appendChild) DOM API 将其创建的所有 DOM 节点放在屏幕上， 在渲染完成并且更新完DOM书之后（更新就是提交，渲染是将component生成component的jsx文件），浏览器会重新绘制整个屏幕。

**React 仅在渲染之间存在差异时才会更改 DOM 节点**



#### state

##### 局部变量不会出发更新的原因：

1. **局部变量无法在多次渲染中持久保存**
2. **更改局部变量不会触发渲染**

##### useState Hook提供了两个功能：

1. state变量用于保存渲染间的数据
2. state setter函数用于更新变量并且触发react重新渲染组件

>  React 如何知道返回哪个 state：[Link]( https://zh-hans.react.dev/learn/state-a-components-memory#how-does-react-know-which-state-to-return)
>
> 在 React 内部，为每个组件保存了一个数组，其中每一项都是一个 state 对。它维护当前 state 对的索引值，在渲染之前将其设置为 “0”。每次调用 useState 时，React 都会为你提供一个 state 对并增加索引值。
>
>  [React Hooks: not magic, just arrays](https://medium.com/@ryardley/react-hooks-not-magic-just-arrays-cd4f1857236e)

**React 会使 state 的值始终”固定“在一次渲染的各个事件处理函数内部。**

##### setState()函数中的内容可以放：

1. 一个更新函数，这个会被加入state更新的队列中，要在一个事件中多次更新某些 state的是，需要使用纯函数来更新
2. 一个值，这个会直接替换state的值

> 对象的定义中使用 `[` 和 `]` 括号来实现属性的动态命名。eg: [e.target.name]: e.target.value



#### 状态管理

状态结构：状态不应该包含冗余或重复的信息

React允许覆盖默认行为，可以通过向组件传递一个唯一的`key`来强制重制其状态。

##### 用state响应输入



