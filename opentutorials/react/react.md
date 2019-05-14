### immutable
shouldComponentUpdate 혹은 React.memo의 props 비교함수에서 비교하고자하는 props를 immutable하게 변경하지않으면 원하지 않는 결과를 얻을 수도 있다.
```javascript
...
  const [contents, setContents] = useState(
    [
      { id:1, title:'HTML', desc:'HTML is for information' },
      { id:2, title:'CSS', desc:'CSS is for design' },
      { id:3, title:'JavaScript', desc:'Javascript is for interactive' }
    ]
...
  // right!
  var _contents = contents.concat({id:maxContentId, title:_title, desc:_desc})
  setContents(_contents);

  console.log(prevProps.data === nextProps.data) // false

  // wrong!
  contents.push({id:maxContentId, title:_title, desc:_desc})    // 기존의 contents 자체를 변경해버림..
  setContents(contents);    

  console.log(prevProps.data === nextProps.data) // true
...

```
immutable하게 복사
- Array의 경우 
    - var b = Array.from(<code>복사할 array</code>);
- Object의 경우
    - var b = Object.assign({}, <code>복사할객체</code>);
- **차라리 immutable.js를 사용하자.**