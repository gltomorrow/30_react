### Input基础输入框

输入框组件，使用回调函数将其值传递给父组件。

* 使用对象解构来设置`<input>`元素的某些属性的默认值。
* 使用适当的属性渲染一个`<input>`元素，并使用`onChange`事件中的`callback`函数将输入值传递给父元素。

```jsx
function Input({ callback, type = 'text', disabled = false, readOnly = false, placeholder = '' }) {
  return (
    <input
      type={type}
      disabled={disabled}
      readOnly={readOnly}
      placeholder={placeholder}
      // event.target.value
      onChange={({ target: { value } }) => callback(value)}
    />
  );
}
```

例子

```jsx
export default function() {
  return <Input type="text" placeholder="Insert some text here..." callback={val => console.log(val)} />;
}
```
