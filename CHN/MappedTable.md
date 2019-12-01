### MappedTable渲染为映射表格

通过对象数组渲染表格，属性名称与列对应，动态创建每一行。

* 使用`Object.keys()`，`Array.prototype.filter()`，`Array.prototype.includes()`和`Array.prototype.reduce()`生成一个`filteredData`数组，包含所有对象 使用`propertyNames`中指定的键。
* 渲染一个`<table>`元素，其中一组列等于`propertyNames`中的值。
* 使用`Array.prototype.map`将`propertyNames`数组中的每个值渲染为`<th>`元素。
* 使用`Array.prototype.map`将`filteredData`数组中的每个对象渲染为`<tr>`元素，对象中的每个键包含一个`<td>`。

```jsx
function MappedTable({ data, propertyNames }) {
  let filteredData = data.map(v =>
    Object.keys(v)
      .filter(k => propertyNames.includes(k))
      // 使用 reduce 迭代，为 acc 对象赋值：
      // 回调函数为 (acc, key) => ((acc[key] = v[key]), acc) 初始值为 {}
      // ((操作), 返回值) 语法解读：括号里进行任意操作，并指定返回值
      .reduce(( acc, key) => ((acc[key] = v[key]), acc), {}),
  );
  return (
    <table>
      <thead>
        <tr>
          {propertyNames.map(val => (
            <th key={`h_${val}`}>{val}</th>
          ))}
        </tr>
      </thead>
      <tbody>
        {filteredData.map((val, i) => (
          <tr key={`i_${i}`}>
            {propertyNames.map(p => (
              <td key={`i_${i}_${p}`}>{val[p]}</td>
            ))}
          </tr>
        ))}
      </tbody>
    </table>
  );
}
```
#### Notes

此组件不适用于嵌套对象，如果在`propertyNames`中指定的任何属性中有嵌套对象，则会中断。

例子

```jsx
export default function() {
  const people = [
    { name: 'John', surname: 'Smith', age: 42 },
    { name: 'Adam', surname: 'Smith', gender: 'male' },
  ];
  const propertyNames = ['name', 'surname', 'age'];
  return <MappedTable data={people} propertyNames={propertyNames} />;
}
```
