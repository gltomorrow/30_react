### DataList渲染为列表

通过数组渲染元素列表。

* 使用 `isOrdered` prop 的值有条件地渲染`<ol>`或`<ul>`列表。
* 使用`Array.prototype.map`将`data`中的每个项目渲染为`<li>`元素，给它一个由其索引和值的串联产生的`key`。
* 默认情况下，省略 `isOrdered` prop 以渲染`<ul>`列表。

```jsx
function DataList({ isOrdered, data }) {
  const list = data.map((val, i) => <li key={`${i}_${val}`}>{val}</li>);
  return isOrdered ? <ol>{list}</ol> : <ul>{list}</ul>;
}
```

例子

```jsx
export default function() {
  const names = ['John', 'Paul', 'Mary'];
  return (
    <div>
      无序列表：
      <DataList data={names} />
      有序列表：
      <DataList data={names} isOrdered />
    </div>
  );
}
```
