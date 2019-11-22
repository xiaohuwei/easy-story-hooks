# easy-story-hooks

![](https://cdn.xiaohuwei.cn/2977740a53948b0e06783984cbb41b10)

![](<https://img.shields.io/badge/author-Hzdy-red.svg?style=for-the-badge&logo=appveyor>)

[![AppVeyor](https://img.shields.io/appveyor/ci/doyoe/css-handbook.svg)](https://ci.appveyor.com/project/doyoe/css-handbook) [![AppVeyor](https://img.shields.io/static/v1.svg?label=lisense&message=MIT&color=success&?style=flat&logo=appveyor)](https://xiaohuwei.cn)  [![AppVeyor](https://img.shields.io/static/v1.svg?label=link&message=996.icu&color=orange)](https://996.icu/#/zh_CN)



🌍   [English](https://www.npmjs.com/package/easy-story-hooks) | [简体中文](https://github.com/xiaohuwei/easy-story-hooks)



> 基于`react hooks` 和 `EventTarget` 实现的最小全局状态管理，可以在组件之间共享全局状态。高性能就像使用`useState`一样简单。

## 使用简单 最简单的全局状态管理

>仅需使用两个步骤，即可初始化全局状态，并将组件状态在两个方向上都绑定到全局状态。与其他全局状态管理工具相比，使用此库不需要对原始代码进行太多修改。仅管理状态仓库，并且修改全局状态的方法返回到组件的内部调用。就像useState一样易于使用！希望世界上不再有困难的全局状态管理。

## 与redux相比，这非常简单！舍弃redux！

> 基于`react hooks`和`EventTarget`全局状态可以在任何组件中使用，并且所有组件的最外层不需要包装`context.provider` Redux主要由`store`，`action组成`，`reducer`等，太大，太复杂，麻烦，组件无用的刷新太多，性能低下。

## 将组件状态绑定到全局状态

> 组件状态更改时的全局状态更改全局状态更改时的组件状态更改高性能，减少了无用的组件刷新而不是使用上下文刷新组件，而是使用setstate来刷新单个组件。如果使用上下文，将导致大量组件的无用刷新。

## 开始

~~~node
npm i easy-story-hooks -S
~~~
或者
~~~node
cnpm i easy-story-hooks -S
~~~
或者
~~~node
yarn add easy-story-hooks
~~~

## 在您的React项目中

```js
import {changeState,useStore,initState,getState} from "easy-story-hooks";
```

### initState

> 函数`initState`用于生成状态的初始值，并且可以多次使用。参数是一个`object`，键名是全局状态名，键值是全局状态初始值。

### useStore

> 函数`useStore`用于订阅全局状态，组件状态在两个方向上都绑定到全局状态。第一个参数是`string`，它是全局状态名称。返回值是一个`Array`，它返回一个有状态值和一个更新它的函数。

### getState

> 函数`getState`用于读取全局状态。

### changeState

> 组件更新状态，用于更改全局状态并通知所有订阅状态，第一个参数是全局状态名称，第二个参数是更新后的状态值，或者函数返回新的状态值。



## Typescript 中的 Api

```js
function useStore(name: string): [any, Function];
function changeState(keyname: string, newvalue: any): void;
function getState(): {
  [key: string]: any;
};
function initState(jsonobject: {
  [key: string]: any;
}): {
  [key: string]: any;
};
```

## 基本语法

### 就像useState一样易于使用！

```js
import React, { useState } from "react";
const [count, setCount] = useState(0);
```

### easy-story-hooks

```js
import React,{useEffect,useState} from 'react';
import {useStore,initState} from "easy-story-hooks";
const App = ()=>{
  initState({
    count:1,
  })
  const [number, setnumber] = useStore("count");
  return (
    <>
    <h1>{number}</h1>
    <button onClick={()=>setnumber(number+1)}>Add one</button>
    </>
  )
}
export default App;
```

### 当然，您可以使用 `changeState`

```js
import React,{useEffect,useState} from 'react';
import {useStore,initState,changeState} from "easy-story-hooks";
const App = ()=>{
  initState({
    count:1,
  })
  const increment = ()=> {
    changeState("count", a => a + 1);
  }
  const [number, setnumber] = useStore("count");
  return (
    <>
    <h1>{number}</h1>
    <button onClick={increment}>Add one</button>
    </>
  )
}
export default App;
```

### 子组件读取全局状态

```js
import React from 'react';
import {getState,changeState} from "easy-story-hooks";
const Test = ()=>{
    let test = getState().count
    const remove = () => {
        changeState("count", a => a - 1);
    }
    return (
        <>
        <h1>{test}</h1>
        <button onClick={remove}>Subcomponent changes count</button>
        </>
    )
}
export default Test;
```



