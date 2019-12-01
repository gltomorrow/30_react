### LimitedTextarea限制字符数的多行文本

呈现限制字符数的多行文本组件。

* 使用`React.useState()` hook 创建`content`状态变量并将其值设置为`value`。
创建一个方法`setFormattedContent`，如果它比`limit`长，它会修剪输入的内容。
* 使用`React.useEffect()` hook 来调用`content`状态变量值的`setFormattedContent`方法。
* 使用`<div>`来包装`<textarea>`和`<p>`元素，它显示字符数并绑定`<textarea>`的`onChange`事件来调用`setFormattedContent`处理 `event.target.value`的值。

参考： <a href="https://zh-hans.reactjs.org/docs/hooks-overview.html" target="_blank">hook文档</a>

```jsx
import React from "react";
function LimitedTextarea({ rows, cols, value, limit }) {
  // React.useState(初始值) 通过在函数组件里调用它，来给组件添加一些内部 state
  // 返回一对值：当前状态和一个让你更新它的函数，你可以在事件处理函数中或其他一些地方调用这个函数。
  const [content, setContent] = React.useState(value);

  const setFormattedContent = text => {
    console.log("setFormattedContent");
    // 符合长度才允许修改
    text.length > limit ? setContent(text.slice(0, limit)) : setContent(text);
  };

  // useEffect 就是一个 Effect Hook ，在组件挂载和更新时执行
  // 可以看做 componentDidMount，componentDidUpdate 和 componentWillUnmount 这三个生命周期函数的组合
  React.useEffect(() => {
    console.log("useEffect");
    setFormattedContent(content);
  }, []);

  return (
    <div>
      <textarea
        rows={rows}
        cols={cols}
        onChange={event => setFormattedContent(event.target.value)}
        value={content}
      />
      <p>
        {content.length}/{limit}
      </p>
    </div>
  );
}
```

例子

```jsx
export default function() {
  return <LimitedTextarea limit={32} value="Hello!" />;
}
```
