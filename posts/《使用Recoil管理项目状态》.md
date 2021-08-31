# 一、recoil简单介绍

`recoil`是Facebook推出的react状态管理库。与其他状态管理库的不同之处在于，Recoil使用简单，有类似于vue中的计算属性的特性，能够高性能的渲染。

# 二、recoil核心api
**非常重要的一点是：在recoil的api使用中，key是必须的属性。并且key必须是全局唯一的。**原因如下：
>Atom 需要一个唯一的 key 值，该 key 可用于调试、持久化以及使用某些高级的 API，这些 API 可让你查看所有 atom 的图。两个 atom 不应拥有相同的 key 值，因此请确保它们在全局上的唯一性。

1. `atom`：`atom`是recoil核心api，它相当于react中的state。也就是状态。它的使用方法如下所示：
```ts
const atomState = atom({
    key:"atomState",
    default:0
})
```
2. `selector`:`selector`的功能类似于vue中的computed属性，它可以依托于一个atom，然后派生出新的值。它的使用方法如下所示：
```ts
const selectorState = selector({
    key:"selectorState",
    get:({get})=>{
        const _val = get(atomState)
        return _val + 1
    }
})
```
当`selector`没有指定set方法的时候，默认是只读的，没有办法对其进行赋值。
3. `Loadable`:`Loadable`对象代表 Recoil atom 或 selector 的当前状态。能够对这个对象返回的状态进行一些自己的处理，比如状态还在loading的时候就显示loading过渡等等。
```ts
function UserInfo({userID}) {
  const userNameLoadable = useRecoilValueLoadable(userNameQuery(userID));setState
  switch (userNameLoadable.state) {
    case 'hasValue':
      return <div>{userNameLoadable.contents}</div>;
    case 'loading':
      return <div>Loading...</div>;
    case 'hasError':
      throw userNameLoadable.contents;
  }
}
```

4. `useRecoilState`:`useRecoilState`和useState的用法一致，可以对存储在recoil中的状态进行读写操作。
```ts
const [state, setState] = useRecoilState(state的名称);
```

5. `useRecoilValue`:当只需要读一个值，而不需要写的时候可以使用useRecoilValue。
```ts
const names = useRecoilValue(namesState);
```

6. `useSetRecoilState`:返回一个 setter 函数，用来更新可写 Recoil state 的值。返回一个可以用来异步改变 state 的 setter 函数。可以传给此 setter 函数一个新的值，也可以传入一个更新函数，此函数接受上一次的值作为其参数。
```ts
const setNamesState = useSetRecoilState(namesState);
```
> 当一个组件需要写入而不需要读取 state 时，推荐使用此 hook。如果组件使用了 useRecoilState() 来获取 setter 函数，那么同时它也会订阅更新，并在 atom 或 selector 更新时重新渲染。使用 useSetRecoilState() 允许组件在值发生改变时而不用给组件订阅重新渲染的情况下设置值。

7. `useResetRecoilState`:返回一个函数，用来把给定 state 重置为其初始值。
```ts
const TodoResetButton = () => {
  const resetList = useResetRecoilState(todoListState);
  return <button onClick={resetList}>Reset</button>;
};
```

> 使用 useResetRecoilState() 可将组件的 state 重置为默认值，无需订阅组件，并且每当 state 改变时会重新渲染该组件。
# 三、使用recoil实现一个todoList

# 四、recoil、context、redux三者之间的对比