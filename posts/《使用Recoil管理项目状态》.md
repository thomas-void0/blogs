# 一、recoil简单介绍

`recoil`是Facebook推出的react状态管理库。与其他状态管理库的不同之处在于，Recoil使用简单，有类似于vue中的计算属性的特性，能够高性能的渲染。

# 二、recoil核心api
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

# 三、使用recoil实现一个todoList

# 四、recoil、context、redux三者之间的对比