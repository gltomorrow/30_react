### DataTable渲染为表格

通过数组渲染表格，动态创建每一行。

*渲染一个带有两列(`ID`和`Value`)的`<table>`元素。
*使用`Array.prototype.map`将`data`中的每个项目渲染为`<tr>`元素，由其索引和值组成，给它一个由两者串联产生的`key`。

```jsx
function DataTable({ data }) {
  return (
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Value</th>
        </tr>
      </thead>
      <tbody>
        {data.map((val, i) => (
          <tr key={`${i}_${val}`}>
            <td>{i}</td>
            <td>{val}</td>
          </tr>
        ))}
      </tbody>
    </table>
  );
}
```

例子

```jsx
export default function() {
  const people = ['John', 'Jesse'];
  return <DataTable data={people} />;
}
```
