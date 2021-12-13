# React

## 1. react hooks

### 1. useState

​	useState是react自带的一个hook函数，他的作用是用来声明状态变量

1. 声明

   ```js
   const [count, setCount] = useState(0)
   ```

2. 读取

   ```html
   <p>You clicked {count} times</p>
   ```

3. 使用

   ```html
   <button onClick={()=>{setCount(count+1)}}>click me</button>
   ```

4. 多状态声明的注意事项

   ```js
   const [age, setAge] = useState(18);
   const [ sex , setSex ] = useState('男')
   const [ work , setWork ] = useState('前端程序员')
   ```

   **React是根据useState出现的顺序来确定对应的state，因此React Hooks不能出现在条件判断语句中，因为它必须有完全一样的渲染顺序。**

### 2. useEffect

1. React首次渲染和之后的每次渲染都会调用一遍`useEffect`函数，而之前我们要用两个生命周期函数分别表示首次渲染`componentDidMonut`和更新导致的重新渲染`componentDidUpdate`。

2. `useEffect`中定义的函数的执行不会阻碍浏览器更新视图，也就是说这些函数时异步执行的，而`componentDidMonut`和`componentDidUpdate`中的代码都是同步执行的。

3. `useEffect`的第二个参数是一个数组，数组中可以写入很多状态对应的变量，意思是当状态值发生变化时，我们才进行解绑。但是当传空数组`[]`时，就是当组件将被销毁时才进行解绑，这也就实现了`componentWillUnmount`的生命周期函数。

   ```js
   function Jinx() {
     useEffect(()=>{
       console.log('useEffect=>jinx的含义就是jinx')
       return ()=>{
       	console.log('jinx的含义就是jinx')
     	}
     },[])
     return <h2>JSPang.com</h2>;
   }
   ```

### 3. useContext

​	在用类声明组件时，父子组建的传值是通过组件属性和props进行的，而函数声明组件没有constructor构造函数也就没有了props的接收，因此hooks为我们准备了useContext。它可以帮助我们跨越组件层级直接传递变量，实现共享。

​	`useContext`和`redux`的作用是不同的，一个解决的是组件之间值传递的问题，一个是应用中统一管理状态的问题，但通过和`useReducer`的配合使用，可以实现类似`Redux`的作用。

​	步骤：

+ createContext函数创建context

+ useContext接受上下文变量

  ```js
  import React, { useState , createContext, useContext } from 'react';
  //===关键代码
  const CountContext = createContext()
  function Counter(){
    const count = useContext(CountContext)
    return (<h2>{count}</h2>)
  }
  function Example(){
      const [ count , setCount ] = useState(0);
  
      return (
          <div>
              <p>You clicked {count} times</p>
              <button onClick={()=>{setCount(count+1)}}>click me</button>
              {/*======关键代码 */}
              <CountContext.Provider value={count}>
                <Counter />
              </CountContext.Provider>
          </div>
      )
  }
  export default Example;
  ```

### 4. useReducer

1. reducer

   reducer是一个函数(state, action)=> newState:接受当前应用的state和出发的动作action，计算并返回最新的state。

2. useReducer接收两个参数

   第一个参数：reducer函数

   第二个参数：初始化的state

   返回值为最新的state和dispatch函数（用来触发reducer函数，计算对应的state）

   ```js
   const [state, dispatch] = useReducer(reducer,initState);
   ```

### 5. useMemo

### 6. useRef

### 7.hook规则

1. 只在最顶层使用Hook，不要在条件或嵌套函数中调用hook。
2. 

