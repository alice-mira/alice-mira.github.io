---
title: 前端梳理React生态
tags: [前端,react]
date: 2025-12-04 08:08:08
---

## 前言

国庆去趟了杭州，但是人太多了，走路都觉得空气很闷，天气也很热，玩了两天就回宿舍躺了，感觉人太多，看不到风景，而且消费也很高，性价比不是很值得，就呆在公寓，看了两本书，有一本是名著，《呼啸山庄》虽然是写的是爱情，但爱情背后是人性。爱情啊，这个课题本来就是让人很难读懂得，关于爱，也看了一篇文章。关于爱上人渣得，爱上人渣，或是那些求而不得甚至是受制于禁忌的爱，本质上也是在追求这种刺激，或者说正是因为这样的对象能给自己麻木的感官更大的刺激，从而误以为这就是「爱」的本质，就像是人们虽然知道「吊桥效应」，但在当下那种面红耳赤心跳加速的感官，其实是很难理性地进行拆解和分析。

青楼女子最会撩人的不是她会多少曲谱、会多少诗词、会多么的千杯不倒，而是在当下故意弹错的那一弦，让那个心念已久的小情郎抬头与自己看似不经意地四目交接。

好吧回归正题，也整理一下，react生态得相关问题，跟知识点。

## React

### Hooks

#### 常见的hooks用法以及使用

**1\. 基础状态与副作用 Hooks**

* **`useState`**：管理组件内部状态，支持多次调用管理多个独立状态。  
   * 用法：`const [state, setState] = useState(initialValue)`  
   * 特点：状态更新异步，依赖旧状态时用函数形式（`setState(prev => newVal)`）。
* **`useEffect`**：处理组件副作用（数据请求、订阅、DOM 操作等）。  
   * 用法：`useEffect(effectFn, dependencies)`  
   * 特点：依赖数组控制执行时机，返回清理函数处理卸载逻辑，空数组 `[]` 仅执行一次。

**2\. 状态与逻辑管理 Hooks**

* **`useReducer`**：管理复杂状态逻辑，替代 `useState` 处理多状态关联场景。  
   * 用法：`const [state, dispatch] = useReducer(reducer, initialState)`  
   * 适用场景：表单处理、多步骤状态切换等复杂状态逻辑。
* **`useContext`**：跨组件共享状态，避免 props 层层传递。  
   * 用法：`const value = useContext(Context)`  
   * 前提：需配合 `createContext` 创建上下文和 `Context.Provider` 提供值。

**3\. 性能优化 Hooks**

* **`useCallback`**：记忆化函数，避免子组件因函数引用变化频繁重渲染。  
   * 用法：`const memoizedFn = useCallback(fn, dependencies)`  
   * 适用场景：传递给子组件的回调函数（如 `onClick`）。
* **`useMemo`**：记忆化计算结果，避免每次渲染重复执行耗时计算。  
   * 用法：`const memoizedValue = useMemo(calculateFn, dependencies)`  
   * 注意：用于**计算密集型操作**，不滥用（避免额外性能开销）。

**4\. 引用与 DOM 操作 Hooks**

* `useRef`  
：在多次渲染间保存值，或直接访问 DOM 元素。  
   * 用法：`const ref = useRef(initialValue)`  
   * 特点：修改 `ref.current` 不触发重渲染，可用于存储计时器、DOM 引用等。

**5\. 自定义 Hooks**

* **核心作用**：封装可复用的组件逻辑，抽离重复代码。
* **命名规则**：必须以 `use` 开头（如 `useWindowSize`、`useFetch`）。
* **示例场景**：封装数据请求逻辑、监听窗口大小、表单验证等。

**6\. Hooks 使用规则**

* 只能在**函数组件顶层**或**自定义 Hooks 中**调用，不可在条件、循环、嵌套函数中使用。
* 每次组件渲染时，Hooks 调用顺序必须**保持一致**。
* 自定义 Hooks 需遵循命名规范，确保 React 正确识别。

**7\. 适用场景速查表**

| Hook        | 核心场景          | 解决问题                 |
| ----------- | ------------- | -------------------- |
| useState    | 简单状态管理        | 函数组件无状态的问题           |
| useEffect   | 副作用处理         | 生命周期逻辑分散的问题          |
| useReducer  | 复杂状态逻辑        | 多状态关联、状态更新逻辑复杂       |
| useContext  | 跨组件状态共享       | props 透传繁琐问题         |
| useCallback | 优化子组件渲染       | 函数引用频繁变化导致重渲染        |
| useMemo     | 优化计算性能        | 重复执行耗时计算             |
| useRef      | 保存跨渲染值或操作 DOM | 获取 DOM 元素、存储不触发重渲染的值 |

#### useCallBack与useMemo怎么做得缓存？

`useCallback` 和 `useMemo` 的缓存是存储在 **组件实例的内部状态** 中的，由 React 内部机制管理。

具体来说，当组件首次渲染时，React 会为组件实例创建一块专属的 “内存空间”，用于存储该组件中所有 Hook（包括 `useState`、`useEffect`、`useCallback`、`useMemo` 等）的状态和缓存信息。

* 对于 `useCallback`：缓存的函数引用会被存储在这块空间中，与组件实例绑定。
* 对于 `useMemo`：缓存的计算结果也会被存储在这块空间中，同样与组件实例绑定。

**几个关键特点：**

1. **与组件实例绑定**：每个组件实例（比如同一个组件渲染多次，会产生多个实例）都有自己独立的缓存空间，互不干扰。例如，两个 `Parent` 组件实例，它们的 `useCallback` 缓存的函数是各自独立的。
2. **随组件生命周期存在**：当组件被卸载时，其对应的缓存空间会被 React 自动清理，不会造成内存泄漏。
3. **依赖项驱动更新**：每次组件重新渲染时，React 会检查 `useCallback`/`useMemo` 的依赖项数组。如果依赖项没变，就直接复用缓存中的值；如果依赖项变了，就更新缓存并存储新的值。

简单说，缓存既不是全局变量，也不是浏览器的本地存储（如 `localStorage`），而是 React 为每个组件实例在内存中维护的一块临时存储区域，专门用于优化组件渲染性能。

#### useCallBack与useMemo页面销毁得时候怎么做得清理？

`useCallback` 和 `useMemo` 本身并不需要手动清理缓存，因为它们的缓存会随着**组件实例的销毁而自动被清理**，具体机制如下：

**1\. 缓存的生命周期与组件实例绑定**

`useCallback` 和 `useMemo` 的缓存数据（函数引用或计算结果）是**存储在组件实例的内部状态中**的，完全依附于组件实例的生命周期：

* 当组件首次渲染时，React 为该组件创建一个实例，并在实例中分配空间存储这些缓存。
* 当组件被销毁（从 DOM 中移除）时，整个组件实例会被 React 标记为 “可回收”。

**2\. 清理依赖 JavaScript 垃圾回收（GC）**

当组件实例被销毁后，它所占用的内存（包括 `useCallback`/`useMemo` 的缓存）会成为 JavaScript 垃圾回收机制的目标：

* 由于组件实例已不再被任何引用（比如父组件不再渲染它，没有其他变量持有它的引用），垃圾回收器会自动识别并释放这部分内存。
* 缓存数据本身不涉及 “副作用”（如事件监听、定时器、网络请求等），因此不需要像 `useEffect` 那样手动编写清理函数（如移除事件监听）。

**3\. 为什么不需要手动清理？**

`useCallback` 和 `useMemo` 的核心是 “缓存值”，而不是 “副作用”：

* 它们不产生需要手动终止的外部资源占用（如 DOM 事件、定时器 ID 等）。
* 缓存的本质是内存中的临时数据，当宿主（组件实例）被销毁后，这些数据自然失去存在意义，会被自动回收。

**总结**

`useCallback` 和 `useMemo` 的缓存清理是**自动完成**的： 组件销毁 → 组件实例被标记为可回收 → JavaScript 垃圾回收器释放实例占用的内存（包括缓存数据）。 开发者无需手动干预，也没有专门的 API 用于清理它们的缓存。

#### useCallBack与useMemo的使用场景以及区别

可能存在的误区包括：何时使用哪一个，是否所有函数都需要用useCallback包裹，或者是否所有计算都需要useMemo。需要指出不必要的使用可能导致性能下降，而不是提升。

在 React 中，`useCallback` 和 `useMemo` 是性能优化工具，但并非所有场景都需要使用。以下是使用指南和最佳实践：

_1\. `useCallback` 的适用场景_\*

`useCallback` 用于缓存函数引用，避免因函数重新创建导致子组件不必要的重新渲染。**仅在以下情况使用**：

* **传递给依赖引用相等性的子组件**（如使用 `React.memo` 的组件）。
* **作为依赖项传递给其他 Hook**（如 `useEffect`、`useMemo`）。

**示例：优化子组件渲染**

```jsx
// 子组件使用 React.memo 浅比较 props
const ChildComponent = React.memo(({ onClick }) => {
  return <button onClick={onClick}>Click</button>;
});

// 父组件使用 useCallback 缓存函数
function Parent() {
  const [count, setCount] = useState(0);
  
  // ✅ 只有依赖项变化时才重新创建函数
  const handleClick = useCallback(() => {
    setCount(count + 1);
  }, [count]); // 依赖 count，必须包含在依赖数组中

  return <ChildComponent onClick={handleClick} />;
}

```

**错误用法（不要过度使用）**

```jsx
function Parent() {
  // ❌ 不必要的 useCallback：函数未传递给子组件
  const handleClick = useCallback(() => {
    console.log('Clicked');
  }, []);

  return <button onClick={handleClick}>Click</button>;
}

```

**2\. `useMemo` 的适用场景**

`useMemo` 用于缓存计算结果，避免重复执行高开销的计算。**仅在以下情况使用**：

* **计算成本高昂**（如大量数据排序、复杂计算）。
* **对象 / 数组作为 props 传递给依赖引用相等性的子组件**。

**示例：缓存昂贵计算**

```jsx
function Example({ items }) {
  // ✅ 只有 items 变化时才重新排序
  const sortedItems = useMemo(() => {
    return [...items].sort((a, b) => a.name.localeCompare(b.name));
  }, [items]);

  return <List items={sortedItems} />;
}

```

**示例：避免子组件不必要的重新渲染**

```jsx
const Child = React.memo(({ style }) => {
  return <div style={style}>Child</div>;
});

function Parent() {
  const [count, setCount] = useState(0);
  
  // ✅ 只有 count 变化时才重新创建 style 对象
  const style = useMemo(() => {
    return { color: count > 5 ? 'red' : 'blue' };
  }, [count]);

  return <Child style={style} />;
}

```

**3\. 何时不使用？**

**不要用 `useCallback` 包裹所有函数**

* **函数未传递给子组件**：普通事件处理函数不需要缓存。
* **依赖频繁变化**：若依赖数组中的值频繁更新，`useCallback` 可能导致更多性能开销。

**不要用 `useMemo` 缓存所有计算**

* **计算成本低**：简单计算（如 [`a + b`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.a.md)）不需要缓存。
* **每次渲染必须执行**：如直接操作 DOM、生成随机数等。

```jsx
function Example() {
  // ❌ 不必要的 useMemo：计算成本低
  const sum = useMemo(() => a + b, [a, b]);

  // ✅ 直接计算更高效
  const sum = a + b;

  return <div>{sum}</div>;
}

```

_4\. 性能反模式_\*

**过度依赖引用相等性**

过度使用 `React.memo`、`useCallback` 和 `useMemo` 可能导致：

* **代码复杂度增加**：依赖数组管理困难。
* **内存占用增加**：缓存大量函数 / 对象。
* **性能下降**：比较依赖项的开销可能超过重新计算的成本。

**错误的依赖数组**

* **遗漏依赖项**：导致闭包陷阱（如 `useEffect` 中使用旧值）。
* **包含不必要的依赖**：导致函数 / 计算频繁重新创建。

**5\. 最佳实践**

1. **优先编写清晰的代码**，而非追求性能优化。
2. **使用 Profiler 工具**（如 React DevTools）定位真正的性能瓶颈。
3. **仅在必要时使用 `useCallback` 和 `useMemo`**，并确保依赖数组正确。
4. **避免过早优化**：大多数情况下，React 的默认渲染性能已经足够好。

**总结**

| **场景**             | **是否使用** |
| ------------------ | -------- |
| 普通事件处理函数           | ❌ 不需要    |
| 传递给 React.memo 的函数 | ✅ 需要     |
| 高开销的计算             | ✅ 需要     |
| 简单计算               | ❌ 不需要    |
| 对象 / 数组作为 props 传递 | ✅ 推荐使用   |

记住：**优化的目标是减少不必要的工作，而非避免所有工作**。

#### 父组件渲染是否引起子组件的渲染

在 React 中，**父组件的渲染并不总是导致子组件的渲染**，这取决于以下因素：

1. **默认行为：父组件渲染会触发子组件渲染**

React 的默认行为是：**当父组件重新渲染时，其所有子组件都会重新渲染**（无论 props 是否变化）。这是因为 React 会递归比较虚拟 DOM 树。

```jsx
function Parent() {
  const [count, setCount] = useState(0);

  // 每次 Parent 渲染时，Child 都会被重新渲染
  return <Child message="Hello" />;
}

function Child({ message }) {
  console.log("Child rendered"); // 每次父组件渲染时都会执行
  return <div>{message}</div>;
}

```

1. **使用 `React.memo` 避免不必要的渲染**

`React.memo` 是一个高阶组件，它会浅比较子组件的 props。**只有当 props 发生变化时**，子组件才会重新渲染。

```jsx
// ✅ Child 只会在 props 变化时重新渲染
const Child = React.memo(({ message }) => {
  console.log("Child rendered");
  return <div>{message}</div>;
});

```

**注意事项**：

* 浅比较的局限性  
```txt  
React.memo  
```  
仅检查 props 的引用是否变化。如果传递对象 / 数组 / 函数，即使内容相同，引用变化也会触发重新渲染。  
```jsx  
function Parent() {  
  const [count, setCount] = useState(0);  
  // ❌ 每次渲染都会创建新的对象，导致 Child 重新渲染  
const data = { value: "static" };  
    
return <Child data={data} />;  
}  
```

```ini
### 3. **函数 / 对象引用变化导致的渲染**

如果父组件在每次渲染时创建新的函数、对象或数组，即使内容相同，也会导致子组件重新渲染（即使使用了 `React.memo`）。

```jsx
function Parent() {
  const [count, setCount] = useState(0);

  // ❌ 每次渲染都会创建新的函数
  const handleClick = () => {
    console.log("Clicked");
  };

  return <Child onClick={handleClick} />; // Child 会重新渲染
}

// 即使使用 React.memo，onClick 的引用变化仍会触发渲染
const Child = React.memo(({ onClick }) => {
  return <button onClick={onClick}>Click</button>;
});

```

**解决方案**：使用 `useCallback` 缓存函数引用。

```jsx
// ✅ 使用 useCallback 确保函数引用不变
const handleClick = useCallback(() => {
  console.log("Clicked");
}, []); // 空依赖数组表示只创建一次函数

```

1. **状态提升与上下文导致的渲染**

如果多个组件共享上层组件的状态（如状态提升或 Context API），上层组件的状态更新会导致所有依赖该状态的子组件重新渲染。

```jsx
// 使用 Context API 时
const MyContext = React.createContext();

function Parent() {
  const [count, setCount] = useState(0);
  
  return (
    <MyContext.Provider value={count}>
      <Child1 /> {/* 依赖 count，会重新渲染 */}
      <Child2 /> {/* 不依赖 count，但仍会重新渲染（默认行为） */}
    </MyContext.Provider>
  );
}

```

**优化方法**：

* 将不依赖状态的子组件移出提供者。
* 使用多个 Context 分离关注点。
1. **强制子组件重新渲染**

即使使用 `React.memo`，也可以通过传递唯一的 key 来强制子组件重新渲染。

```jsx
function Parent() {
  const [count, setCount] = useState(0);
  
  // 每次 count 变化时，Child 都会重新创建（而非更新）
  return <Child key={count} message="Hello" />;
}

```

**总结：父组件渲染对子组件的影响**

| 条件                                     | 子组件是否重新渲染 |
| -------------------------------------- | --------- |
| 子组件未使用 React.memo                      | ✅ 总是重新渲染  |
| 子组件使用 React.memo，且 props 未变化           | ❌ 不重新渲染   |
| 子组件使用 React.memo，但 props 中的对象 / 函数引用变化 | ✅ 重新渲染    |
| 父组件通过 key 强制更新                         | ✅ 重新渲染    |

**性能优化建议**：

* 使用 `React.memo` 包裹纯组件。
* 使用 `useCallback` 和 `useMemo` 避免不必要的引用变化。
* 使用 Profiler 工具定位渲染瓶颈。

#### useEffect与useLayoutEffect的区别

在 React 中，`useEffect` 和 `useLayoutEffect` 是用于处理副作用的 Hooks，但它们的执行时机和适用场景有重要区别。

**1\. `useEffect`（默认副作用）**

* **执行时机**：在浏览器完成渲染后（视觉更新已完成），异步执行。
* 特点：  
   * 不会阻塞页面渲染，适合处理不影响视觉的副作用（如数据获取、订阅、日志）。  
   * 可能在多次渲染后合并执行（如在浏览器空闲时）。

**示例**

```jsx
useEffect(() => {
  // 在页面渲染完成后执行
  console.log('Effect 执行');
  
  return () => {
    // 清理函数在组件卸载前或下次 effect 执行前调用
    console.log('Effect 清理');
  };
}, []); // 空依赖数组表示只在挂载和卸载时执行

```

**2\. `useLayoutEffect`（布局副作用）**

* **执行时机**：在浏览器完成 DOM 更新但尚未绘制到屏幕前，同步执行。
* 特点：  
   * 会阻塞页面渲染，适合需要读取 DOM 布局并立即更新的场景（如测量元素尺寸、滚动位置）。
* 总是在 `useEffect` 之前执行。

**示例**

```jsx
useLayoutEffect(() => {
  // 在 DOM 更新后、绘制前执行
  const width = elementRef.current.offsetWidth;
  console.log('元素宽度:', width);
  
  // 可以同步更新 DOM（如调整样式）
  elementRef.current.style.opacity = 0.8;
  
  return () => {
    // 清理函数在组件卸载前或下次 effect 执行前调用
    console.log('LayoutEffect 清理');
  };
}, []);

```

**3\. 核心区别对比**

| **特性**     | useEffect  | useLayoutEffect       |
| ---------- | ---------- | --------------------- |
| **执行时机**   | 渲染后（异步）    | 渲染前（同步）               |
| **是否阻塞渲染** | ❌ 否        | ✅ 是                   |
| **适用场景**   | 数据获取、订阅、日志 | DOM 测量、布局调整、同步 DOM 更新 |
| **性能影响**   | 低（不阻塞用户界面） | 高（可能导致视觉闪烁）           |

**4\. 何时使用哪个？**

**优先使用 `useEffect`**

* 大多数副作用场景（如网络请求、设置定时器）。
* 不依赖 DOM 布局的操作。

**使用 `useLayoutEffect` 的情况**

* 需要读取 DOM 布局信息（如元素尺寸、滚动位置）。
* 需要在用户看到更新前同步修改 DOM（如避免视觉闪烁）。

**示例：避免视觉闪烁**

```jsx
function App() {
  const [width, setWidth] = useState(0);
  const ref = useRef(null);

  // ❌ 使用 useEffect 可能导致闪烁（先显示默认值，再更新）
  useEffect(() => {
    const w = ref.current.offsetWidth;
    setWidth(w); // 会触发额外渲染
  }, []);

  // ✅ 使用 useLayoutEffect 可避免闪烁（在绘制前更新）
  useLayoutEffect(() => {
    const w = ref.current.offsetWidth;
    setWidth(w); // 同步更新，用户看不到中间状态
  }, []);

  return <div ref={ref} style={{ width: `${width}px` }}>Hello</div>;
}

```

**5\. 性能注意事项**

* **避免在 `useLayoutEffect` 中执行耗时操作**，否则会阻塞页面渲染，导致卡顿。
* 如果副作用不需要操作 DOM，始终使用 `useEffect` 以保持最佳性能。

**总结**

| **场景**        | 推荐 Hook         |
| ------------- | --------------- |
| 数据获取、订阅       | useEffect       |
| DOM 测量、同步样式更新 | useLayoutEffect |
| 避免视觉闪烁        | useLayoutEffect |
| 优化性能          | 优先使用 useEffect  |

记住：**`useLayoutEffect` 是 `useEffect` 的同步版本，仅在必要时使用**。

#### 为什么不能在条件语句中进行使用

React Hooks 不能在条件语句中执行（即使条件 “一直为真”），核心原因与 React 内部对 Hooks 的**状态管理机制**和**调用顺序依赖**有关。

**1\. React 依赖 Hooks 的调用顺序识别状态**

React 内部通过 \*\*“调用顺序”**来跟踪每个 Hook 对应的状态。例如，当你在组件中多次调用 `useState` 或 `useEffect` 时，React 会维护一个**链表结构 \*\*，按调用顺序存储每个 Hook 的状态信息（如 `useState` 的值、`useEffect` 的依赖等）。

每次组件渲染时，React 会按**相同的顺序**遍历这个链表，将 Hook 调用与对应的状态关联起来。如果 Hooks 的调用顺序发生变化，React 就会 “认错” 状态，导致状态混乱或报错。

**2\. 条件语句会破坏调用顺序的稳定性**

即使条件 “一直为真”，将 Hook 放在条件语句中也会**破坏 React 对 “调用顺序不变” 的假设**。

举个例子：

```jsx
function MyComponent() {
  if (true) { // 即使条件永远为真
    const [count, setCount] = useState(0); // ❌ 错误：Hook 在条件中
  }
  const [name, setName] = useState('');
  // ...
}

```

表面上看，[`if (true)`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.true.md) 似乎不会改变执行顺序，但 React 无法 “预知” 这个条件未来是否会变化。假设未来某天，这个条件被修改为 `if (someFlag)`，而 `someFlag` 在某次渲染中变为 [`false`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.false.md)，此时：

* 第一次渲染：执行 `useState(0)` → 执行 `useState('')`（顺序：\[0, 1\]）
* 第二次渲染：不执行 `useState(0)` → 执行 `useState('')`（顺序：\[1\]）

React 会发现第二次渲染的 Hook 数量 / 顺序与第一次不一致，直接抛出错误：[`Hooks can only be called inside the body of a function component`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.function.md)。

**3\. 规则的设计是为了 “防患于未然”**

React 禁止在条件、循环、嵌套函数中调用 Hooks，本质上是一种**强制约束**，确保开发者写出的代码符合 “Hook 调用顺序稳定” 的要求。

即使你能保证当前条件 “一直为真”，但代码维护中可能会被修改（比如添加 else 分支、调整条件判断），此时隐藏的顺序问题就会暴露。React 通过提前禁止这种写法，避免了潜在的难以调试的状态错误。

**总结**

Hooks 的调用必须满足 **“在组件顶层、每次渲染顺序一致”**，这与 React 内部通过顺序跟踪状态的机制紧密相关。条件语句（即使条件恒真）会破坏这种稳定性，因此被 React 明确禁止。这一规则不是技术限制，而是为了保证组件状态管理的可靠性。

### react fiber跟useEffect是怎么关联的

React Fiber 和 useEffect 看似是 React 中两个独立的概念（Fiber 是架构底层引擎，useEffect 是上层 Hooks API），但它们的关联体现在 **Fiber 架构为 useEffect 的执行时机、调度优先级和副作用管理提供了底层支撑**。具体关联可以从以下几个角度理解：

1. **Fiber 架构的两阶段工作模式决定了 useEffect 的执行时机**

React Fiber 核心是将渲染工作拆分为「协调（Reconciliation）」和「提交（Commit）」两个阶段：

* **协调阶段**：找出前后 DOM 树的差异（Diff 算法），可被中断、暂停或恢复（为了高优先级任务让路，比如用户输入）。
* **提交阶段**：执行实际的 DOM 操作（插入 / 更新 / 删除节点），此阶段不可中断。

而 `useEffect` 的副作用执行时机，正依赖于 Fiber 的这两个阶段：

* **协调阶段**：React 会在 Fiber 节点上标记副作用（包括 `useEffect` 的回调和清理函数），并判断依赖数组是否变化，决定是否需要执行新的副作用或清理旧的副作用。
* **提交阶段之后**：`useEffect` 的回调函数会在 DOM 更新完成（提交阶段结束）后异步执行。这是因为 Fiber 允许在提交阶段后，将副作用调度到浏览器空闲时执行，避免阻塞主线程。
1. **Fiber 的调度机制控制 useEffect 的优先级**

Fiber 架构的核心能力是「优先级调度」—— 可以为不同任务分配优先级（如用户输入 > 渲染 > 副作用），高优先级任务可打断低优先级任务。

`useEffect` 的执行被归为「低优先级任务」，这正是由 Fiber 的调度机制（如 `scheduler` 包）实现的：

* 当组件渲染完成（提交阶段结束）后，React 不会立即执行 `useEffect` 回调，而是通过 Fiber 调度器（如 `requestIdleCallback` 或模拟的空闲时间检测）将其推迟到浏览器主线程空闲时执行。
* 这样做的好处是：避免副作用（如数据请求、日志打印）阻塞用户交互（如点击、输入）等高频优先级操作，保证应用响应性。
1. **Fiber 节点存储 useEffect 的副作用信息**

在 Fiber 架构中，每个组件对应一个 Fiber 节点，节点上有一个 `effectTag` 属性和 `effects` 链表，用于存储副作用相关信息：

* 当组件中使用 `useEffect` 时，React 会在协调阶段为对应的 Fiber 节点标记副作用类型（如 `PassiveEffect`，表示需要执行 `useEffect`）。
* 所有标记了副作用的 Fiber 节点会被串联成 `effects` 链表，在提交阶段结束后，React 会遍历这个链表，执行 `useEffect` 的回调函数（并处理清理逻辑）。

简单说：**Fiber 节点是 useEffect 副作用的「载体」**，没有 Fiber 对副作用的存储和追踪，React 无法知道哪些组件需要执行副作用。

1. **useEffect 的清理函数与 Fiber 的中断恢复**

当组件卸载或 `useEffect` 依赖变化时，需要执行清理函数（如取消订阅、清除定时器）。这一过程也依赖 Fiber 的特性：

* 在 Fiber 协调阶段，如果发现组件需要卸载或 `useEffect` 依赖变化，会先标记「需要执行清理函数」，并将其加入副作用链表。
* 由于 Fiber 支持任务中断，即使在协调阶段被高优先级任务打断，已标记的清理函数也会被妥善保存，待任务恢复后继续处理，确保清理逻辑不会丢失。

**总结**

React Fiber 是底层架构，为 `useEffect` 提供了：

* **执行时机的保障**（提交阶段后异步执行）；
* **优先级调度的能力**（低优先级，不阻塞主线程）；
* **副作用的存储与追踪**（通过 Fiber 节点的 `effects` 链表）。

可以说，`useEffect` 能以「不阻塞渲染、自动管理依赖和清理」的方式工作，其底层完全依赖于 Fiber 架构的设计。

`useEffect` 的执行时机可以简单概括为：**「渲染完成后执行，依赖控制执行频率，清理函数在卸载或重执行前触发」**。 它整合了类组件中 `componentDidMount`、`componentDidUpdate`、`componentWillUnmount` 三个生命周期的功能，通过依赖数组灵活控制副作用的执行时机。

### useEffect 第二个参数如果不要会造成什么问题

在 React 中，`useEffect` 的第二个参数（依赖数组）用于控制副作用的执行时机。如果省略这个参数，会导致以下问题：

1. **性能问题：副作用频繁执行**

`useEffect` 的回调函数会在**每次组件渲染完成后都执行**（包括初始渲染和所有更新渲染）。

如果副作用包含耗时操作（如 API 请求、大量 DOM 操作、复杂计算等），会导致组件每次更新都重复执行这些操作，显著降低性能，甚至引发页面卡顿。

1. **可能引发无限循环**

如果副作用内部修改了组件状态（如 `setState`），而状态变化又会触发组件重新渲染，会形成「渲染 → 副作用执行 → 状态更新 → 再次渲染」的无限循环，最终导致应用崩溃。

例如：

```javascript
function Counter() {
  const [count, setCount] = useState(0);

  // 省略第二个参数，每次渲染后都会执行
  useEffect(() => {
    // 修改状态 → 触发重新渲染 → 再次执行effect → ...无限循环
    setCount(prev => prev + 1);
  }); // 没有依赖数组

  return <div>{count}</div>;
}

```

1. **资源管理问题**

对于需要清理的副作用（如事件监听、定时器、订阅等），省略依赖数组会导致：

* 每次渲染都重复创建资源（如重复绑定事件）
* 清理函数（effect 回调返回的函数）会在每次渲染前执行，但可能无法彻底清理旧资源，最终导致内存泄漏。

例如：

```javascript
useEffect(() => {
  // 每次渲染都会新增一个事件监听（旧的可能没被正确清理）
  window.addEventListener('resize', handleResize);
  
  return () => {
    window.removeEventListener('resize', handleResize);
  };
}); // 没有依赖数组 → 多次绑定/解绑，可能残留监听

```

**正确做法**

* **空依赖数组 `[]`**：副作用仅在组件**初始渲染后执行一次**，类似类组件的 `componentDidMount`。
* **包含依赖项**：`[dep1, dep2]`，副作用仅在依赖项发生变化时执行，避免不必要的重复执行。

```javascript
// 仅初始渲染执行一次
useEffect(() => {
  fetchData();
}, []);

// 仅当 userId 变化时执行
useEffect(() => {
  fetchUser(userId);
}, [userId]);

```

总之，省略 `useEffect` 的第二个参数会导致副作用过度执行，引发性能、逻辑甚至崩溃问题，应根据实际需求明确指定依赖项。

### useEffect怎么渲染到浏览器

`useEffect` 本身并不直接参与「渲染到浏览器」的过程 ——React 中负责将组件渲染到浏览器 DOM 的是 React 的核心渲染机制（如协调阶段、提交阶段），而 `useEffect` 是在**渲染完成后**处理「副作用」的工具。它与浏览器渲染的关联在于：**它总是在组件已经渲染到浏览器 DOM 之后执行**，可以安全地与浏览器环境交互（如操作 DOM、添加事件监听等）。

具体流程：从状态更新到 `useEffect` 执行

1. **状态 / Props 变化触发渲染**当组件的 `state` 或 `props` 变化时，React 会触发重新渲染：  
   * 先执行组件函数，生成新的虚拟 DOM（VNode）。  
   * 进入「协调阶段（Reconciliation）」：对比新旧虚拟 DOM，计算出需要更新的 DOM 节点（Diff 算法）。
2. **提交阶段：更新浏览器 DOM**协调完成后，React 进入「提交阶段（Commit）」：  
   * 将计算出的 DOM 变化实际应用到浏览器 DOM 中（如插入、更新、删除节点）。  
   * 此时，浏览器已经完成了 DOM 的更新（可以理解为「已经渲染到浏览器了」）。
3. **`useEffect` 执行：在渲染后处理副作用**提交阶段结束后，React 会异步执行 `useEffect` 的回调函数：  
   * 此时 DOM 已经是最新的，可以安全地读取或修改 DOM（比如获取元素尺寸、添加滚动监听等）。  
   * 这一步是「非阻塞」的：`useEffect` 会被调度到浏览器主线程空闲时执行，不会阻塞用户交互或页面绘制。

**示例：`useEffect` 在渲染后操作 DOM**

比如在 `useEffect` 中获取渲染后的 DOM 元素属性：

```jsx
import { useState, useEffect, useRef } from 'react';

function Example() {
  const [count, setCount] = useState(0);
  const divRef = useRef(null);

  // 组件渲染到浏览器后执行
  useEffect(() => {
    // 此时 div 已经被渲染到 DOM 中，可以安全访问其属性
    if (divRef.current) {
      console.log('div 宽度:', divRef.current.offsetWidth);
    }
  }, [count]); // 依赖 count，count 变化后会重新执行

  return (
    <div ref={divRef} style={{ padding: count * 10 }}>
      点击次数: {count}
      <button onClick={() => setCount(c => c + 1)}>点击</button>
    </div>
  );
}

```

* 当点击按钮时，`count` 变化 → 组件重新渲染 → DOM 更新（div 的 padding 变化）→ `useEffect` 执行 → 读取到更新后的 div 宽度。

**关键区别：`useEffect` 与 `useLayoutEffect`**

如果需要在浏览器「绘制（paint）」之前执行副作用（比如同步修改 DOM 避免闪烁），可以用 `useLayoutEffect`，它的执行时机是：

* 提交阶段 DOM 更新后 **立即同步执行**（在浏览器绘制前），会阻塞渲染。

而 `useEffect` 是 **异步执行**（在浏览器绘制后），不会阻塞渲染，是大多数场景的首选。

**总结**

`useEffect` 不直接参与「渲染到浏览器」的过程，而是在**渲染完成（DOM 已更新）后**执行，专门用于处理需要与浏览器环境交互的副作用（如 DOM 操作、订阅、数据请求等）。它的执行时机确保了操作基于最新的 DOM 状态，且不会阻塞页面渲染。

### React 中rende函数的原理是什么？

**记忆点：类组件中表现为返回虚拟dom,描述UI结构**（props跟state改变进行调用，纯函数）

**React整体的渲染机制**

**1.生成虚拟dom=>2.协调器进行协调，对比旧的虚拟dom(diff算法)=>3.提交更新真实dom**

在 React 中，“render 函数” 的概念可以从两个层面理解：**类组件中的 `render()` 方法** 和 **React 整体的渲染机制**。前者是组件输出 UI 的入口，后者是 React 将组件描述转换为真实 DOM 的底层流程。

**一、类组件中 `render()` 方法的作用**

在类组件中，`render()` 是一个**必须实现的核心方法**，它的作用是： 根据组件当前的 `props` 和 `state`，返回一个**React 元素（虚拟 DOM）**，描述组件应该渲染的 UI 结构。

```jsx
class MyComponent extends React.Component {
  render() {
    // 根据 props 和 state 返回 React 元素
    return <div>Hello, {this.props.name}</div>;
  }
}

```

**核心特点**：

1. **纯函数特性**：`render()` 本身不修改组件状态，也不产生副作用（如数据请求、DOM 操作），仅根据输入（`this.props` 和 `this.state`）返回输出（React 元素）。
2. **条件触发**：当组件的 `props` 或 `state` 发生变化时，React 会**重新调用 `render()`**，生成新的 React 元素，为后续的 “DOM 更新” 做准备。

**二、React 渲染机制的底层原理**

React 的整体渲染流程可以分为**三个阶段**，`render()` 方法是触发这一流程的起点之一：

**1\. 生成虚拟 DOM（Virtual DOM）**

* **虚拟 DOM** 是一个轻量级的 JavaScript 对象，结构与真实 DOM 一致（包含标签名、属性、子元素等），但不涉及浏览器渲染层的操作。
* 类组件通过 `render()` 返回虚拟 DOM；函数组件则直接通过返回值生成虚拟 DOM（函数组件本身可视为一个 “render 函数”）。  
```jsx  
// 虚拟 DOM 的简化结构（实际由 React 内部创建）  
const virtualDOM = {  
  type: 'div',  
  props: {  
    children: 'Hello, React'  
  }  
};  
```

**2\. 协调（Reconciliation）：对比新旧虚拟 DOM（Diff 算法）**

当组件的 `props` 或 `state` 变化时，React 会生成**新的虚拟 DOM**，并与**旧的虚拟 DOM** 进行对比（这一过程称为 “协调”），找出两者的差异（“Diff”）。

React 的 Diff 算法有三个核心优化策略：

* **同层比对**：只对比同一层级的节点，不跨层级比较（减少复杂度）。
* **类型判断**：若节点类型（如 [`div`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.div.md) 与 [`span`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.span.md)）不同，直接销毁旧节点并创建新节点。
* **key 复用**：列表节点通过 `key` 属性标识唯一性，相同 `key` 的节点会被优先复用（避免不必要的销毁 / 创建）。  
```jsx  
// 旧虚拟 DOM  
<ul>  
  <li key="1">Item 1</li>  
  <li key="2">Item 2</li>  
</ul>  
// 新虚拟 DOM（只更新 Item 2，复用 Item 1）  
<ul>  
  <li key="1">Item 1</li>  
  <li key="2">Item 2 Updated</li>  
</ul>  
```

**3\. 提交（Commit）：更新真实 DOM**

协调阶段找出差异后，React 进入 “提交” 阶段，将差异**批量更新到真实 DOM** 中。

* 对于新增的虚拟 DOM 节点：创建对应的真实 DOM 元素并插入页面。
* 对于删除的虚拟 DOM 节点：移除对应的真实 DOM 元素。
* 对于修改的虚拟 DOM 节点：仅更新变化的属性（如 `className`、[`style`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.style.md) 等），而非重新创建整个节点。

**三、总结：render 函数在整体流程中的角色**

1. `render()` 是组件输出 UI 描述（虚拟 DOM）的入口，触发于 `props` 或 `state` 变化时。
2. React 通过对比新旧虚拟 DOM（Diff 算法），计算出最小更新范围，避免全量重渲染。
3. 最终只将必要的变更应用到真实 DOM，实现 “高效更新”（这也是 React 性能优势的核心原因）。

**简单来说：`render()` 负责 “描述 UI 应该是什么样”，而 React 底层机制负责 “高效地让真实 DOM 变成描述的样子”。**

### 什么是Suspense组件？它解决了什么问题？

**记忆点：：主要用于协调异步操作的加载状态，让组件在等待异步数据（如网络请求、代码分割）时能够优雅地显示占位内容（loading 状态），而无需手动管理复杂的加载逻辑。将异步加载的 “等待逻辑” 从组件中抽离，通过声明式方式统一管理加载状态**

**向上查找，并发控制（暂停低任务优先渲染用户相关内容），批量处理，（进行合并），react18，增强持数据加载与服务器渲染**

`Suspense` 是 React 16.6 引入的组件，主要用于**协调异步操作的加载状态**，让组件在等待异步数据（如网络请求、代码分割）时能够优雅地显示占位内容（loading 状态），而无需手动管理复杂的加载逻辑。

**核心作用：解决异步加载的 “状态碎片化” 问题**

在 `Suspense` 出现前，处理异步数据加载通常需要：

1. 定义 `loading` 状态（如 [`const [loading, setLoading] = useState(true)`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.true.md)）
2. 异步操作开始时设为 [`true`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.true.md)，结束后设为 [`false`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.false.md)
3. 在组件中通过条件判断显示加载态或内容（`{loading ? <Spinner /> : <Content />}`）

这种方式的问题在于：

* 加载状态与业务逻辑混杂，代码冗余
* 多个异步操作时，需要管理多个 `loading` 状态，容易出错
* 无法统一协调多个异步依赖的加载顺序

**`Suspense` 的工作方式**

`Suspense` 通过**声明式语法**，将 “等待异步资源” 与 “显示加载态” 分离，核心用法：

```jsx
// 用 Suspense 包裹可能需要等待异步资源的组件
<Suspense fallback={<Spinner />}>
  {/* 子组件加载异步资源时，会触发 Suspense 显示 fallback */}
  <AsyncComponent />
</Suspense>

```

* `fallback`：必填属性，指定异步资源加载完成前显示的占位内容（如加载动画）
* 当 `Suspense` 的子组件（或深层子组件）正在加载异步资源时，React 会暂停渲染，并显示 `fallback` 内容
* 异步资源加载完成后，自动替换为实际内容

**适用场景**

1. **代码分割（动态导入）**配合 `React.lazy` 实现组件的按需加载，是 `Suspense` 最成熟的应用场景：  
```jsx  
import { Suspense, lazy } from 'react';  
// 动态导入组件（返回 Promise）  
const LazyComponent = lazy(() => import('./LazyComponent'));  
function App() {  
  return (  
    <Suspense fallback={<div>Loading...</div>}>  
      <LazyComponent />  
    </Suspense>  
  );  
}  
```
2. **数据请求（React 18+ 实验性支持）**配合 `use` 钩子或数据获取库（如 React Query、SWR 的 Suspense 模式），直接在组件中声明式获取数据：  
```jsx  
// 数据获取函数（返回 Promise）  
async function fetchUser(id) {  
  const res = await fetch([`/api/users/${id}`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.users.md));  
  return res.json();  
}  
// 组件中直接使用，无需手动管理 loading  
function UserProfile({ id }) {  
  const user = fetchUser(id); // 触发 Suspense  
  return <div>{user.name}</div>;  
}  
// 上层用 Suspense 统一管理加载态  
function App() {  
  return (  
    <Suspense fallback={<Spinner />}>  
      <UserProfile id="123" />  
    </Suspense>  
  );  
}  
```

关键特性

* **向上查找**：如果子组件触发了 Suspense，React 会向上查找最近的 `Suspense` 组件并显示其 `fallback`
* **并发控制**：在 React 并发模式下，`Suspense` 可以暂停低优先级渲染，优先显示用户交互相关内容
* **批量处理**：多个异步依赖可以被同一个 `Suspense` 统一管理，只需一个 `fallback`

**`Suspense` 增强：支持数据加载与服务器渲染**

React 18 扩展了 `Suspense` 的能力，使其从 “仅支持代码分割” 升级为 “可协调任意异步操作”：

* **数据加载**：配合 `use` 钩子（React 18.3+）或数据库（如 React Query、SWR 的 Suspense 模式），`Suspense` 可直接等待数据请求完成，自动显示 `fallback` 加载态（无需手动管理 `loading` 状态）。
* **服务器组件（Server Components）**：在服务器渲染中，`Suspense` 可将页面拆分为 “优先渲染” 和 “延迟渲染” 的部分，先发送已准备好的内容到客户端，提升首屏加载速度。

```jsx
// React 18 中，Suspense 可直接等待数据加载
<Suspense fallback={<Spinner />}>
  <UserProfile userId={1} /> {/* 组件内部获取数据，触发 Suspense */}
</Suspense>

```

**总结**

`Suspense` 解决的核心问题是：**将异步加载的 “等待逻辑” 从组件中抽离，通过声明式方式统一管理加载状态**，让开发者更专注于业务逻辑，同时简化代码结构、提升可维护性。目前在代码分割场景中已稳定可用，在数据请求场景中仍在持续优化（React 18+ 提供更好的支持）。

### react中setState的执行机制和实现原理？

记忆点：**执行机制：批处理优先，行为因场景而异，核心原则批量处理优先**

**实现原理：主要依赖于更新队列” 和 “调度系统”，入队更新：创建更新对象并加入队列=>调度更新=>合并计算=>触发渲染：更新dom**

在 React 中，`setState` 是类组件更新状态的核心 API，其设计围绕 “高效更新” 和 “灵活控制” 展开。理解其执行机制和实现原理，需要从**行为表现**和**底层逻辑**两个层面拆解：

一、**执行机制：批处理为核心，行为因场景而异**

`setState` 的核心特性是 **“批处理更新”**，但具体行为会因调用场景和 React 版本而有所不同，并非简单的 “同步” 或 “异步”。

**1\. 核心原则：批处理（Batching）优先**

React 会将多个 `setState` 调用合并为一次更新，减少不必要的重渲染，这是性能优化的关键。

* **批处理生效场景**（表现为 “异步合并”）：  
   * React 合成事件回调（如 `onClick`、`onChange`）：React 会包裹事件处理逻辑，自动开启批处理。  
   * 生命周期函数（如 `componentDidMount`、`componentDidUpdate`）：在组件生命周期流程中，批处理默认开启。  
   * React 18+ 中的大部分场景（包括 `setTimeout`、`Promise.then` 等异步回调）：通过 “自动批处理” 统一生效。  
```jsx  
// 示例：批处理合并更新  
handleClick = () => {  
  this.setState({ count: 1 });  
  this.setState({ name: 'Bob' });  
  // 最终只触发一次重渲染，state 同时更新 count 和 name  
};  
```

**2\. 非批处理场景（表现为 “同步更新”）**

在少数场景下，批处理不会生效，`setState` 会立即更新状态并触发渲染：

* **React 17 及之前**：原生 DOM 事件（`addEventListener` 绑定）、`setTimeout`/`setInterval`、`Promise` 回调等 “非 React 控制的上下文”。
* **所有版本**：通过 `ReactDOM.flushSync` 强制同步更新（主动打破批处理）。  
```jsx  
// React 17 中，setTimeout 回调内批处理不生效  
componentDidMount() {  
  setTimeout(() => {  
    this.setState({ count: 1 });  
    console.log(this.state.count); // 输出 1（同步更新）  
  }, 0);  
}  
// 强制同步更新（所有版本）  
import { flushSync } from 'react-dom';  
flushSync(() => {  
  this.setState({ count: 1 });  
});  
console.log(this.state.count); // 输出 1（同步更新）  
```

**3\. 函数式更新：依赖前序状态的正确姿势**

当新状态依赖于上一次状态（如累加、切换）时，必须使用**函数形式**的 `setState`，否则可能因批处理合并导致计算错误。

```jsx
// 错误：依赖未更新的 state，多次调用可能只生效一次
this.setState({ count: this.state.count + 1 });
this.setState({ count: this.state.count + 1 }); // 实际只加 1

// 正确：函数形式接收前一次状态，确保计算准确
this.setState(prevState => ({ count: prevState.count + 1 }));
this.setState(prevState => ({ count: prevState.count + 1 })); // 最终加 2

```

**二、实现原理：四步完成状态更新**

`setState` 的底层逻辑依赖于 React 的 “更新队列” 和 “调度系统”，核心流程可分为四步：

**1\. 入队更新：创建更新对象并加入队列**

调用 `setState` 时，React 不会立即修改 `state`，而是创建一个**更新对象**（包含新状态、更新类型等信息），并将其加入当前组件的**更新队列**（`updateQueue`）。

* 每个组件实例维护一个独立的更新队列，确保状态更新按调用顺序处理。
* 多次调用 `setState` 会生成多个更新对象，依次入队等待处理。

**2\. 调度更新：由 Scheduler 决定处理时机**

React 的**调度器（Scheduler）** 会根据当前上下文判断何时处理更新队列：

* 若处于 “批处理模式”（如合成事件回调），调度器会延迟处理，等待当前事件循环中的所有 `setState` 调用完成后再统一处理。
* 若处于 “非批处理模式”（如 `setTimeout` 回调），调度器会立即触发处理（React 17 及之前）。
* React 18 后，调度器通过 “并发渲染” 架构，可中断、暂停或恢复更新，优先处理高优先级任务（如用户输入）。

**3\. 处理更新：合并更新并计算新状态**

调度器触发处理后，React 会遍历组件的更新队列，通过 “合并函数” 计算最终状态：

* 对于**对象形式**的 `setState({ ... })`：直接浅层合并（只合并顶层属性，嵌套对象需手动处理）。
* 对于**函数形式**的 `setState(prev => { ... })`：按顺序执行函数，将前一次计算结果作为下一次的输入，确保依赖正确。

**4\. 触发渲染：更新 DOM**

计算出新状态后，React 会触发组件的 “重渲染流程”：

1. 调用 `render` 方法生成新的虚拟 DOM（Virtual DOM）。
2. 通过 Diff 算法对比新旧虚拟 DOM，找出最小更新差异。
3. 将差异批量更新到真实 DOM（提交阶段），完成视图更新。

**三、关键结论**

1. `setState` 的核心是**批处理机制**，目的是减少重渲染次数，优化性能。
2. 行为表现（同步 / 异步）取决于是否处于 “React 控制的批处理上下文”，React 18 通过自动批处理统一了大多数场景的行为。
3. 依赖前序状态时必须使用**函数形式**，避免因批处理合并导致的计算错误。
4. 底层通过 “更新队列”+“调度器” 实现，兼顾性能与灵活性。

理解这些机制，能帮助开发者避开 “状态更新延迟”“计算错误” 等常见陷阱，写出更可靠的代码。

### setState是异步更新还是同步更新

**记忆点：取决于 调用场景 和 React 的批量更新机制。**

在 React 中，`setState` 的执行时机（异步或同步）取决于 **调用场景** 和 **React 的批量更新机制**。理解这一点对于避免常见的状态更新陷阱非常重要。

**一、核心结论**

1. **异步场景**（默认行为）：  
   * **合成事件**（React 事件系统中的事件，如 `onClick`、`onChange`）。  
   * **生命周期方法**（如 `componentDidMount`、`render`）。  
   * **批量更新**：多个 `setState` 会被合并为一次更新。
2. **同步场景**：  
   * **原生事件**（如 `addEventListener` 绑定的事件）。  
   * **定时器**（如 `setTimeout`、`setInterval`）。  
   * **Promise 回调**（如 `.then()`）。  
   * **手动调用 `ReactDOM.flushSync()`**。

**二、异步场景详解**

**1\. 合成事件中的异步行为**

```jsx
class Counter extends React.Component {
  state = { count: 0 };

  handleClick = () => {
    this.setState({ count: this.state.count + 1 });
    console.log(this.state.count); // 输出 0（异步更新，尚未生效）
  };

  render() {
    return <button onClick={this.handleClick}>{this.state.count}</button>;
  }
}

```

**原因**：React 会在事件处理函数执行完毕后 **批量更新状态**，以提升性能。

**2\. 生命周期方法中的异步行为**

```jsx
componentDidMount() {
  this.setState({ data: 'loaded' });
  console.log(this.state.data); // 输出 undefined（异步更新，尚未生效）
}

```

**三、同步场景详解**

**1\. 原生事件中的同步行为**

```jsx
componentDidMount() {
  document.getElementById('btn').addEventListener('click', () => {
    this.setState({ count: 1 });
    console.log(this.state.count); // 输出 1（同步更新）
  });
}

```

**原因**：原生事件不受 React 事件系统控制，状态更新会立即执行。

**2\. 定时器中的同步行为**

```jsx
setTimeout(() => {
  this.setState({ count: 1 });
  console.log(this.state.count); // 输出 1（同步更新）
}, 0);

```

**3\. Promise 回调中的同步行为**

```jsx
fetchData().then(() => {
  this.setState({ data: 'loaded' });
  console.log(this.state.data); // 输出 'loaded'（同步更新）
});

```

**四、批量更新机制**

React 会将 **同一事件循环内** 的多个 `setState` 合并为一次更新，以减少渲染次数：

```jsx
handleClick = () => {
  this.setState({ count: this.state.count + 1 }); // 第一次调用
  this.setState({ count: this.state.count + 1 }); // 第二次调用
  // 最终 count 只增加 1，而非 2！
};

```

**解决方案**：使用函数式 `setState` 确保每次更新基于最新状态：

```jsx
handleClick = () => {
  this.setState(prevState => ({ count: prevState.count + 1 })); // 第一次调用
  this.setState(prevState => ({ count: prevState.count + 1 })); // 第二次调用
  // 最终 count 增加 2
};

```

**五、强制同步更新（React 16+）**

使用 `ReactDOM.flushSync()` 强制同步执行状态更新：

```jsx
import ReactDOM from 'react-dom';

handleClick = () => {
  ReactDOM.flushSync(() => {
    this.setState({ count: this.state.count + 1 });
  });
  console.log(this.state.count); // 输出 1（同步更新）
};

```

**注意**：过度使用 `flushSync` 会影响性能，应谨慎使用。

**六、总结与最佳实践**

1. **默认假设 `setState` 是异步的**，避免依赖更新后的状态立即执行代码。
2. 使用回调函数获取最新状态  
```jsx  
this.setState({ count: 1 }, () => {  
  console.log(this.state.count); // 输出 1（回调在更新后执行）  
});  
```
3. 优先使用函数式 `setState`  
处理依赖前一个状态的更新：  
```jsx  
this.setState(prevState => ({ count: prevState.count + 1 }));  
```
4. **理解批量更新规则**：同一事件循环内的多个 `setState` 会被合并。

通过合理处理 `setState` 的异步特性，可以避免常见的状态管理陷阱，写出更可靠的 React 应用。

`setState` 的 “异步 / 同步” 差异，本质上是 React 在 **性能优化（批量更新）** 和 **场景可控性** 之间的权衡：

* 对于 React 可控的场景（合成事件、生命周期），通过异步批量更新减少 DOM 操作，提升性能；
* 对于 React 不可控的场景（原生事件、定时器等），通过同步更新保证状态与 DOM 的一致性，避免不可预期的行为。

理解这一点，就能从底层逻辑上解释为什么 `setState` 会有看似矛盾的行为 —— 它不是 “随机的异步或同步”，而是 React 为了兼顾性能和可靠性设计的合理机制。

在 React 中，子组件因`useEffect`导致重复渲染和重复请求，通常与依赖项处理、组件记忆化或数据缓存有关。以下是具体解决方法：

**1\. 优化`useEffect`的依赖项**

`useEffect`会在依赖项变化时重新执行。若依赖项是**每次渲染都会生成新引用的值**（如对象、数组、匿名函数），会导致不必要的重复执行。

**错误示例**

```jsx
// 子组件
function Child({ id }) {
  // 每次渲染都会创建新对象，导致useEffect重复执行
  const params = { id: id }; 

  useEffect(() => {
    fetchData(params); // 重复请求
  }, [params]); // 错误：params引用每次都变
}

```

**解决方法**：

* 依赖项使用原始值（而非对象 / 数组）
* 用`useMemo`记忆复杂依赖项

```jsx
function Child({ id }) {
  // 用useMemo记忆对象，确保引用稳定
  const params = useMemo(() => ({ id }), [id]); 

  useEffect(() => {
    fetchData(params); 
  }, [params]); // 仅当id变化时执行
}

```

1. **防止子组件不必要的重渲染**

父组件重渲染时，子组件可能被连带重渲染，导致`useEffect`重复触发。可通过以下方式优化：

**（1）用`React.memo`记忆子组件**

`React.memo`会浅比较 props，若 props 未变化则阻止子组件重渲染。

```jsx
// 用React.memo包装子组件
const Child = React.memo(({ id, fetchData }) => {
  useEffect(() => {
    fetchData(id);
  }, [id, fetchData]);

  return <div>...</div>;
});

```

**（2）用`useCallback`记忆父组件传递的函数**

父组件的函数若未被记忆，每次渲染会生成新引用，导致子组件的`fetchData` props 变化，触发重渲染。

```jsx
// 父组件
function Parent() {
  // 用useCallback记忆函数，确保引用稳定
  const fetchData = useCallback((id) => {
    // 请求逻辑
  }, []); // 依赖项为空，函数仅创建一次

  return <Child id={id} fetchData={fetchData} />;
}

```

**3\. 缓存请求结果，避免重复请求**

即使`useEffect`执行，也可通过缓存避免重复请求相同数据（如用`useState`\+ 条件判断，或专门的缓存库）。

**示例：本地缓存请求结果**

```jsx
function Child({ id }) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(false);

  useEffect(() => {
    // 若已有数据，直接返回（缓存生效）
    if (data?.id === id) return;

    const fetchData = async () => {
      setLoading(true);
      try {
        const res = await api.get([`/data/${id}`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.id.md));
        setData(res.data);
      } catch (err) {
        console.error(err);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [id, data]); // 依赖id和当前数据

  return <div>{data?.content}</div>;
}

```

**4\. 清理未完成的请求**

组件卸载或依赖项变化时，若前一次请求未完成，可能导致内存泄漏或错误。需在`useEffect`的清理函数中取消请求。

**示例：用 AbortController 取消请求**

```jsx
useEffect(() => {
  const controller = new AbortController(); // 创建控制器
  const signal = controller.signal;

  const fetchData = async () => {
    try {
      const res = await fetch([`/data/${id}`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.id.md), { signal }); // 关联信号
      const data = await res.json();
      setData(data);
    } catch (err) {
      if (err.name !== 'AbortError') { // 忽略主动取消的错误
        console.error(err);
      }
    }
  };

  fetchData();

  // 清理函数：取消未完成的请求
  return () => controller.abort();
}, [id]);

```

**总结**

解决步骤优先级：

1. 检查并优化`useEffect`的依赖项（核心原因）
2. 用`React.memo`+`useCallback`防止子组件无效重渲染
3. 缓存请求结果（减少重复请求）
4. 清理未完成的请求（避免副作用残留）

通过以上方法，可有效避免子组件因`useEffect`导致的重复渲染和请求问题。

### useState，每一次函数重新渲染的时候，useState怎么能够做到返回的状态是之前的状态呢？

在 React 中，`useState` 之所以能在函数组件重新渲染时返回 “之前的状态”，核心在于 **React 内部为每个组件实例维护了一份独立的 “状态存储”**，且通过 “调用顺序” 与 `useState` 建立了稳定的关联。

具体原理拆解：

1. **状态不存储在函数作用域中**

函数组件每次重新渲染时，函数体都会被重新执行。如果状态像普通变量一样存储在函数作用域中（例如 `let count = 0`），那么每次执行函数都会被重置为初始值。

但 `useState` 的状态 **存储在 React 内部为组件实例分配的 “内存空间” 中**（可以理解为一个与组件实例绑定的对象 / 链表），与函数的执行上下文无关。因此，无论函数渲染多少次，状态都会被 “持久化” 保存。

1. **通过 “调用顺序” 关联状态**

React 会为每个组件实例维护一个 **“Hooks 链表”**，链表中的每个节点对应一个 Hook（如 `useState`、`useEffect` 等）的信息（包括状态值、更新函数等）。

当组件第一次渲染时：

* 执行 `const [count, setCount] = useState(0)`，React 会在链表中创建一个新节点，存储初始状态 `0`，并返回 `[状态值, 更新函数]`。

当组件重新渲染时：

* React 会按照 **“Hooks 的调用顺序”** 遍历链表，找到对应 `useState` 节点中存储的 “最新状态”，并返回该状态。

这也是为什么 **Hooks 必须在函数组件顶层调用，不能放在条件 / 循环中**—— 如果调用顺序改变，React 会无法匹配到正确的状态节点，导致状态错乱。

1. **更新状态时的 “重新渲染触发”**

当调用 `setCount(newValue)` 时，React 会：

1. 更新该 `useState` 节点中存储的状态值（替换为 `newValue`）。
2. 标记组件需要重新渲染。
3. 组件重新执行时，`useState` 会从链表中读取更新后的状态值并返回。

**举个简化的类比：**

可以把组件实例想象成一个 “文件夹”，`useState` 的状态就是文件夹里的 “文件”。

* 第一次渲染：创建文件夹，新增一个文件（比如 `count.txt`），内容是初始值 `0`。
* 重新渲染：打开同一个文件夹，读取 `count.txt` 的最新内容（无论文件夹被打开多少次，文件内容都由上次保存的结果决定）。
* 调用 `setCount`：修改 `count.txt` 的内容，并通知 “系统” 重新打开文件夹查看。

**关键结论：**

`useState` 能在重新渲染时返回之前的状态，本质是因为：

1. 状态存储在 React 内部与组件实例绑定的独立空间中（而非函数作用域）。
2. 通过固定的调用顺序，`useState` 每次都能准确找到对应的状态节点。

这种设计既保证了函数组件的简洁性，又实现了状态的持久化管理。

### 什么是react插槽(Portals)？说明一下它的使用场景？

**记忆点：逻辑与DOM分离**

* **从 React 组件树的角度看，通过 Portals 渲染的内容仍然是当前组件的子元素，会正常参与组件的生命周期、事件冒泡等逻辑。**
* **从 DOM 结构的角度看，这部分内容会被插入到指定的目标 DOM 节点中，脱离原有的父组件 DOM 层级。**

**悬浮框，提示符，通知提示**

在 React 中，**Portals（ portals，直译为 “门户”）** 是一种特殊的渲染机制，允许你将组件的子元素**渲染到父组件的 DOM 层级结构之外的另一个 DOM 节点中**。简单来说，就是组件的逻辑上的父级仍然是 React 组件树中的父组件，但视觉上的渲染位置可以 “跳出” 原有的 DOM 层级，插入到页面的其他地方（如 [`body`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.body.md) 标签下）。

**一、Portals 的基本用法与原理**

Portals 通过 `ReactDOM.createPortal()` 方法实现，语法如下：

```jsx
import ReactDOM from 'react-dom';

function MyComponent() {
  // 第一个参数：要渲染的内容（React 元素、组件等）
  // 第二个参数：目标 DOM 节点（必须是真实的 DOM 元素）
  return ReactDOM.createPortal(
    <div>这是通过 Portals 渲染的内容</div>,
    document.getElementById('portal-container') // 目标容器
  );
}

```

**核心原理**：

* 从 React 组件树的角度看，通过 Portals 渲染的内容仍然是当前组件的子元素，会正常参与组件的生命周期、事件冒泡等逻辑。
* 从 DOM 结构的角度看，这部分内容会被插入到指定的目标 DOM 节点中，脱离原有的父组件 DOM 层级。

**二、Portals 的关键特性**

1. **逻辑与 DOM 分离**： 内容在 React 组件树中仍属于原组件的子节点（可访问父组件的 `props`、`state`），但 DOM 位置独立，解决了 “逻辑归属” 与 “视觉位置” 不一致的问题。
2. **事件冒泡正常生效**： 尽管内容渲染在其他 DOM 节点，但事件（如 `onClick`）会正常冒泡到 React 组件树中的父组件。例如：  
```jsx  
function Parent() {  
  const [show, setShow] = useState(false);  
  return (  
    <div onClick={() => setShow(false)}> {/* 点击父组件关闭弹窗 */}  
      <button onClick={() => setShow(true)}>打开弹窗</button>  
      {show && ReactDOM.createPortal(  
        <div className="modal">弹窗内容</div>,  
        document.body  
      )}  
    </div>  
  );  
}  
```  
点击弹窗内容时，事件会冒泡到 `Parent` 组件的外层 [`div`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.div.md)，触发关闭逻辑（符合 React 事件冒泡机制）。

**三、Portals 的典型使用场景**

Portals 主要用于解决 **“内容需要视觉上脱离父组件 DOM 层级”** 的场景，尤其是当父组件存在样式限制（如 `overflow: hidden`、`z-index` 层级低）时，避免内容被截断或遮挡。

**1\. 模态框（Modal）**

这是 Portals 最常见的场景。模态框通常需要覆盖整个页面，但如果父组件有 `overflow: hidden` 或固定高度，直接在父组件内渲染会导致模态框被截断。通过 Portals 将模态框渲染到 [`body`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.body.md) 下，可避免此问题：

```jsx
function Modal({ children, onClose }) {
  // 渲染到 body 下的独立容器，避免父组件样式影响
  return ReactDOM.createPortal(
    <div className="modal-overlay" onClick={onClose}>
      <div className="modal-content" onClick={e => e.stopPropagation()}>
        {children}
      </div>
    </div>,
    document.body
  );
}

```

**2\. 悬浮提示（Tooltip）或下拉菜单（Dropdown）**

当组件（如下拉菜单）需要显示在父组件外部（如超出父容器边界）时，父组件的 `overflow: hidden` 会导致内容被隐藏。使用 Portals 可将其渲染到 [`body`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.body.md) 下，确保完整显示：

```jsx
function Dropdown({ options }) {
  return ReactDOM.createPortal(
    <div className="dropdown">
      {options.map(option => (
        <div key={option.id}>{option.label}</div>
      ))}
    </div>,
    document.getElementById('dropdown-container')
  );
}

```

**3\. 通知提示（Notification/Toast）**

全局通知（如操作成功提示、错误警告）通常需要显示在页面顶层，且不依赖于某个具体父组件。通过 Portals 将通知容器固定在 [`body`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.body.md) 下，可实现全局显示：

```jsx
function Notification({ message }) {
  return ReactDOM.createPortal(
    <div className="notification">{message}</div>,
    document.getElementById('notification-container')
  );
}

```

**4\. 富文本编辑器或弹窗组件**

某些复杂组件（如富文本编辑器的弹窗工具栏、图片预览弹窗）需要突破编辑器容器的样式限制（如 `z-index` 较低、存在定位上下文），通过 Portals 可确保其显示在正确层级。

**四、使用 Portals 的注意事项**

1. **目标 DOM 节点需提前存在**： 确保 `ReactDOM.createPortal()` 的第二个参数（目标容器）在渲染时已存在于 DOM 中（可在 [`index.html`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.html.md) 中提前定义，如 [`<div id="portal-container"></div>`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.id.md)）。
2. **样式隔离**： 由于内容渲染在独立 DOM 节点，需注意样式冲突（可使用 CSS Modules 或命名空间避免）。
3. **事件冒泡需谨慎处理**： 虽然事件会正常冒泡，但如果不希望父组件响应事件（如点击模态框内容不触发背景关闭），需用 `e.stopPropagation()` 阻止冒泡。

**总结**

React Portals 是一种 “打破 DOM 层级限制” 的渲染机制，核心价值是**让组件的逻辑归属与视觉渲染位置分离**。其典型使用场景包括模态框、悬浮提示、全局通知等需要脱离父组件 DOM 层级的元素，解决了样式限制导致的内容截断、层级冲突等问题，同时保持了 React 组件模型的事件冒泡和生命周期特性。

### react 组件的更新机制是怎样的？

记忆点：

用于在**状态（`state`）或属性（`props`）变化时，高效更新 UI**。这一机制围绕 “最小化 DOM 操作” 和 “优化渲染性能” 设计，涉及**更新触发、任务调度、协调（Diff）、提交（DOM 更新）** 等多个阶段，并依赖 Fiber 架构实现可中断的高效更新。

React 组件的更新机制是其核心功能之一，用于在**状态（`state`）或属性（`props`）变化时，高效更新 UI**。这一机制围绕 “最小化 DOM 操作” 和 “优化渲染性能” 设计，涉及**更新触发、任务调度、协调（Diff）、提交（DOM 更新）** 等多个阶段，并依赖 Fiber 架构实现可中断的高效更新。

**一、更新的触发：什么会导致组件更新？**

组件更新的源头是**状态或属性的变化**，具体触发场景包括：

1. **状态变化（`state`）**：  
   * 类组件调用 `this.setState()` 或 `this.forceUpdate()`；  
   * 函数组件调用 `useState` 的更新函数（如 `setCount`）或 `useReducer` 的 `dispatch` 函数。 状态变化会直接触发组件重新渲染。
2. **属性变化（`props`）**：  
   * 父组件更新后，子组件接收的 `props` 发生变化，会触发子组件重新渲染（除非被优化手段阻止）。
3. **上下文（Context）变化**：  
   * 若组件通过 `useContext` 或 `Context.Consumer` 消费上下文，当上下文 `value` 变化时，组件会重新渲染。
4. **强制更新**：  
   * 类组件调用 `this.forceUpdate()`，或函数组件中使用 `useImperativeHandle` 等强制触发更新（跳过状态检查）。

**二、更新的核心流程：从触发到 DOM 更新**

React 组件的更新过程可分为 **4 个核心阶段**，依赖 Fiber 架构实现高效调度和中断恢复：

**阶段 1：更新入队与调度（Scheduling）**

状态或属性变化后，React 不会立即执行更新，而是先将更新任务**加入队列**，并由 **Scheduler（调度器）** 决定何时执行。

* **批处理（Batching）**：React 会将多个连续的更新（如同一事件回调中多次调用 `setState`）合并为一次更新，减少渲染次数。例如：  
```jsx  
// 类组件  
handleClick() {  
  this.setState({ count: 1 });  
  this.setState({ count: 2 }); // 两次更新会合并，最终 count 为 2  
}  
// 函数组件  
const handleClick = () => {  
  setCount(c => c + 1);  
  setCount(c => c + 1); // 合并为一次更新，count 最终 +2  
};  
```  
（React 18 后，批处理在更多场景下生效，包括异步操作如 `setTimeout` 中。）
* **优先级排序**：Scheduler 根据任务优先级（如用户输入 > 动画 > 普通更新）决定执行顺序，高优先级任务（如点击、滚动）可中断低优先级任务（如列表渲染），避免卡顿。

**阶段 2：协调（Reconciliation）—— 计算差异（可中断）**

协调阶段是 React 计算 “需要更新哪些部分” 的核心阶段，依赖 **Fiber 架构** 和 **Diff 算法**，且**可被高优先级任务中断**。

1. **构建新 Fiber 树**： 从根组件开始，基于新的 `state`/`props` 重新生成组件的虚拟 DOM（通过 `render` 方法或函数组件执行），并映射为新的 Fiber 树（Fiber 是工作单元的载体）。
2. **Diff 算法对比新旧 Fiber 树**： React 通过 Diff 算法对比新旧 Fiber 树，计算最小差异：  
   * 同层节点仅对比同层级（不跨层级），降低复杂度；  
   * 节点类型不同则直接替换子树；  
   * 节点类型相同则对比 `props` 和子节点，标记差异类型（如 “更新”“新增”“删除”）。
3. **标记副作用（Effect Tag）**： 对需要更新的节点标记副作用（如 `Update`、`Placement`、`Deletion`），并收集到 “Effect List” 中，供后续提交阶段使用。

**阶段 3：提交（Commit）—— 执行 DOM 更新（不可中断）**

协调阶段完成后，React 进入提交阶段，**根据 Effect List 执行实际的 DOM 操作**，此阶段不可中断（避免 DOM 状态不一致）。

1. **执行前置副作用（`before mutation`）**： 调用 `getSnapshotBeforeUpdate`（类组件）等生命周期钩子，获取更新前的 DOM 状态。
2. **执行 DOM 操作**： 根据 Effect List 中的标记，执行具体的 DOM 操作：  
   * 新增节点（`Placement`）：将新节点插入 DOM；  
   * 更新节点（`Update`）：更新 DOM 属性或内容（如 `className`、`textContent`）；  
   * 删除节点（`Deletion`）：移除旧节点，解绑事件。
3. **执行后置副作用（`layout`）**：  
   * 调用类组件生命周期钩子（`componentDidMount`、`componentDidUpdate`）；  
   * 调用函数组件的 `useEffect` 清理函数（上一次渲染的副作用）和回调函数；  
   * 更新 `ref` 引用，使其指向最新的 DOM 节点。

**阶段 4：清理与收尾**

提交阶段后，React 会清理临时变量（如旧 Fiber 树），并通知 Scheduler 调度下一个等待的任务。

**三、更新优化：避免不必要的重渲染**

默认情况下，父组件更新会触发所有子组件重新渲染，即使子组件 `props` 未变化。React 提供了多种优化手段减少无效更新：

1. **`React.memo`（函数组件）**： 对函数组件进行记忆化处理，仅当 `props` 真正变化时才重新渲染（浅比较 `props`）。  
```jsx  
const MemoizedChild = React.memo(ChildComponent);  
// 仅当 ChildComponent 的 props 浅比较不同时，才会重新渲染  
```
2. **`shouldComponentUpdate`（类组件）**： 类组件可重写此方法，通过自定义逻辑判断是否需要更新（返回 [`false`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.false.md) 则跳过更新）。  
```jsx  
class ChildComponent extends React.Component {  
  shouldComponentUpdate(nextProps) {  
    // 仅当 props.id 变化时才更新  
    return nextProps.id !== this.props.id;  
  }  
}  
```
3. **`useMemo` 与 `useCallback`（函数组件）**：  
   * `useMemo` 记忆化计算结果，避免每次渲染重复计算；  
   * `useCallback` 记忆化函数引用，避免因函数重新创建导致子组件 `props` 变化。  
```jsx  
const Child = React.memo(({ onClick }) => <button onClick={onClick} />);  
const Parent = () => {  
  // 记忆化 onClick 函数，避免每次渲染创建新函数  
  const handleClick = useCallback(() => {}, []);  
  return <Child onClick={handleClick} />;  
};  
```
4. **拆分组件与状态下沉**： 将不相关的状态拆分到独立组件中，避免状态变化导致大面积重渲染。

**四、函数组件与类组件更新的差异**

虽然核心流程一致，但函数组件和类组件的更新在细节上存在差异：

* **状态存储**：类组件的状态存储在实例的 `this.state` 中；函数组件的状态通过 Hooks 存储在 Fiber 节点的链表中（依赖调用顺序）。
* **更新触发**：类组件依赖 `setState` 合并状态；函数组件的 `useState` 更新函数是独立的，不会合并状态（需通过函数式更新 `setX(x => x + 1)` 依赖前值）。
* **生命周期**：类组件通过生命周期钩子控制更新逻辑；函数组件通过 `useEffect`、`useLayoutEffect` 等 Hooks 处理副作用。

**总结**

React 组件的更新机制是一个 “**触发→调度→协调→提交**” 的完整流程，核心特点包括：

1. **批处理与优先级调度**：合并更新、优先处理高优先级任务，提升性能；
2. **Fiber 架构支持中断**：协调阶段可被中断，避免主线程阻塞；
3. **Diff 算法精准更新**：最小化 DOM 操作，只更新变化的部分；
4. **丰富的优化手段**：通过 `React.memo`、`useMemo` 等减少无效重渲染。

这一机制既保证了 UI 与状态的一致性，又通过多种优化策略确保了复杂应用的流畅性。

### react的Immutable的原理是什么？

记忆点：

**问题，解决状态难以追踪，导致无效的重渲染或漏渲染，“数据一旦创建就不可修改，任何修改都会返回一个新的数据源”。**

**核心：不可变性，结构共享性。**

在 React 中，**Immutable（不可变数据）** 并非 React 内置的功能，而是一种**数据管理思想**，其核心是 “数据一旦创建就不可修改，任何修改都会返回一个新的数据源”。这种思想在 React 中被广泛应用于状态（`state`）和属性（`props`）的管理，目的是**提高状态对比的效率**、**减少不必要的重渲染**，并让状态变化更可预测。

**一、为什么需要 Immutable？**

JavaScript 中的对象和数组默认是**可变的（Mutable）**：当你修改一个对象的属性或数组的元素时，会直接改变原对象（因为对象 / 数组是引用类型，变量存储的是内存地址）。这种特性在 React 中会带来问题：

1. **状态变化难以追踪**：直接修改原状态后，无法通过引用对比判断数据是否变化（原引用没变，但内容变了）。
2. **导致无效重渲染或漏渲染**：React 依赖 “引用对比” 判断是否需要更新组件（如 `React.memo`、`shouldComponentUpdate`）。若原对象被修改但引用不变，React 会认为数据没变化，导致漏渲染；若频繁创建新对象（即使内容没变），则会触发无效重渲染。

**二、Immutable 的核心原理**

Immutable 的核心是 **“不可变性”和“结构共享”**：

**1\. 不可变性：修改数据时返回新对象，原对象保持不变**

对于 Immutable 数据，任何修改操作（如添加、删除、更新属性）都不会改变原对象，而是返回一个**全新的对象**。原对象始终保持创建时的状态，这确保了数据的 “可追溯性”。

**示例（原生 JavaScript 模拟 Immutable）**：

```javascript
// 原对象（Immutable）
const original = { name: "React", version: 18 };

// 修改时返回新对象，原对象不变
const updated = { ...original, version: 19 };

console.log(original.version); // 18（原对象未变）
console.log(updated.version);  // 19（新对象）
console.log(original === updated); // false（引用不同，便于判断变化）

```

**2\. 结构共享：只复制变化的部分，复用未变化的部分**

对于嵌套结构（如 [`{ a: { b: { c: 1 } }, d: 2 }`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.a.md)），如果每次修改都完整复制整个对象，会产生巨大的性能和内存开销。Immutable 通过 **“结构共享”** 优化：

* 只复制被修改的属性及其所在的 “路径”；
* 未被修改的属性复用原对象的引用，不重复占用内存。

**示例（嵌套对象的结构共享）**：

```javascript
// 原对象（嵌套结构）
const original = {
  user: { name: "Alice", age: 20 },
  settings: { theme: "light" }
};

// 修改 user.age，返回新对象（结构共享）
const updated = {
  ...original, // 复用原对象的引用（但实际是新对象）
  user: {      // user 被修改，创建新对象
    ...original.user, // 复用 user 中未变的属性（name）
    age: 21           // 只修改 age
  }
};

// 未修改的部分复用原引用
console.log(original.settings === updated.settings); // true（共享引用）
// 修改的部分是新引用
console.log(original.user === updated.user); // false（新对象）
console.log(original === updated); // false（新对象）

```

通过结构共享，既保证了不可变性，又避免了全量复制的性能损耗。

**三、Immutable 在 React 中的应用价值**

React 的更新机制严重依赖 “数据是否变化” 的判断，而 Immutable 数据通过 **“引用对比”** 就能高效判断变化，无需深比较，从而优化性能：

**1\. 优化 `shouldComponentUpdate`（类组件）**

类组件中，`shouldComponentUpdate` 通过对比 `nextProps` 和 `this.props`、`nextState` 和 `this.state` 决定是否重渲染。若使用 Immutable 数据，只需浅比较引用即可：

```javascript
class MyComponent extends React.Component {
  shouldComponentUpdate(nextProps, nextState) {
    // 浅比较：若引用不同，说明数据变化，需要重渲染
    return nextProps.data !== this.props.data || nextState.count !== this.state.count;
  }
}

```

如果数据是可变的（如直接修改原对象），[`nextProps.data`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.data.md) 与 [`this.props.data`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.data.md) 引用相同，即使内容变化，`shouldComponentUpdate` 也会返回 [`false`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.false.md)，导致漏渲染。

**2\. 优化 `React.memo`（函数组件）**

`React.memo` 对函数组件进行记忆化，默认浅比较 `props`。若 `props` 是 Immutable 数据，引用变化即代表内容变化，能精准触发重渲染：

```javascript
// 记忆化组件：仅当 props.data 引用变化时才重渲染
const MemoizedComponent = React.memo(({ data }) => {
  return <div>{data.name}</div>;
});

// 使用时：修改 data 会返回新引用，触发更新
const Parent = () => {
  const [data, setData] = useState({ name: "React" });
  
  const handleClick = () => {
    // 正确：返回新对象（Immutable 思想）
    setData(prev => ({ ...prev, name: "React 18" }));
  };
  
  return <MemoizedComponent data={data} />;
};

```

**3\. 让状态变化可预测，便于调试**

Immutable 数据的 “不可修改” 特性确保了：

* 任何时间点的状态都是 “快照”，不会被后续操作篡改；
* 配合 Redux 等状态管理库时，可实现 “时间旅行”（回溯历史状态），便于调试。

**四、实现 Immutable 的工具库**

手动实现 Immutable 数据（尤其是嵌套结构）容易出错且繁琐，实际开发中常用工具库：

1. **Immer**：最常用的库，通过 “draft 模式” 允许 “看似修改” 数据，实际自动生成 Immutable 新对象，语法简洁：  
```javascript  
import { produce } from "immer";  
const original = { count: 1 };  
// "修改" draft，实际生成新对象  
const updated = produce(original, draft => {  
  draft.count += 1; // 看似直接修改，实际操作的是临时草稿  
});  
console.log(original.count); // 1（原对象不变）  
console.log(updated.count);  // 2（新对象）  
```
2. **Immutable.js**：提供完整的 Immutable 数据结构（如 `Map`、`List`），但语法较特殊，需要学习新 API。
3. **原生扩展**：ES6+ 的扩展运算符（`...`）、`Object.assign`、数组方法（[`map`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.map.md)、`filter` 等，返回新数组）可实现简单的 Immutable 操作，但嵌套结构需要手动处理。

**总结**

React 中 Immutable 的核心原理是：**数据一旦创建就不可修改，修改时通过 “结构共享” 返回新对象，仅复制变化部分，复用未变化部分**。这种思想解决了 JavaScript 引用类型的 “可变” 特性带来的状态追踪难题，让 React 能通过高效的 “引用对比” 判断数据变化，减少无效重渲染，同时使状态变化更可预测、更易于调试。

在实际开发中，结合 Immer 等工具库，可轻松实现 Immutable 数据管理，显著提升 React 应用的性能和可维护性。

### 如何获取setState的最新值

**记忆点：使用函数式更新，避免直接使用this.state**

在 React 中，`setState` 的异步特性是为了优化性能（例如批量更新），但这可能导致难以立即获取最新状态值。以下是确保获取最新状态值的几种方法：

1. **使用函数式更新（最可靠方式）**

当新状态依赖于旧状态时，使用 **函数式更新** 确保每次更新都基于最新状态：

```javascript
// 错误方式：可能使用旧的 this.state.count
this.setState({ count: this.state.count + 1 });

// 正确方式：使用函数式更新，参数 prevState 是最新状态
this.setState(prevState => ({
  count: prevState.count + 1
}));

```

**原理**：React 会将所有函数式更新放入队列，按顺序执行，确保每个更新都基于上一次的结果。

1. **在回调函数中获取最新值**

`setState` 的第二个参数是回调函数，会在状态更新完成后执行

```javascript
this.setState(
  { count: this.state.count + 1 },
  () => {
    console.log('最新值:', this.state.count); // 此时状态已更新
  }
);

```

1. **在 `componentDidUpdate` 中处理更新后逻辑**

组件更新完成后，`componentDidUpdate` 会被调用，此时 `this.state` 是最新值：

```javascript
componentDidUpdate(prevProps, prevState) {
  if (prevState.count !== this.state.count) {
    console.log('状态已更新为:', this.state.count);
  }
}

```

1. **使用 `useState` 的函数式更新（Hooks 方式）**

在函数组件中，使用 `useState` 的函数式更新和 `useEffect` 监听变化：

```javascript
const [count, setCount] = useState(0);

// 函数式更新，确保基于最新值
const increment = () => {
  setCount(prevCount => prevCount + 1);
};

// 监听状态变化，更新后执行
useEffect(() => {
  console.log('最新 count:', count);
}, [count]);

```

1. **避免直接依赖 `this.state`**

不要在 `setState` 前后直接读取 `this.state`，而是通过上述方法间接获取最新值。例如：

```javascript
// 错误：可能读取到旧值
this.setState({ count: this.state.count + 1 });
console.log(this.state.count); // 可能不是最新值

// 正确：使用回调或函数式更新
this.setState(prev => ({ count: prev.count + 1 }));

```

为什么需要这些方法？

React 可能会将多次 `setState` 合并为一次更新（例如在同一个事件处理函数中），以提高性能。如果直接依赖 `this.state`，可能会使用到未更新的值。而 **函数式更新** 和 **回调函数** 是 React 提供的明确获取最新状态的方式。

总结

* **函数式更新**：适用于新状态依赖旧状态的场景（如计数、数组操作）。
* **回调函数**：适用于需要立即使用最新状态的场景（如更新 DOM）。
* **生命周期 / 副作用**：适用于在状态更新后执行额外逻辑（如网络请求）。

通过这些方法，可以确保在 React 中可靠地处理状态更新。

### React中组件之间如何通信

在 React 中，组件通信的方式取决于组件之间的关系（父子、兄弟、跨层级、无关联等），不同场景需要选择不同的方案。以下是常见的组件通信方式及适用场景：

**一、父子组件通信：最基础的通信方式**

父子组件是最直接的关系，通信通过 **`props`** 和 **回调函数** 实现，是 React 中最常用的通信模式。

**1\. 父组件 → 子组件：通过 `props` 传递数据**

父组件将数据作为 `props` 传递给子组件，子组件通过 `props` 接收并使用。**示例**：

```jsx
// 父组件
function Parent() {
  const parentData = "来自父组件的数据";
  return <Child message={parentData} />; // 通过 props 传递
}

// 子组件
function Child(props) {
  return <div>子组件接收：{props.message}</div>; // 通过 props 接收
}

```

`props` 可以传递任意类型数据（基本类型、对象、函数、组件等），且是**单向只读**的（子组件不能直接修改 `props`，需通过父组件更新）。

**2\. 子组件 → 父组件：通过回调函数传递数据**

父组件将一个回调函数作为 `props` 传给子组件，子组件调用该函数并传入数据，实现向父组件 “发送消息”。**示例**：

```jsx
// 父组件
function Parent() {
  const [childData, setChildData] = useState("");

  // 定义回调函数，接收子组件的数据
  const handleChildMsg = (data) => {
    setChildData(data);
  };

  return (
    <div>
      <Child onSendMsg={handleChildMsg} />
      <p>父组件接收：{childData}</p>
    </div>
  );
}

// 子组件
function Child(props) {
  const sendData = () => {
    // 调用父组件传入的回调函数，传递数据
    props.onSendMsg("来自子组件的数据");
  };
  return <button onClick={sendData}>发送给父组件</button>;
}

```

**二、兄弟组件通信：通过父组件中转**

兄弟组件（同一父组件的子组件）之间无法直接通信，需以**父组件为中间层**：

1. 子组件 A 将数据通过回调传给父组件；
2. 父组件将数据通过 `props` 传给子组件 B。

**示例**：

```jsx
// 父组件（中间层）
function Parent() {
  const [sharedData, setSharedData] = useState("");

  return (
    <div>
      <BrotherA onUpdate={setSharedData} /> {/* A 传数据给父组件 */}
      <BrotherB data={sharedData} /> {/* 父组件传数据给 B */}
    </div>
  );
}

// 兄弟组件 A
function BrotherA(props) {
  const handleClick = () => {
    props.onUpdate("A 发送的数据"); // 传给父组件
  };
  return <button onClick={handleClick}>A 发送</button>;
}

// 兄弟组件 B
function BrotherB(props) {
  return <div>B 接收：{props.data}</div>; // 从父组件接收
}

```

**三、跨层级组件通信：Context API**

当组件层级较深（如祖父→孙子→曾孙），通过 `props` 一层层传递（“props drilling”）会非常繁琐。此时可使用 **Context API** 创建全局上下文，让所有后代组件直接访问数据。

**Context 通信流程：**

1. **创建 Context**：使用 `createContext` 创建上下文对象；
2. **提供数据**：通过 `Context.Provider` 包裹组件树，用 `value` 传递数据；
3. **消费数据**：后代组件通过 `useContext` 钩子或 `Context.Consumer` 读取数据。

**示例**：

```jsx
// 1. 创建 Context（可单独抽离为文件）
import { createContext, useContext, useState } from "react";

const MyContext = createContext(); // 创建上下文

// 2. 提供数据（祖先组件）
function Grandparent() {
  const [globalData, setGlobalData] = useState("全局数据");

  return (
    // Provider 包裹子树，value 传递数据（可包含更新函数）
    <MyContext.Provider value={{ globalData, setGlobalData }}>
      <Parent />
    </MyContext.Provider>
  );
}

// 中间组件（无需传递 props）
function Parent() {
  return <Child />;
}

// 3. 消费数据（深层子组件）
function Child() {
  // 通过 useContext 直接获取上下文数据
  const { globalData, setGlobalData } = useContext(MyContext);

  return (
    <div>
      <p>子组件获取：{globalData}</p>
      <button onClick={() => setGlobalData("更新后的全局数据")}>
        更新数据
      </button>
    </div>
  );
}

```

**适用场景**：中小型应用的跨层级通信（避免过度使用，否则会导致组件耦合度升高）。

**四、无关联组件通信：全局状态管理**

对于完全无关联的组件（如不同路由页面、不同模块的组件），需使用**全局状态管理工具**，将状态抽离到全局 store 中，所有组件均可访问和修改。

**常用方案：**

1. **Redux / Redux Toolkit**： 最流行的全局状态管理库，通过 `store` 存储全局状态，组件通过 `dispatch` 发送 `action` 修改状态，通过 `useSelector` 读取状态。**核心流程**：  
   * 定义 `reducer`（处理状态更新的纯函数）；  
   * 创建 `store`（集中管理状态）；  
   * 用 `Provider` 包裹应用，让所有组件访问 `store`；  
   * 组件通过 `useSelector` 获取状态，`useDispatch` 发送 `action`。
2. **MobX**： 基于 “响应式编程” 的状态管理库，通过 `observable` 定义状态，`action` 修改状态，组件通过 `observer` 监听状态变化。
3. **React 18 + useReducer + Context**： 轻量级方案，用 `useReducer` 管理复杂状态逻辑，配合 Context 实现全局访问（适合中小型应用，避免引入第三方库）。

**Redux 示例（简化）**：

```jsx
// 1. 定义 reducer 和初始状态
const initialState = { count: 0 };
function counterReducer(state = initialState, action) {
  switch (action.type) {
    case "INCREMENT": return { ...state, count: state.count + 1 };
    default: return state;
  }
}

// 2. 创建 store
import { configureStore } from "@reduxjs/toolkit";
const store = configureStore({ reducer: counterReducer });

// 3. 用 Provider 包裹应用
import { Provider } from "react-redux";
function App() {
  return (
    <Provider store={store}>
      <ComponentA />
      <ComponentB />
    </Provider>
  );
}

// 4. 组件 A 读取状态
import { useSelector } from "react-redux";
function ComponentA() {
  const count = useSelector((state) => state.count);
  return <div>Count: {count}</div>;
}

// 5. 组件 B 修改状态
import { useDispatch } from "react-redux";
function ComponentB() {
  const dispatch = useDispatch();
  return <button onClick={() => dispatch({ type: "INCREMENT" })}>加 1</button>;
}

```

**五、其他通信方式**

1. **事件总线（Event Bus）**： 基于发布 - 订阅模式（如使用 `mitt` 库），组件通过 “发布事件” 和 “订阅事件” 通信，适合简单场景。  
```jsx  
import mitt from "mitt";  
const emitter = mitt(); // 创建事件总线  
// 组件 A 发布事件  
function ComponentA() {  
  return <button onClick={() => emitter.emit("msg", "Hello")}>发送</button>;  
}  
// 组件 B 订阅事件  
function ComponentB() {  
  useEffect(() => {  
    const handleMsg = (data) => console.log("接收：", data);  
    emitter.on("msg", handleMsg); // 订阅  
    return () => emitter.off("msg", handleMsg); // 取消订阅  
  }, []);  
  return null;  
}  
```
2. **Ref 通信**： 父组件通过 `ref` 直接访问子组件的实例或 DOM 元素，适合获取子组件的状态 / 方法（但会破坏组件封装，谨慎使用）。  
```jsx  
function Parent() {  
  const childRef = useRef(null);  
  return (  
    <div>  
      <Child ref={childRef} />  
      <button onClick={() => childRef.current.log()}>调用子组件方法</button>  
    </div>  
  );  
}  
// 子组件需用 forwardRef 暴露 ref  
const Child = forwardRef((props, ref) => {  
  const log = () => console.log("子组件方法");  
  useImperativeHandle(ref, () => ({ log })); // 暴露指定方法  
  return <div>子组件</div>;  
});  
```

**总结：如何选择通信方式？**

| 组件关系    | 推荐方式                | 适用场景           |
| ------- | ------------------- | -------------- |
| 父子组件    | props + 回调函数        | 直接的父子关系，数据单向流动 |
| 兄弟组件    | 父组件中转               | 同一父组件下的简单通信    |
| 跨层级组件   | Context API         | 中小型应用的深层级通信    |
| 无关联组件   | Redux / MobX / 全局状态 | 大型应用的全局数据共享    |
| 简单非关联组件 | 事件总线（mitt）          | 小型应用，临时通信需求    |

核心原则：**尽量使用简单的方式解决问题**，避免过度设计（如小应用不必引入 Redux，用 Context 即可）。

### **react核心实现原理**

记忆点：

React 的核心实现原理围绕 “高效更新 UI” 展开，通过**声明式编程模型**、**虚拟 DOM（Virtual DOM）**、**Fiber 架构**、**协调算法（Reconciliation）** 等机制，解决了传统 DOM 操作效率低、状态管理复杂的问题。其核心目标是：在保证开发体验（简洁的声明式 API）的同时，最小化真实 DOM 操作（因为 DOM 操作是前端性能瓶颈之一）。

1. 通过**虚拟 DOM** 减少真实 DOM 操作，用 JS 计算替代高成本 DOM 操作；
2. 基于**Fiber 架构**实现可中断的渲染流程，配合优先级调度保证页面响应性；
3. 用**高效的 Diff 算法**计算虚拟 DOM 差异，最小化更新成本；
4. 通过**状态驱动**和**声明式 API**，简化 UI 开发逻辑，同时支持批量更新、并发更新等优化。

React 的核心实现原理围绕 “高效更新 UI” 展开，通过**声明式编程模型**、**虚拟 DOM（Virtual DOM）**、**Fiber 架构**、**协调算法（Reconciliation）** 等机制，解决了传统 DOM 操作效率低、状态管理复杂的问题。其核心目标是：在保证开发体验（简洁的声明式 API）的同时，最小化真实 DOM 操作（因为 DOM 操作是前端性能瓶颈之一）。

**一、核心设计理念：声明式编程与组件化**

React 的核心思想是 **“声明式描述 UI”**，开发者只需关注 “UI 应该是什么样子”（基于当前状态），而非 “如何一步步更新 UI”（命令式）。这种模式依赖两大基础：

1. **组件化**：UI 被拆分为独立、可复用的组件（如 [`function Component()`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.function.md) 或 `class Component`），每个组件封装了自身的状态（`state`）和渲染逻辑（`render`）。
2. **状态驱动**：组件的 UI 由其内部状态（`state`）或外部传入的属性（`props`）决定，状态变化时，React 自动重新渲染组件。

**二、虚拟 DOM（Virtual DOM）：减少真实 DOM 操作**

真实 DOM 操作（如创建、修改、删除节点）是性能密集型操作（涉及浏览器重排、重绘）。React 引入**虚拟 DOM** 作为中间层，优化这一过程。

**1\. 什么是虚拟 DOM？**

虚拟 DOM 是**用 JavaScript 对象描述真实 DOM 结构的轻量级副本**。例如，一个真实的 [`<div class="box">Hello</div>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.div.md) 对应的虚拟 DOM 可能是：

```javascript
{
  type: 'div',        // 标签类型
  props: { className: 'box' },  // 属性
  children: 'Hello'   // 子节点
}

```

组件的 `render()` 方法（或函数组件的返回值）本质上就是生成这样的虚拟 DOM 对象。

1. **虚拟 DOM 的工作流程**

当组件状态变化时，React 会经历以下步骤：

1. **生成新虚拟 DOM**：基于新状态重新执行 `render`，生成新的虚拟 DOM 树。
2. **对比新旧虚拟 DOM**：通过 “Diff 算法” 计算新旧虚拟 DOM 的差异（哪些节点需要新增、修改或删除）。
3. **更新真实 DOM**：只将计算出的 “最小差异” 应用到真实 DOM 上（而非重新渲染整个 DOM 树）。

这一过程的核心优势是：**用 JavaScript 计算（低成本）替代大量真实 DOM 操作（高成本）**，从而提升性能。

**三、Fiber 架构：解决渲染阻塞问题**

React 16 引入 **Fiber 架构**，解决了大型应用中 “长时间渲染导致页面卡顿” 的问题。其核心是将渲染工作**分解为可中断、可恢复的小单元**，并支持优先级调度。

**1\. 为什么需要 Fiber？**

在 Fiber 之前，React 的渲染过程是 “同步且不可中断的”：一旦开始渲染（从根组件到叶子组件递归对比虚拟 DOM），会占用主线程直到完成。如果组件层级很深（如 1000 层），这一过程可能耗时 100ms 以上，导致页面无法响应用户输入（如点击、滚动），产生卡顿。

**2\. Fiber 的核心设计**

* **Fiber 节点**：将虚拟 DOM 节点扩展为 “Fiber 节点”，每个节点对应一个工作单元，存储：  
   * 组件类型、属性、子节点等信息；  
   * 工作状态（是否已完成、依赖的优先级等）；  
   * 指针（用于连接成链表，支持中断后恢复）。
* **工作循环（Work Loop）**：渲染过程被分为两个阶段，支持中断和恢复：  
   1. **协调阶段（Reconciliation）**：  
         * 遍历 Fiber 树，对比新旧节点，标记需要更新的节点（如 “新增”“删除”“修改”）；  
         * 此阶段的工作可被中断（如更高优先级的任务到来，如用户输入），中断后可从上次中断的节点继续。  
   2. **提交阶段（Commit）**：  
         * 执行真实 DOM 操作（根据协调阶段的标记更新 DOM）；  
         * 调用生命周期钩子（如 `componentDidMount`、`useEffect`）；  
         * 此阶段不可中断（避免 DOM 处于不一致状态）。

**3\. 优先级调度**

Fiber 配合 **Scheduler（调度器）** 实现任务优先级：

* 高优先级任务（如用户输入、动画）可中断低优先级任务（如列表渲染）；
* 空闲时再继续低优先级任务，保证页面响应性。

**四、协调算法（Reconciliation）：高效计算 DOM 差异**

协调算法（又称 “Diff 算法”）是虚拟 DOM 对比的核心，目标是**以最小成本找出新旧虚拟 DOM 树的差异**。React 的 Diff 算法基于两个假设（实际开发中需遵循，否则可能影响性能）：

1. **同层节点类型不同，则直接替换**：不跨层级对比节点（如一个 [`div`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.div.md) 的子节点不会与 [`span`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.span.md) 的子节点对比）。
2. **同层节点类型相同，则通过 `key` 标识唯一性**：用于列表节点的复用（避免错误复用导致的状态混乱）。

**1\. 树级对比（层级差异）**

React 只对比**同一层级**的节点：

* 若父节点类型不同（如 [`div`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.div.md) 变为 [`span`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.span.md)），则直接删除旧节点及其所有子节点，创建新节点。
* 若父节点类型相同，则继续对比其子女节点。

这一策略将 Diff 复杂度从 O (n³)（全量对比）降低到 O (n)（线性对比）。

**2\. 列表节点对比（`key` 的作用）**

对于列表节点（如 [`[<li />, <li />]`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.li.md)），若没有 `key` 或 `key` 不稳定（如用索引 `index` 作为 `key`），React 可能错误复用节点，导致状态异常

**示例**：

```jsx
// 旧列表（无 key 或 key 为 index）
[<li>1</li>, <li>2</li>]

// 新列表（在头部插入元素）
[<li>0</li>, <li>1</li>, <li>2</li>]

```

若无稳定 `key`，React 会认为 “1 变成 0，2 变成 1，新增 2”，导致所有节点被修改；而有稳定 `key` 时，React 能正确识别 “新增 0，1 和 2 未变”，仅新增一个节点。

**3\. 组件级对比**

若两个组件的类型相同（如都是 `User` 组件），则复用组件实例，仅对比其 `props` 差异；若类型不同，则直接卸载旧组件，挂载新组件。

**五、状态更新机制：从 `setState` 到并发更新**

React 的状态更新是触发重新渲染的核心，其机制在不断优化（从同步更新到并发更新）。

**1\. 状态更新的基本流程**

* 调用 `setState`（类组件）或 `setXxx`（Hooks，如 `useState` 的更新函数）时，React 会将状态更新加入队列。
* 触发 “调度”：Scheduler 决定何时执行更新（根据优先级）。
* 进入协调阶段：重新计算虚拟 DOM 差异。
* 进入提交阶段：更新真实 DOM 并执行副作用。

**2\. 批量更新（Batching）**

React 会将多个连续的状态更新 “合并” 为一次渲染，减少不必要的 DOM 操作。例如：

```javascript
// 类组件
this.setState({ count: this.state.count + 1 });
this.setState({ count: this.state.count + 1 }); 
// 最终 count 只 +1（合并为一次更新）

// Hooks
const [count, setCount] = useState(0);
setCount(c => c + 1);
setCount(c => c + 1); 
// 最终 count 只 +1（合并）

```

**3\. 并发更新（React 18+）**

React 18 引入 “并发更新”，允许**同一时间存在多个版本的 UI 渲染**（但只提交最终版本）。例如，在输入框打字时，高优先级的输入更新可以中断低优先级的列表渲染，避免输入卡顿。

**六、Hooks 原理：函数组件的状态管理**

React 16.8 引入的 Hooks（如 `useState`、`useEffect`），让函数组件拥有了状态和副作用能力，其实现依赖**链表存储**和**调用顺序**。

* **Hooks 存储**：每个函数组件对应一个 `Hook` 链表，`useState`、`useEffect` 等 Hooks 按调用顺序依次存入链表。
* **依赖数组**：`useEffect(fn, [dep])` 中的依赖数组用于判断副作用是否需要重新执行（对比前后依赖是否变化）。
* **规则限制**：Hooks 必须在函数组件顶层调用（不能在条件 / 循环中），否则会破坏链表的调用顺序，导致状态错乱。

**总结**

React 的核心实现原理可概括为：

1. 通过**虚拟 DOM** 减少真实 DOM 操作，用 JS 计算替代高成本 DOM 操作；
2. 基于**Fiber 架构**实现可中断的渲染流程，配合优先级调度保证页面响应性；
3. 用**高效的 Diff 算法**计算虚拟 DOM 差异，最小化更新成本；
4. 通过**状态驱动**和**声明式 API**，简化 UI 开发逻辑，同时支持批量更新、并发更新等优化。

这些机制共同让 React 既能提供简洁的开发体验，又能在复杂应用中保持高性能。

### React的事件机制

记忆点：

本质是通过 “将所有组件的事件处理函数统一委托给顶层容器节点”，利用 DOM 事件冒泡特性实现高效的事件管理。这种机制既减少了事件绑定的内存消耗，又简化了跨浏览器兼容处理，同时适配 React 组件化模型。

实现原理：核心依赖两个关键设计：**统一的委托目标**和**事件映射表**。

当用户触发一个事件（如点击按钮）时，React 事件委托机制的完整处理流程可分为 5 步，涉及**原生事件冒泡**和**React 事件分发**两个阶段：

**阶段 1：原生 DOM 事件冒泡**

**阶段 2：React 事件分发与处理**

1.顶层委托节点捕获事件，捕获之后react做事件的分发

2.**查找对应处理函数**

3.**创建合成事件并执行处理函数**

**关键细节：委托机制的特殊处理**

**1\. 如何关联 DOM 元素与组件的事件处理函数？**

唯一性：将 “标识 + 事件类型 + 处理函数” 存入事件映射表

2.**事件冒泡的 “两层独立性”**

**3\. 不支持冒泡的事件如何处理？**

对于原生不支持冒泡的事件（如 `focus`、`blur`），React 会采用**事件捕获**（而非冒泡）机制实现委托

React 事件系统的**事件委托机制**是其核心设计之一，本质是通过 “将所有组件的事件处理函数统一委托给顶层容器节点”，利用 DOM 事件冒泡特性实现高效的事件管理。这种机制既减少了事件绑定的内存消耗，又简化了跨浏览器兼容处理，同时适配 React 组件化模型。以下从**实现原理、完整流程、核心细节、版本变化**四个维度详细解析：

**一、核心设计：为什么需要事件委托？**

传统原生 DOM 事件处理中，开发者通常会为每个元素单独绑定事件（如 [`button.addEventListener('click', handler)`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.button.md)）。这种方式在 React 组件化场景下存在明显缺陷：

* **性能问题**：一个页面可能有上千个组件（如列表项），每个组件绑定事件会导致大量内存占用，且频繁的绑定 / 解绑（如组件挂载 / 卸载）会引发性能损耗。
* **跨浏览器兼容**：不同浏览器的事件模型存在差异（如 IE 的 `attachEvent` 与标准 `addEventListener`），单独处理成本高。
* **组件动态性**：React 组件会频繁更新（如列表项增删），动态元素的事件绑定需要手动维护，容易遗漏或重复绑定。

React 的事件委托机制正是为解决这些问题而生：**将所有事件处理函数统一委托到一个顶层节点，利用事件冒泡特性，在顶层统一接收和分发事件**。

**二、实现原理：委托目标与事件映射表**

React 事件委托的核心依赖两个关键设计：**统一的委托目标**和**事件映射表**。

**1\. 统一的委托目标（Delegation Target）**

React 会将所有事件的处理逻辑**委托到一个顶层容器节点**，而非在每个组件对应的 DOM 元素上直接绑定。这个委托目标在不同 React 版本中有所变化：

* **React 16 及之前**：委托目标是 `document`（整个页面的根节点）。
* **React 17 及之后**：委托目标改为 React 应用的**挂载容器节点**（如 [`div#root`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.div.md)，即 `ReactDOM.render(<App />, root)` 中的 `root`）。

**为什么 React 17 要修改委托目标？**

* 避免与其他框架（如 jQuery）在 `document` 上的事件处理冲突（其他框架可能也会在 `document` 绑定事件，导致事件顺序混乱）。
* 支持同一页面中嵌入多个独立的 React 应用（每个应用的事件委托在自己的容器内，互不干扰）。

**2\. 事件映射表（Event Registry）**

React 内部维护了一个**事件映射表**（可理解为一个键值对集合），用于记录 “DOM 元素 / 组件” 与 “事件处理函数” 的对应关系。当事件触发时，React 通过这个映射表找到对应的处理函数并执行。

映射表的核心信息包括：

* 事件类型（如 `click`、`change`）；
* 对应的 DOM 元素（或组件实例）；
* 开发者定义的事件处理函数（如 `onClick` 回调）。

**三、完整流程：从事件触发到处理函数执行**

当用户触发一个事件（如点击按钮）时，React 事件委托机制的完整处理流程可分为 5 步，涉及**原生事件冒泡**和**React 事件分发**两个阶段：

**阶段 1：原生 DOM 事件冒泡**

1. **用户触发事件**：如点击 [`<button>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.button.md) 元素，浏览器生成原生事件对象（如 `MouseEvent`），并从触发元素（[`button`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.button.md)）开始向上冒泡。
2. **事件沿 DOM 树向上传播**：按照原生 DOM 规则，事件依次经过父元素、祖父元素…… 最终到达 React 的委托目标（如 `#root` 或 `document`）。

**阶段 2：React 事件分发与处理**

1. **顶层委托节点捕获事件**：委托目标上的原生事件监听器（由 React 内部提前注册）捕获到冒泡上来的原生事件，将其传递给 React 的**事件分发器（Event Dispatcher）**。
2. **查找对应处理函数**： 事件分发器根据以下信息在 “事件映射表” 中查找匹配的处理函数：  
   * 原生事件的类型（如 `'click'`）；  
   * 事件的原始触发元素（`event.target`，即被点击的 [`button`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.button.md)）。 （注：React 会通过 DOM 元素与组件的对应关系，找到该元素所属的组件及绑定的事件处理函数，如 `onClick` 回调。）
3. **创建合成事件并执行处理函数**：  
   * React 创建**合成事件对象（SyntheticEvent）**，封装原生事件的属性和方法（如 `target`、`stopPropagation`），并统一跨浏览器差异。  
   * 将合成事件作为参数，调用找到的事件处理函数（如开发者定义的 `handleClick`）。  
   * 处理函数执行完成后，合成事件对象在 React 17 前会被回收复用（事件池机制），React 17 后则直接销毁。

**四、关键细节：委托机制的特殊处理**

**1\. 如何关联 DOM 元素与组件的事件处理函数？**

当 React 渲染组件时（如执行 `render` 生成 DOM），会为每个绑定了事件（如 `onClick`）的 DOM 元素添加一个**唯一标识**（内部属性），并将 “标识 + 事件类型 + 处理函数” 存入事件映射表。当事件触发时，通过 `event.target` 的唯一标识即可在映射表中找到对应的处理函数。

**2\. 事件冒泡的 “两层独立性”**

React 合成事件的 “冒泡” 与原生 DOM 事件的 “冒泡” 是**两个独立的流程**：

* **原生冒泡**：从触发元素到委托目标（如 [`button → ... → #root`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.button.md)），是浏览器原生行为。
* **合成事件冒泡**：在 React 事件系统内部模拟的冒泡（如从子组件到父组件），通过 `e.stopPropagation()` 可阻止。

**注意**：

* 调用合成事件的 `e.stopPropagation()` 只能阻止合成事件的冒泡（如子组件的 `onClick` 阻止父组件的 `onClick`），但无法阻止原生事件继续向浏览器顶层（如 `window`）冒泡。
* 若在原生事件中调用 `e.stopPropagation()`，会阻止事件到达 React 委托目标，导致 React 事件处理函数**无法触发**。

**3\. 不支持冒泡的事件如何处理？**

对于原生不支持冒泡的事件（如 `focus`、`blur`），React 会采用**事件捕获**（而非冒泡）机制实现委托，确保这些事件也能被顶层节点捕获并处理。

**五、优势总结**

React 事件委托机制的核心价值体现在：

1. **性能优化**：只需在顶层节点绑定少量事件监听器，替代大量元素的单独绑定，减少内存消耗和 DOM 操作。
2. **简化管理**：动态新增 / 删除组件时，无需手动绑定 / 解绑事件（映射表会自动更新）。
3. **跨浏览器兼容**：通过合成事件屏蔽浏览器差异，开发者无需关注 `addEventListener` 与 `attachEvent` 等兼容问题。
4. **适配组件模型**：事件处理函数自动绑定组件实例（如 `this` 指向组件），符合 React 组件化开发习惯。

**总结**

React 事件委托机制的本质是：**以顶层容器为统一委托目标，利用 DOM 事件冒泡特性，通过事件映射表关联 DOM 元素与组件事件处理函数，最终实现高效、兼容、易维护的事件管理**。这一机制是 React 事件系统高性能和易用性的核心保障，也是理解 React 事件行为（如冒泡、跨组件通信）的基础。

### React Router 中hash与history得区别

在 React Router 中，`hash` 和 `history` 是两种不同的路由模式，核心区别体现在 URL 表现形式、底层实现原理、兼容性及服务器配置等方面。以下是具体对比：

**1\. URL 表现形式**

* **hash 模式**： URL 中会包含 `#`（哈希符），哈希后面的部分作为路由标识。 例如：[`http://example.com/#/home`](http://example.com/#/home)、[`http://example.com/#/user/123`](http://example.com/#/user/123)。`#` 及其后面的内容不会被发送到服务器，仅作为浏览器端的路由标识。
* **history 模式**： URL 中没有 `#`，路由看起来像普通的 URL 路径。 例如：[`http://example.com/home`](http://example.com/home)、[`http://example.com/user/123`](http://example.com/user/123)。 这种模式的 URL 更符合用户对 “正常网址” 的认知。

**2\. 底层实现原理**

* **hash 模式**： 基于浏览器的 `hashchange` 事件实现。当 URL 中 `#` 后面的内容变化时，浏览器会触发 `hashchange` 事件，React Router 监听该事件并更新路由视图，**不会导致页面重新加载**。 原理：`#` 是浏览器的原生特性，用于定位页面内锚点，其变化不会触发 HTTP 请求。
* **history 模式**： 基于 HTML5 的 `History API`（`history.pushState()`、`history.replaceState()`）实现。这些 API 允许在不刷新页面的情况下修改浏览器的历史记录和 URL，React Router 通过调用这些方法更新路由，并监听 `popstate` 事件（如用户点击前进 / 后退按钮）来同步视图。 原理：通过 API 手动修改 URL 和历史记录，本质上是对浏览器历史栈的操作。

**3\. 兼容性**

* **hash 模式**： 兼容性更好，支持所有现代浏览器及旧版本浏览器（如 IE9 及以下），因为 `#` 是浏览器的原生特性，无需依赖高级 API。
* **history 模式**： 依赖 HTML5 的 `History API`，因此兼容性稍差，不支持 IE9 及以下版本浏览器（这些浏览器没有实现 `pushState` 等方法）。

**4\. 服务器配置要求**

* **hash 模式**： 无需特殊配置服务器。因为 `#` 后面的内容不会被发送到服务器，无论用户访问 [`http://example.com/#/home`](http://example.com/#/home) 还是 [`http://example.com/#/user`](http://example.com/#/user)，服务器只会接收到 [`http://example.com`](http://example.com) 的请求，只需返回单页应用的入口 HTML 文件（如 [`index.html`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.html.md)）即可。
* **history 模式**：**需要服务器额外配置**。因为当用户直接访问 [`http://example.com/home`](http://example.com/home) 或刷新页面时，浏览器会向服务器发送 `GET /home` 的请求，若服务器没有配置对应路由，会返回 404 错误。 解决方式：服务器需将所有路由请求（如 `/home`、`/user/*` 等）都指向单页应用的入口 HTML 文件（[`index.html`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.html.md)），让前端路由接管页面渲染。 例如：Nginx 配置需添加 [`try_files $uri $uri/ /index.html;`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.html.md)。

**5\. 其他注意事项**

* **SEO 友好性**： 两者对 SEO 都有一定限制（单页应用的通病），但 history 模式的 URL 更 “正常”，搜索引擎可能更易识别（需配合服务端渲染 SSR 进一步优化）。
* **路由参数传递**： 两者都支持通过路由参数（如 [`/user/:id`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.id.md)）传递数据，用法在 React Router 中一致，区别仅在于 URL 表现形式。
* **哈希值的局限性**： hash 模式中，`#` 后面的内容会被浏览器视为 “片段标识符”，可能与页面内的锚点（如 [`<a href="#top">`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.a.md)）冲突。

**如何选择？**

* 若需要兼容旧浏览器（如 IE9），或不想配置服务器，选 **hash 模式**。
* 若追求更美观的 URL、更好的用户体验，且能控制服务器配置，选 **history 模式**（推荐现代应用使用）。

在 React Router 中，两种模式的使用方式也很简单：

* hash 模式：通过 `HashRouter` 组件启用。
* history 模式：通过 `BrowserRouter` 组件启用（默认模式）。

例如：

```jsx
// hash 模式
import { HashRouter, Routes, Route } from 'react-router-dom';

function App() {
  return (
    <HashRouter>
      <Routes>
        <Route path="/home" element={<Home />} />
      </Routes>
    </HashRouter>
  );
}

// history 模式（默认）
import { BrowserRouter, Routes, Route } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/home" element={<Home />} />
      </Routes>
    </BrowserRouter>
  );
}

```

### 为什么let a = 1,修改a =2react不会重新渲染，需要通过useState触发重新渲染呢？

**记忆点：React 只认自己 “管理的状态”，不认普通变量，心区别在于是否被 React 纳入 “可追踪的状态系统”**

在 React 中，组件的重新渲染机制与 “状态追踪” 密切相关。let 声明的普通变量和 useState 创建的状态，核心区别在于**是否被 React 纳入 “可追踪的状态系统”**，这直接决定了变量修改后是否会触发组件重新渲染。

**1\. 普通变量（let a = 1）为什么不触发重新渲染？**

用 [`let a = 1`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.a.md) 声明的变量，本质上是**JavaScript 环境中的普通变量**，它的变化完全在 React 的 “感知范围之外”。

React 组件的渲染逻辑是：**只有当组件的 “依赖项”（props 或 state）发生变化时，才会触发重新渲染**。而普通变量的修改：

* 不会被 React 记录到 “依赖追踪系统” 中；
* 变量值变化后，React 完全不知情，自然不会触发组件的重新渲染；
* 即使变量值变了，组件的 UI 也不会更新（因为组件不会重新执行渲染逻辑）。

例如：

```jsx
function App() {
  let a = 1; // 普通变量

  const handleClick = () => {
    a = 2; // 修改变量，但 React 不知道
    console.log(a); // 控制台会输出 2，但 UI 不会变
  };

  return (
    <div>
      <p>{a}</p> {/* 始终显示 1，因为组件没重新渲染 */}
      <button onClick={handleClick}>修改 a</button>
    </div>
  );
}

```

点击按钮后，[`a`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.a.md) 的值确实变成了 2，但组件没有重新渲染，所以页面上显示的还是初始值 1。

**2\. useState 为什么能触发重新渲染？**

`useState` 是 React 提供的**状态管理钩子**，它的核心作用是将变量 “纳入 React 的状态系统”，让 React 能够追踪其变化。

当使用 `useState` 时：

* React 会在组件内部创建一个 “状态容器”，存储该状态的当前值；
* 当通过  
```txt  
setXxx  
```  
（状态更新函数）修改状态时，React 会：  
   1. 更新 “状态容器” 中的值；  
   2. 主动触发组件的重新渲染（调度一次更新）；  
   3. 重新执行组件函数时，`useState` 会返回最新的状态值，从而更新 UI。

例如：

```jsx
import { useState } from 'react';

function App() {
  const [a, setA] = useState(1); // 被 React 追踪的状态

  const handleClick = () => {
    setA(2); // 通知 React：状态变了，请重新渲染
  };

  return (
    <div>
      <p>{a}</p> {/* 点击后会显示 2，因为组件重新渲染了 */}
      <button onClick={handleClick}>修改 a</button>
    </div>
  );
}

```

点击按钮后，`setA(2)` 会告诉 React 状态已更新，React 会重新执行 `App` 组件，此时 `useState` 返回最新的 [`a = 2`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.a.md)，UI 随之更新。

**核心原因：React 的 “响应式设计”**

React 并非自动追踪所有变量的变化（这会导致性能灾难），而是通过 `useState`、`useReducer` 等 API 明确标记 “需要追踪的状态”。只有这些被标记的状态发生变化时，React 才会触发重新渲染，这是一种 “精确控制” 的设计。

普通变量的修改属于 “外部变化”，React 无法感知；而 `useState` 的更新函数会主动通知 React 状态变化，从而启动重新渲染流程。

简单说：**React 只认自己 “管理的状态”，不认普通变量**

### Diff算法的实现

用于计算新旧虚拟dom树的最小差异

核心思想一致：**通过优化对比策略降低复杂度，快速定位需要更新的节点**。

记忆点：

Diff 算法的核心是**通过 “同层对比、类型优先、key 标识” 三大策略，将树形结构对比复杂度从 O (n³) 降至 O (n)**

实现步骤：

**1\. 树级对比：快速排除跨层级差异**

**2\. 组件级对比：复用相同类型组件**

**3\. 列表节点对比：通过 key 复用节点（核心难点）**

Diff 算法是虚拟 DOM 机制的核心，用于计算**新旧虚拟 DOM 树的最小差异**，最终只将这些差异应用到真实 DOM，从而减少不必要的 DOM 操作。不同框架（如 React、Vue）的 Diff 实现略有差异，但核心思想一致：**通过优化对比策略降低复杂度，快速定位需要更新的节点**。

**一、Diff 算法的核心优化策略**

传统的树形结构全量对比（如递归对比所有节点）时间复杂度为 **O(n³)**（n 为节点数），难以满足前端高频更新需求。前端框架的 Diff 算法通过以下策略将复杂度优化至 **O(n)**（线性复杂度）：

1. **同层对比**：只对比同一层级的节点，不跨层级比较（如不将父节点与子节点对比）。若父节点类型不同，直接判定 “整个子树需要替换”，无需深入子节点对比。
2. **类型优先**：若两个节点类型不同（如 [`div`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.div.md) 与 [`span`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.span.md)），直接判定 “旧节点需删除，新节点需创建”，不再对比子节点。
3. **列表 key 标识**：对于列表节点（如 [`[<li/>, <li/>]`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.li.md)），通过 `key` 标识节点唯一性，快速定位可复用节点，避免错误复用导致的状态异常。

**二、React Diff 算法的实现步骤**

以 React 为例，Diff 算法的核心流程分为**树级对比**、**组件级对比**、**列表节点对比**三个层次，逐步缩小差异范围。

**1\. 树级对比：快速排除跨层级差异**

树级对比是 Diff 的第一层检查，目标是快速判断 “是否需要全量替换子树”：

* 遍历新旧虚拟 DOM 树的同一层级节点（如根节点的子节点、子节点的子节点等）。
* 若当前层级的节点数量、类型差异较大（如旧节点是 [`div`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.div.md)，新节点是 [`span`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.span.md)），则直接标记 “删除旧节点及其所有子节点，创建新节点及其子节点”，终止该分支的深层对比。

**示例**：

```javascript
// 旧虚拟 DOM
{ type: 'div', children: [{ type: 'p', children: '旧内容' }] }

// 新虚拟 DOM
{ type: 'span', children: [{ type: 'p', children: '新内容' }] }

```

树级对比发现根节点类型从 [`div`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.div.md) 变为 [`span`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.span.md)，直接判定 “删除旧 [`div`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.div.md) 子树，创建新 [`span`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.span.md) 子树”，无需对比子节点 [`p`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.p.md)。

**2\. 组件级对比：复用相同类型组件**

当节点类型相同时（如都是 [`div`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.div.md) 标签或都是 `User` 组件），进入组件级对比：

* **原生标签（如 [`div`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.div.md)、[`p`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.p.md)）**： 对比节点属性（`props`）的差异（如 `className`、[`style`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.style.md)、`onClick` 等），标记 “需要更新的属性”（无需重新创建节点，只需更新属性）。
* **自定义组件（如 `User`）**： 复用组件实例（避免重新初始化），仅对比 `props` 差异。若 `props` 相同，则组件不重新渲染；若 `props` 不同，触发组件的 `render` 方法生成新的子虚拟 DOM，继续递归对比。

**示例**：

```javascript
// 旧虚拟 DOM（自定义组件）
{ type: User, props: { name: '旧名' }, children: [] }

// 新虚拟 DOM（自定义组件）
{ type: User, props: { name: '新名' }, children: [] }

```

组件类型相同，对比 `props` 发现 `name` 变化，触发 `User` 组件重新渲染，继续对比其内部子节点。

**3\. 列表节点对比：通过 key 复用节点（核心难点）**

列表节点（如 [`ul`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.ul.md) 的 [`li`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.li.md) 子节点）是 Diff 中最复杂的场景，因为列表可能频繁增删、排序，需要高效定位可复用节点。React 通过 `key` 实现这一目标。

**（1）无 key 或 key 不稳定（如 index）的问题**

若列表节点无 `key` 或使用索引 `index` 作为 `key`，当列表变化时（如头部插入元素），React 会错误地复用节点，导致状态混乱。

**示例**：

```jsx
// 旧列表（key 为 index）
[<li key={0}>A</li>, <li key={1}>B</li>]

// 新列表（头部插入 C）
[<li key={0}>C</li>, <li key={1}>A</li>, <li key={2}>B</li>]

```

React 会认为 “key=0 的节点从 A 变为 C”“key=1 的节点从 B 变为 A”，导致所有节点被重新渲染（而非仅新增 C）。

**（2）key 为唯一标识时的对比逻辑**

当 `key` 是稳定的唯一标识（如数据 ID）时，React 通过以下步骤对比列表：

1. **构建旧节点 key 映射表**：将旧列表节点按 `key` 存储为 `{ key: 节点 }` 的映射（如 `{ 'a1': 节点A, 'b2': 节点B }`），便于快速查找。
2. 遍历新列表节点  
：  
   * 对每个新节点，用其 `key` 在旧映射表中查找对应的旧节点。  
   * 若找到（`key` 匹配且类型相同）：复用旧节点，对比并更新属性 / 子节点，记录节点位置变化（如需移动）。  
   * 若未找到：标记 “需要创建新节点”。
3. **清理未复用的旧节点**：遍历旧映射表，标记所有未被新列表复用的节点为 “需要删除”。

**（3）列表 Diff 的优化：减少移动操作**

为进一步减少节点移动次数，React 会通过 “双指针法” 定位节点的最小移动范围：

* 用两个指针（`oldStart`、`oldEnd` 指向旧列表首尾，`newStart`、`newEnd` 指向新列表首尾）。
* 优先对比首尾节点（如旧首 vs 新首、旧尾 vs 新尾），若匹配则直接复用，指针向中间移动；
* 若首尾不匹配，再用 `key` 映射表查找，找到后移动节点，否则创建新节点。

这种策略能在多数场景下（如列表尾部新增 / 删除）避免全量遍历，进一步提升效率。

**三、简化版 Diff 算法实现代码**

以下是模拟 React Diff 核心逻辑的简化代码，展示如何对比两个虚拟 DOM 节点并生成差异：

```javascript
// 虚拟 DOM 节点结构（简化）
// { type, key, props, children }

/**
 * 对比新旧虚拟 DOM 节点，返回差异对象
 * @param {*} oldVNode 旧虚拟 DOM
 * @param {*} newVNode 新虚拟 DOM
 * @returns 差异对象 { type: 'REPLACE' | 'UPDATE' | 'MOVE' | 'REMOVE' | 'ADD', ... }
 */
function diff(oldVNode, newVNode) {
  // 1. 新节点不存在：标记删除旧节点
  if (!newVNode) {
    return { type: 'REMOVE', vnode: oldVNode };
  }

  // 2. 旧节点不存在：标记新增新节点
  if (!oldVNode) {
    return { type: 'ADD', vnode: newVNode };
  }

  // 3. 节点类型不同（如 div  vs span，或不同组件）：标记替换
  if (oldVNode.type !== newVNode.type) {
    return { type: 'REPLACE', oldVNode, newVNode };
  }

  // 4. 节点类型相同且是文本节点：对比内容
  if (typeof oldVNode === 'string' && typeof newVNode === 'string') {
    if (oldVNode !== newVNode) {
      return { type: 'UPDATE', content: newVNode };
    }
    return null; // 无差异
  }

  // 5. 节点类型相同且是元素/组件：对比 props 和 children
  const diffResult = { type: 'UPDATE', props: {}, children: [] };
  let hasDiff = false;

  // 5.1 对比 props 差异
  const allProps = { ...oldVNode.props, ...newVNode.props };
  Object.keys(allProps).forEach(key => {
    const oldVal = oldVNode.props[key];
    const newVal = newVNode.props[key];
    if (oldVal !== newVal) {
      diffResult.props[key] = newVal;
      hasDiff = true;
    }
  });

  // 5.2 对比子节点（列表 Diff）
  const oldChildren = oldVNode.children || [];
  const newChildren = newVNode.children || [];
  const oldKeyMap = createKeyMap(oldChildren); // 构建旧子节点 key 映射

  // 遍历新子节点，查找可复用旧节点
  newChildren.forEach((newChild, newIndex) => {
    const key = newChild.key;
    if (key) {
      const oldChild = oldKeyMap[key];
      if (oldChild) {
        // 递归对比子节点差异
        const childDiff = diff(oldChild, newChild);
        if (childDiff) {
          diffResult.children.push({
            index: newIndex,
            diff: childDiff,
            key: key
          });
          hasDiff = true;
        }
        delete oldKeyMap[key]; // 标记为已复用
      } else {
        // 新节点，无对应旧节点：新增
        diffResult.children.push({
          index: newIndex,
          diff: { type: 'ADD', vnode: newChild },
          key: key
        });
        hasDiff = true;
      }
    } else {
      // 无 key：简单对比同位置节点（不推荐，仅作示例）
      const oldChild = oldChildren[newIndex];
      const childDiff = diff(oldChild, newChild);
      if (childDiff) {
        diffResult.children.push({ index: newIndex, diff: childDiff });
        hasDiff = true;
      }
    }
  });

  // 剩余未复用的旧节点：标记删除
  Object.values(oldKeyMap).forEach(oldChild => {
    diffResult.children.push({
      diff: { type: 'REMOVE', vnode: oldChild }
    });
    hasDiff = true;
  });

  return hasDiff ? diffResult : null;
}

// 辅助函数：创建旧子节点的 key 映射表
function createKeyMap(children) {
  const map = {};
  children.forEach(child => {
    if (child.key) {
      map[child.key] = child;
    }
  });
  return map;
}

```

**四、Diff 算法的意义与局限**

* **意义**：通过高效对比定位最小差异，将 DOM 操作从 “全量更新” 变为 “精准更新”，大幅减少重排 / 重绘，是虚拟 DOM 性能优势的核心保障。
* 局限：  
   1. 额外的 JavaScript 计算开销（但通常远小于 DOM 操作开销）；  
   2. 列表 `key` 设计不当（如用 index）会导致 Diff 效率下降甚至状态异常；  
   3. 极端场景（如完全逆序的列表）仍可能产生较多移动操作（部分框架通过 “最长递增子序列” 算法进一步优化）。

**总结**

Diff 算法的核心是**通过 “同层对比、类型优先、key 标识” 三大策略，将树形结构对比复杂度从 O (n³) 降至 O (n)**，高效计算新旧虚拟 DOM 的差异。其中，列表节点的 `key` 处理是实现难点，合理使用稳定唯一的 `key` 是保证 Diff 效率和正确性的关键。理解 Diff 算法有助于优化组件渲染性能（如避免不必要的节点类型变化、合理设计 `key` 等）。

### 虚拟dom

虚拟 DOM（Virtual DOM）是前端框架（如 React、Vue）中用于优化 DOM 操作的核心技术，本质是**用 JavaScript 对象描述真实 DOM 结构的轻量级副本**。它通过减少直接操作真实 DOM 的次数（因为 DOM 操作是前端性能瓶颈之一），大幅提升页面渲染效率。

**一、为什么需要虚拟 DOM？**

真实 DOM 是浏览器渲染引擎管理的节点，包含大量属性和方法（如 `parentNode`、[`style`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.style.md)、`getBoundingClientRect` 等），操作真实 DOM 会触发浏览器的**重排（Reflow）** 和**重绘（Repaint）**，性能开销极大。

例如，直接修改一个列表中 1000 个元素的文本，会触发 1000 次真实 DOM 操作和多次重排；而通过虚拟 DOM，可先在 JavaScript 中计算所有修改，再一次性更新真实 DOM，仅触发少数几次重排。

**二、虚拟 DOM 的本质：JavaScript 对象**

虚拟 DOM 是对真实 DOM 的**结构化描述**，用简单的 JavaScript 对象表示节点的类型、属性、子节点等信息。

**示例**： 一个真实的 DOM 节点：

```html
<div class="container" id="app">
  <p>Hello</p>
  <button onclick="handleClick()">Click me</button>
</div>

```

对应的虚拟 DOM 对象（简化版）：

```javascript
{
  type: 'div',                // 节点类型（标签名或组件名）
  props: {                    // 节点属性
    className: 'container',   // 对应 class（避免与 JS 关键字冲突）
    id: 'app'
  },
  children: [                 // 子节点列表（同样是虚拟 DOM 对象）
    { type: 'p', props: {}, children: 'Hello' },
    { 
      type: 'button', 
      props: { onClick: handleClick }, 
      children: 'Click me' 
    }
  ]
}

```

在 React 中，组件的 `render()` 方法（或函数组件的返回值）本质上就是生成这样的虚拟 DOM 对象（React 中称为 `ReactElement`）。

**三、虚拟 DOM 的工作流程**

当组件状态（如 `state`、`props`）变化时，虚拟 DOM 的工作流程可分为 **“生成新树→对比差异→更新真实 DOM”** 三步：

**1\. 生成新虚拟 DOM 树（Render 阶段）**

状态变化时，组件会重新执行渲染逻辑（如 React 的 `render` 或函数组件的重新调用），生成**新的虚拟 DOM 树**。

这一步是纯 JavaScript 计算，不涉及任何 DOM 操作，性能开销极低。

**2\. 对比新旧虚拟 DOM 树（Diff 阶段）**

通过**Diff 算法**（又称 “协调算法”）对比新旧虚拟 DOM 树，计算出两者的**最小差异**（哪些节点需要新增、修改、删除）。

Diff 算法是虚拟 DOM 性能的核心，前端框架会通过优化策略降低对比复杂度：

* **同层对比**：只对比同一层级的节点（不跨层级比较），将复杂度从 O (n³)（全量对比）降至 O (n)（线性对比）。
* **key 优化**：列表节点通过 `key` 标识唯一性，避免错误复用节点（如列表增删时，用 `key` 快速定位变化的节点）。
* **类型判断**：若节点类型（如 [`div`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.div.md) 与 [`span`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.span.md)）不同，直接判定为 “需替换”，不再深入对比子节点。

**3\. 应用差异到真实 DOM（Patch 阶段）**

将 Diff 阶段计算出的 “差异” 批量应用到真实 DOM 上，**只更新必要的节点**（而非重新渲染整个 DOM 树），从而减少重排 / 重绘次数。

**四、虚拟 DOM 的核心优势**

1. **提升性能**：用低成本的 JavaScript 计算替代高成本的 DOM 操作，减少重排 / 重绘。
2. **简化开发**：开发者只需描述 “UI 应该是什么样子”（基于状态），无需手动操作 DOM（框架自动处理差异更新）。
3. **跨平台能力**：虚拟 DOM 是与平台无关的 JavaScript 对象，可被渲染到不同平台（如 React 中，虚拟 DOM 可通过 `ReactDOM` 渲染到浏览器 DOM，通过 `ReactNative` 渲染到原生组件）。
4. **批量更新**：所有状态变化可先在虚拟 DOM 层累积，再一次性更新到真实 DOM，避免频繁的 DOM 操作。

**五、虚拟 DOM 的局限性**

1. **额外的计算开销**：生成虚拟 DOM 和 Diff 对比需要消耗 JavaScript 执行时间（但通常远小于直接操作 DOM 的开销）。
2. **并非所有场景都更优**：对于简单的、频繁更新的场景（如输入框实时校验），直接操作 DOM 可能比虚拟 DOM 更快（因此 Vue 提供了 `v-directive`、React 提供了 `useRef` 等绕过虚拟 DOM 的方案）。

**六、虚拟 DOM 与真实 DOM 的核心区别**

| 维度    | 真实 DOM         | 虚拟 DOM                  |
| ----- | -------------- | ----------------------- |
| 本质    | 浏览器渲染引擎管理的节点   | JavaScript 对象（内存中的数据结构） |
| 操作成本  | 高（触发重排 / 重绘）   | 低（纯 JS 计算）              |
| 跨平台性  | 依赖浏览器环境        | 与平台无关（可渲染到任何环境）         |
| 属性复杂度 | 包含大量浏览器内置属性和方法 | 只包含必要的描述性属性（轻量）         |

**总结**

虚拟 DOM 是前端框架解决 “高效更新 UI” 问题的核心方案，其核心逻辑是：**用 JavaScript 对象描述 DOM 结构，通过 Diff 算法计算最小更新差异，最终批量应用到真实 DOM**。这一机制既降低了 DOM 操作的性能开销，又简化了开发流程，同时为跨平台渲染提供了基础。

理解虚拟 DOM 有助于深入掌握 React、Vue 等框架的渲染原理，以及在性能优化时做出更合理的决策（如合理使用 `key`、避免不必要的渲染等）。

### React 渲染流程

**记忆点：跟组件渲染流程差不多**

**从「状态更新」到「UI 最终呈现」的完整过程，主要分为 触发更新、协调（Reconciliation）、渲染（Rendering）、提交（Commit） 四个核心阶段。**

1. **点击按钮 → 调用 `setCount`（触发更新）。**
2. **协调阶段：**  
   * **重新执行组件函数，生成新的虚拟 DOM。**  
   * **Diff 算法对比新旧虚拟 DOM，发现计数器文本变化。**  
   * **Fiber 树标记该节点为「需要更新（Update）」。**
3. **渲染阶段：通知 `ReactDOM` 准备更新计数器节点。**
4. **提交阶段：**  
   * **修改真实 DOM 中计数器的文本。**  
   * **执行依赖 `count` 的 `useEffect` 回调。**

React 的渲染流程是从「状态更新」到「UI 最终呈现」的完整过程，主要分为 **触发更新、协调（Reconciliation）、渲染（Rendering）、提交（Commit）** 四个核心阶段。理解这一流程有助于优化组件性能、避免不必要的渲染。

**1\. 触发更新（Update Trigger）**

渲染流程的起点是「状态变化」，常见触发场景包括：

* 组件初始化（首次渲染）。
* 组件内部 `setState`（类组件）或 `setXxx`（函数组件 `useState`）调用。
* 父组件传递的 `props` 发生变化。
* `useReducer` 触发的状态更新。

当状态变化时，React 会标记该组件为「需要更新」，并进入协调阶段。

**2\. 协调阶段（Reconciliation）：计算差异（Diffing）**

协调阶段是 React 的「核心优化阶段」，目的是**找出新旧虚拟 DOM（Virtual DOM）的差异**，确定需要更新的部分（最小化 DOM 操作）。

**核心步骤：**

* **生成虚拟 DOM（Virtual DOM）**虚拟 DOM 是 React 对真实 DOM 的轻量抽象（JavaScript 对象），描述了 UI 的结构和属性。 当组件状态更新时，React 会调用组件的 `render` 方法（类组件）或重新执行函数组件，生成**新的虚拟 DOM 树**。
* **Diff 算法：对比新旧虚拟 DOM**React 通过高效的 Diff 算法对比新旧虚拟 DOM 树，找出差异（哪些节点需要新增、删除、修改）。 Diff 算法的特点：  
   1. **同层比较**：只对比同一层级的节点（不跨层级比较，降低复杂度）。  
   2. **列表节点用 `key` 区分**：对于列表，通过 `key` 标识节点身份，避免因顺序变化导致的误判（`key` 不变则认为是同一节点，仅更新内容）。  
   3. **类型判断**：若节点类型（如 [`div`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.div.md) vs [`span`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.span.md)）不同，直接销毁旧节点并创建新节点（不深入比较子节点）。
* **生成 Fiber 树**React 16+ 引入「Fiber 架构」，将虚拟 DOM 的 Diff 过程拆分为可中断、可恢复的小单元（Fiber 节点）。每个 Fiber 节点对应一个组件或 DOM 元素，记录了节点的类型、属性、子节点、更新优先级等信息。 协调阶段会构建「新的 Fiber 树」，标记出需要更新的节点（如 `Placement` 新增、`Update` 修改、`Deletion` 删除）。

**3\. 渲染阶段（Rendering）：准备更新**

协调阶段完成后，React 会根据 Fiber 树的标记，确定每个节点的具体更新操作，并通知「渲染器（Renderer）」。

* **渲染器的作用**：React 本身不直接操作 DOM，而是通过渲染器（如浏览器环境的 `ReactDOM`、移动平台的 `React Native`）处理具体平台的渲染逻辑。
* 此阶段是「纯计算阶段」，不操作真实 DOM，可被浏览器的事件循环中断（优先处理用户输入等高频任务），保证 UI 响应流畅。

**4\. 提交阶段（Commit）：更新真实 DOM**

提交阶段是「实际操作真实 DOM」的阶段，不可中断，主要做三件事：

1. **执行 DOM 操作**根据 Fiber 树的标记，批量执行真实 DOM 的增删改（如 `appendChild`、`removeChild`、修改属性等），最小化 DOM 操作以提升性能。
2. **执行副作用（Side Effects）**  
   * 类组件：调用 `componentDidMount`（首次渲染）、`componentDidUpdate`（更新）、`componentWillUnmount`（卸载）等生命周期方法。  
   * 函数组件：执行 `useEffect`、`useLayoutEffect` 等钩子的回调（`useLayoutEffect` 在 DOM 更新后同步执行，`useEffect` 在浏览器绘制后异步执行）。
3. **更新引用和状态**更新组件的真实 DOM 引用（如 `useRef`），并标记更新完成。

**总结：完整流程示例**

以「点击按钮更新计数器」为例：

1. 点击按钮 → 调用 `setCount`（触发更新）。
2. 协调阶段：  
   * 重新执行组件函数，生成新的虚拟 DOM。  
   * Diff 算法对比新旧虚拟 DOM，发现计数器文本变化。  
   * Fiber 树标记该节点为「需要更新（Update）」。
3. 渲染阶段：通知 `ReactDOM` 准备更新计数器节点。
4. 提交阶段：  
   * 修改真实 DOM 中计数器的文本。  
   * 执行依赖 `count` 的 `useEffect` 回调。

React 渲染流程的核心是「通过虚拟 DOM 和 Diff 算法减少真实 DOM 操作」，结合 Fiber 架构实现可中断的渲染，平衡性能与用户体验。

### 为什么要使用HOOK？

在 React 中，**Hook** 是 React 16.8 引入的特性，其核心目的是**解决类组件（Class Component）的固有缺陷**，同时让函数组件（Function Component）能够拥有状态管理和副作用处理能力，最终让代码更简洁、逻辑更清晰、复用更高效。

**为什么需要 Hook？—— 类组件的痛点**

在 Hook 出现之前，React 组件主要通过 “类组件” 实现复杂逻辑（如状态管理、生命周期），但类组件存在几个明显问题：

1. **逻辑复用困难，容易导致 “嵌套地狱”**

类组件中复用状态逻辑的主流方式是 **高阶组件（HOC）** 或 **Render Props**，但这两种方式都会导致组件层级嵌套过深（“Wrapper Hell”）。

例如，用高阶组件复用 “权限校验” 和 “数据加载” 逻辑：

```jsx
// 高阶组件嵌套示例
const EnhancedComponent = withAuth(withData(FooComponent));

// 渲染时的实际结构（嵌套层级多，调试困难）
<WithAuth>
  <WithData>
    <FooComponent />
  </WithData>
</WithAuth>

```

而 Hook 允许直接在函数组件中**提取和复用逻辑**，无需修改组件结构：

```jsx
// 用自定义 Hook 复用逻辑（无嵌套）
function FooComponent() {
  const { user } = useAuth(); // 复用权限逻辑
  const { data } = useData(); // 复用数据加载逻辑
  // ...
}

```

1. **复杂组件难以维护，逻辑分散**

类组件中，**相关逻辑往往被拆分到不同的生命周期方法中**，导致代码碎片化。

例如，一个 “数据请求 + 订阅事件 + 清理” 的逻辑：

```jsx
class MyComponent extends React.Component {
  state = { data: null };

  componentDidMount() {
    // 1. 数据请求
    fetchData().then(data => this.setState({ data }));
    // 2. 订阅事件
    window.addEventListener('resize', this.handleResize);
  }

  componentDidUpdate(prevProps) {
    // 3. 依赖变化时重新请求数据（与 mount 时的请求逻辑分离）
    if (prevProps.id !== this.props.id) {
      fetchData().then(data => this.setState({ data }));
    }
  }

  componentWillUnmount() {
    // 4. 清理事件订阅（与 mount 时的订阅逻辑分离）
    window.removeEventListener('resize', this.handleResize);
  }

  // ...
}

```

相关的 “数据请求” 和 “事件订阅” 逻辑被拆到 3 个生命周期中，维护时需要在多个方法间跳转，容易遗漏逻辑（比如忘记清理）。

而 Hook 可以将**相关逻辑聚合到一起**（如 `useEffect`）：

```jsx
function MyComponent({ id }) {
  const [data, setData] = useState(null);

  // 数据请求 + 依赖处理（聚合相关逻辑）
  useEffect(() => {
    fetchData().then(data => setData(data));
  }, [id]); // 仅当 id 变化时重新执行

  // 事件订阅 + 清理（聚合相关逻辑）
  useEffect(() => {
    const handleResize = () => {/* ... */};
    window.addEventListener('resize', handleResize);
    // 清理函数（与订阅逻辑放在一起）
    return () => window.removeEventListener('resize', handleResize);
  }, []); // 仅执行一次

  // ...
}

```

逻辑按功能聚合，而非按生命周期拆分，代码可读性和可维护性大幅提升。

1. **类组件的 “this” 绑定问题**

类组件中，`this` 的指向是动态的，需要手动绑定（如在构造函数中 `bind`，或用箭头函数），否则容易出现 `this` 指向错误：

```jsx
class MyComponent extends React.Component {
  state = { count: 0 };

  constructor(props) {
    super(props);
    // 必须手动绑定 this，否则调用时 this 为 undefined
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState({ count: this.state.count + 1 });
  }

  render() {
    return <button onClick={this.handleClick}>点击</button>;
  }
}

```

而函数组件中**没有 “this”**，所有变量和函数的作用域明确，避免了 `this` 绑定的心智负担：

```jsx
function MyComponent() {
  const [count, setCount] = useState(0);

  // 无需绑定 this，直接使用
  const handleClick = () => {
    setCount(count + 1);
  };

  return <button onClick={handleClick}>点击</button>;
}

```

1. **函数组件的功能限制被打破**

在 Hook 出现前，函数组件只能是 “无状态组件”（Stateless Component），无法拥有自己的状态或处理副作用（如数据请求、事件监听），只能依赖 props 渲染 UI。

Hook 让函数组件能够：

* 通过 `useState` 拥有自己的状态；
* 通过 `useEffect` 处理副作用（数据请求、事件订阅等）；
* 通过 `useContext` 消费上下文；
* 通过 `useReducer` 处理复杂状态逻辑；
* 等等。

如今，函数组件 + Hook 可以实现类组件的所有功能，且写法更简洁。

**总结：Hook 的核心价值**

1. **简化逻辑复用**：用自定义 Hook 替代高阶组件和 Render Props，避免组件嵌套，让逻辑复用更直观。
2. **聚合相关逻辑**：将分散在生命周期中的代码按功能聚合，提升复杂组件的可维护性。
3. **消除 this 困扰**：函数组件中无需处理 this 绑定，减少错误和冗余代码。
4. **增强函数组件能力**：让函数组件支持状态和副作用，成为 React 组件的主流编写方式。

简言之，Hook 让 React 代码更**简洁、灵活、易于维护**，是 React 开发范式的一次重要升级，目前已成为 React 开发的推荐方式。

### 什么是react得调度？怎么实现得？

**React 调度的核心实现**

React 的调度机制主要依赖两个核心部分：**Scheduler 调度器**和**Fiber 架构**，二者配合实现 “可中断、可恢复、优先级驱动” 的任务执行。

1. Scheduler 调度器：管理任务优先级与执行时机

React 内置了一个独立的 `scheduler` 包（可单独使用），负责：

* 对任务进行优先级分级；
* 按照优先级排序并调度任务执行；
* 利用浏览器空闲时间执行低优先级任务，避免阻塞主线程。

**（1）优先级分级**

Scheduler 将任务分为不同优先级（从高到低）：

* **Immediate**：同步执行（最高优先级，如 `flushSync` 触发的更新）；
* **UserBlocking**：用户阻塞级（如点击、输入等交互，需在 250ms 内响应）；
* **Normal**：普通优先级（如网络请求后的 UI 更新）；
* **Low**：低优先级（如非紧急的数据计算）；
* **Idle**：空闲时执行（最低优先级，如日志上报，可延迟至浏览器完全空闲）。

优先级通过 “过期时间”（expiration time）量化：优先级越高，过期时间越近（即需要尽快执行）。

**（2）时间切片（Time Slicing）**

为避免长任务阻塞主线程，Scheduler 实现了 “时间切片”：将一个长任务拆分成多个小任务，每个小任务执行时间不超过**5ms**（约为单帧时间的 1/3），剩余时间交还给浏览器处理 UI 和用户事件。

实现依赖浏览器的 **`requestIdleCallback` 模拟**（原生 `requestIdleCallback` 兼容性差且触发频率低，React 用 `setTimeout` 和 `requestAnimationFrame` 做了 polyfill）：

* 每次执行任务前，计算当前可用时间（`deadline`）；
* 若任务执行超过可用时间，立即暂停，登记下一次执行；
* 等浏览器处理完其他任务后，再恢复执行剩余部分。

**（3）任务队列与调度循环**

* Scheduler 维护一个**优先级队列**（最小堆实现），按任务过期时间排序；
* 调度循环（`workLoop`）不断从队列中取出 “最紧急”（优先级最高）的任务执行；
* 若执行中出现更高优先级的新任务，会中断当前任务，优先执行新任务（“抢占式调度”）。

**2\. Fiber 架构：支持任务的中断与恢复**

Fiber 是 React 16 引入的新数据结构，本质是 “可中断的工作单元”。每个 Fiber 节点对应一个组件，存储了组件的类型、DOM 信息、更新状态等。

Fiber 架构为调度提供了基础：

* **任务拆分**：将组件树的渲染（`reconciliation`）过程拆分成单个 Fiber 节点的处理（如计算新状态、比较子节点）；
* **可中断与恢复**：每个 Fiber 节点的处理可以被暂停、标记，后续恢复时从暂停处继续（通过 `alternate` 属性保存当前状态）；
* **优先级关联**：每个 Fiber 节点会记录对应的任务优先级，方便调度器判断是否需要中断当前任务，执行更高优先级任务。

**3\. 调度流程（简化版）**

当触发组件更新（如 `setState`、`useState` 更新）时，React 的调度流程大致如下：

1. **触发更新**：生成更新任务，计算任务优先级（根据更新源，如用户交互触发高优先级）；
2. **提交任务**：将任务交给 Scheduler，加入优先级队列；
3. **调度执行**：Scheduler 从队列中取出最高优先级任务，启动执行；
4. Fiber 工作循环：  
   * 执行当前 Fiber 节点的处理（如 `beginWork`）；  
   * 检查是否超时（超过时间切片）或有更高优先级任务；  
   * 若需中断：保存当前 Fiber 状态，将控制权交回浏览器；  
   * 若未中断：继续处理下一个 Fiber 节点，直到完成整棵树的协调（`reconciliation`）；
5. **提交阶段（Commit）**：完成协调后，一次性更新 DOM（此阶段不可中断，确保 UI 一致性）。

**总结**

React 的调度是 “优先级驱动 + 可中断执行” 的机制，核心依赖：

* **Scheduler**：负责优先级管理、时间切片、任务队列调度，确保高优先级任务优先执行，避免阻塞主线程；
* **Fiber 架构**：将渲染任务拆分为可中断的工作单元，支持任务的暂停、恢复和抢占，配合调度器实现灵活的执行控制。

这种机制让 React 能够在处理复杂 UI 更新时，依然保持流畅的用户交互体验，是 React 并发模式（Concurrent Mode）的核心基础。

### Fiber

#### **react Fiber怎么做让react性能进行了提升**

记忆点：

解决了什么问题，解决了传统协调算法的性能瓶颈，同步递归，无法中断，无法优先级调度造成页面的卡顿问题

通过：**增量渲染**（Incremental Rendering）和**优先级调度**

核心优化：**1\. 任务分片与增量渲染**，**2\. 优先级调度**，**3\. 双缓存树（Double Buffering）**，4\. 生命周期细化与副作用处理，**5\. 浏览器友好的调度策略**

React Fiber 是 React 16.x 版本引入的协调算法（Reconciliation Algorithm）的重构，它通过**增量渲染**（Incremental Rendering）和**优先级调度**（Priority Scheduling）解决了传统协调算法的性能瓶颈，显著提升了大型应用的响应速度和用户体验。其核心优化机制如下：

**1\. 任务分片与增量渲染**

传统 React 的协调过程是**同步递归**的，在复杂组件树中可能导致长时间阻塞主线程，引发页面卡顿。Fiber 将渲染任务拆分为多个**小任务单元**（Fiber 节点），允许浏览器在任务间隙处理高优先级事件（如用户输入、动画）：

```javascript
// 传统协调（同步递归，可能导致卡顿）
function reconcileChildren(currentChildren, newChildren) {
  // 递归比较所有子节点，直到完成
}

// Fiber 协调（异步可中断，分阶段执行）
function workLoopConcurrent() {
  while (workInProgress !== null && !shouldYield()) {
    workInProgress = performUnitOfWork(workInProgress);
  }
}

```

**2\. 优先级调度**

Fiber 为不同类型的更新分配**优先级**（如动画更新优先级高于数据加载），允许高优先级任务中断低优先级任务：

```javascript
// 不同类型更新的优先级示例
const HIGH_PRIORITY = 1; // 如用户输入、动画
const LOW_PRIORITY = 5;  // 如数据获取、UI 渲染

// 调度器可根据优先级暂停或恢复任务
scheduleCallback(LOW_PRIORITY, () => {
  // 低优先级更新任务
});

```

**3\. 双缓存树（Double Buffering）**

Fiber 使用**双缓存技术**维护两棵 Fiber 树（current 和 workInProgress），在内存中完成所有变更计算后一次性提交，减少 DOM 操作次数：

```javascript
// 当前渲染的树
let currentRoot = null;
// 正在构建的工作树
let workInProgressRoot = null;

function commitRoot() {
  // 将内存中完成的变更一次性应用到 DOM
  commitWork(workInProgressRoot);
  currentRoot = workInProgressRoot;
}

```

**4\. 生命周期细化与副作用处理**

Fiber 将生命周期方法分为**render 阶段**（可中断）和**commit 阶段**（不可中断），并引入 `useEffect` 等 API 处理副作用，避免不必要的重复渲染：

```javascript
// 渲染阶段（可中断，纯计算）
function render() {
  return <Component />;
}

// 提交阶段（DOM 操作、副作用执行）
useEffect(() => {
  // 副作用操作（如订阅、DOM 更新）
  return () => cleanup; // 清理函数
}, [dependencies]);

```

**5\. 浏览器友好的调度策略**

Fiber 利用 `requestIdleCallback` 或 `MessageChannel` 实现**空闲时段渲染**，确保在浏览器帧间隙执行低优先级任务：

```javascript
// 使用 MessageChannel 实现微任务调度
const channel = new MessageChannel();
const port = channel.port2;
channel.port1.onmessage = performWorkUntilDeadline;

function scheduleWork() {
  port.postMessage(null); // 在下一个空闲时段执行任务
}

```

**性能提升的具体表现**

* **动画 / 交互流畅度**：高优先级更新（如滚动、过渡）可立即执行，避免卡顿
* **大型应用响应速度**：复杂组件树的渲染被分片，用户操作能及时响应
* **资源利用率**：通过优先级调度，减少不必要的渲染开销

React Fiber 通过架构层面的重构，从根本上解决了传统协调算法的性能瓶颈，为现代 Web 应用提供了更高效、更流畅的用户体验。

#### react fiber为什么使用它，原理是什么

记忆点：**解决了什么问题，解决了传统协调算法的性能瓶颈，同步递归，无法中断，无法优先级调度造成页面的卡顿问题**

**通过：增量渲染（Incremental Rendering）和优先级调度**

**Fiber 的核心原理：可中断的工作单元与优先级调度**

**1\. Fiber 节点：工作单元的载体**

**2.工作循环（Work Loop）：分阶段处理工作单元**

**（1）协调阶段（Reconciliation Phase）：可中断的 “计算阶段”**

**（2）提交阶段（Commit Phase）：不可中断的 “执行阶段”**

**3\. 优先级调度：优先处理关键任务**

**（1）优先级划分**

**（2）调度机制**

**将渲染工作拆分为可中断的 “Fiber 工作单元”，通过链表结构实现非递归遍历，配合优先级调度机制，在保证 UI 正确更新的同时，优先响应高优先级任务（如用户输入），避免主线程阻塞**。

React Fiber 是 React 16 引入的**新协调引擎（Reconciliation Engine）**，其核心目标是解决传统 React 架构中 “长时间渲染阻塞主线程” 的问题，让 React 应用在处理复杂 UI 更新时保持流畅的用户交互（如点击、滚动、动画等）。

**一、为什么需要 Fiber？传统架构的痛点**

在 Fiber 之前，React 使用**栈式协调器（Stack Reconciler）** 处理组件渲染。其工作方式是：从根组件开始，递归遍历所有子组件，同步执行 “Diff 对比→计算更新→渲染 DOM” 的全过程，一旦开始就无法中断 —— 如果组件树层级较深（如 1000 层），这一过程可能持续 100ms 以上（超过人眼感知的 16ms 阈值），导致主线程被阻塞，页面无法响应用户输入或动画，产生卡顿。

具体来说，传统架构的问题包括：

1. **不可中断**：渲染过程一旦开始，必须完整执行，无法被高优先级任务（如用户点击）打断。
2. **递归调用栈限制**：依赖 JavaScript 函数调用栈递归遍历组件树，层级过深可能导致栈溢出。
3. **无法优先级调度**：所有更新任务（如 UI 渲染、动画、用户输入）优先级相同，无法优先处理关键任务。

**二、Fiber 的核心原理：可中断的工作单元与优先级调度**

Fiber 的本质是**将渲染工作分解为可中断、可恢复的 “小单元”**，并通过优先级调度决定这些单元的执行顺序，从而避免主线程长时间阻塞。其核心设计包括以下几点：

**1\. Fiber 节点：工作单元的载体**

Fiber 将每个组件（或 DOM 节点）抽象为一个**Fiber 节点**，每个节点代表一个 “工作单元”。Fiber 节点不仅包含组件的类型、属性、DOM 信息等，还添加了用于 “中断与恢复” 的关键信息：

```javascript
const fiberNode = {
  type: 'div', // 组件类型（如 'div' 或自定义组件）
  props: { className: 'box' }, // 组件属性
  stateNode: document.createElement('div'), // 对应的真实 DOM 节点（或组件实例）
  // 以下为 Fiber 核心控制字段
  parent: parentFiber, // 父 Fiber 节点（构成树结构）
  child: childFiber, // 第一个子 Fiber 节点
  sibling: nextFiber, // 下一个兄弟 Fiber 节点（替代递归栈，实现链表遍历）
  alternate: currentFiber, // 指向当前节点的“备用节点”（用于存储新旧状态对比）
  effectTag: 'UPDATE', // 标记当前节点的更新类型（如更新、新增、删除）
  expirationTime: 100, // 优先级时间戳（用于判断任务优先级）
  // ... 其他状态字段
};

```

**核心改进**：

* 用**链表结构**（`parent`/`child`/`sibling`）替代递归栈，使遍历过程可中断（无需依赖函数调用栈）。
* 每个 Fiber 节点对应一个 “工作单元”，工作单元的处理（如 Diff 对比、计算更新）可以独立完成，便于拆分和中断。

**2\. 工作循环（Work Loop）：分阶段处理工作单元**

Fiber 将渲染过程拆分为两个阶段，通过 “工作循环” 调度执行，支持中断和恢复：

**（1）协调阶段（Reconciliation Phase）：可中断的 “计算阶段”**

* **任务**：遍历 Fiber 树（基于链表），对比新旧节点（Diff 算法），标记需要更新的节点（`effectTag`），并构建 “Effect List”（记录所有需要执行的 DOM 操作）。
* **特点**：纯 JavaScript 计算，**可被中断**（如更高优先级任务到来时暂停，保存当前进度）。中断后可从上次暂停的 Fiber 节点继续处理。

**（2）提交阶段（Commit Phase）：不可中断的 “执行阶段”**

* **任务**：根据协调阶段生成的 “Effect List”，执行实际的 DOM 操作（新增、删除、修改节点），并调用组件生命周期钩子（如 `componentDidMount`、`useEffect`）。
* **特点**：直接操作 DOM 和用户可见的状态，**不可中断**（避免 DOM 处于不一致状态，影响用户体验）。

**3\. 优先级调度：优先处理关键任务**

Fiber 配合 **Scheduler（调度器）** 实现任务优先级管理，确保高优先级任务（如用户输入、动画）优先执行，低优先级任务（如列表渲染）可被中断。

* **优先级划分**：React 定义了不同优先级的任务（从高到低）：  
   * 同步优先级（Synchronous）：如用户输入回调，必须立即执行，不可中断。  
   * 用户阻塞优先级（UserBlocking）：如动画、滚动，需要在短时间内完成。  
   * 正常优先级（Normal）：如网络请求后的 UI 更新，可延迟但不太久。  
   * 低优先级（Low）：如非紧急的后台计算。  
   * 空闲优先级（Idle）：仅在浏览器空闲时执行（如日志上报）。
* **调度机制**：  
   1. 每次处理一个工作单元前，Scheduler 检查是否有更高优先级任务；  
   2. 若有，暂停当前工作单元，保存进度，先处理高优先级任务；  
   3. 高优先级任务完成后，从上次暂停的位置恢复低优先级任务。  
（底层依赖 `requestIdleCallback` 或模拟的空闲时间检测，利用浏览器主线程的空闲时段处理低优先级任务。）

**三、Fiber 带来的核心价值**

1. **解决主线程阻塞**：通过拆分工作单元和中断机制，避免长时间占用主线程，保证用户交互和动画的流畅性。
2. **支持优先级调度**：关键任务（如输入、动画）优先执行，提升应用响应速度。
3. **为并发模式奠定基础**：Fiber 的可中断特性是 React 并发模式（Concurrent Mode）的核心，支持 “同一时间存在多个 UI 版本”（如渲染一个版本的同时准备另一个版本），进一步优化用户体验。
4. **避免栈溢出**：用链表遍历替代递归栈，支持更深层级的组件树渲染。

**总结**

Fiber 是 React 为解决 “大型应用渲染卡顿” 问题而设计的新型协调引擎，其核心原理是：**将渲染工作拆分为可中断的 “Fiber 工作单元”，通过链表结构实现非递归遍历，配合优先级调度机制，在保证 UI 正确更新的同时，优先响应高优先级任务（如用户输入），避免主线程阻塞**。

这一设计从根本上改善了 React 应用的性能和用户体验，同时为后续的并发特性（如 Suspense、并发渲染）提供了基础。

#### react onClick事件可以中断嘛？

React 中的 `onClick` 事件处理函数本身的**同步执行过程无法被中断**，但它所触发的**后续渲染更新（如状态变化引发的重新渲染）可以被中断**，这与 React 的事件机制和 Fiber 架构密切相关。

React 中的 `onClick` 事件处理函数本身的**同步执行过程无法被中断**，但它所触发的**后续渲染更新（如状态变化引发的重新渲染）可以被中断**，这与 React 的事件机制和 Fiber 架构密切相关。具体可从以下两方面理解：

**一、`onClick` 事件处理函数的执行：不可中断的同步过程**

当用户触发 `onClick` 事件时，React 的事件处理流程是：

1. 原生 DOM 事件冒泡至顶层委托节点，React 捕获事件并创建合成事件对象；
2. 调用开发者定义的 `onClick` 处理函数（如 `handleClick`），此函数在**主线程**中同步执行。

由于 JavaScript 是**单线程**的，一旦 `onClick` 处理函数开始执行，在其完成前（或遇到异步操作前），主线程会被独占，无法被其他任务（包括高优先级任务）中断。例如

```jsx
function handleClick() {
  // 模拟耗时的同步操作（如大量循环计算）
  for (let i = 0; i < 1000000000; i++) {} 
  console.log("处理完成");
}

<button onClick={handleClick}>点击</button>

```

点击按钮后，`handleClick` 中的循环会阻塞主线程，期间页面无法响应其他交互（如滚动、输入），直到循环完成。

**二、`onClick` 触发的更新：可被中断的渲染过程**

`onClick` 事件通常会触发状态更新（如 `setState` 或 `useState` 的更新函数），而状态更新引发的**组件重新渲染过程（协调阶段）是可以被中断的**，这依赖于 Fiber 架构的特性：

1. **状态更新进入调度队列**：调用 `setState` 后，React 会将更新任务加入队列，并由 Scheduler（调度器）根据优先级排序。
2. **协调阶段（Reconciliation）可中断**：在 Fiber 架构中，重新渲染的 “协调阶段”（计算虚拟 DOM 差异）被拆分为多个小工作单元，执行过程中会定期检查是否有更高优先级任务（如用户输入、动画）。若有，则暂停当前更新，先处理高优先级任务，稍后再恢复。
3. **提交阶段不可中断**：最终将差异应用到真实 DOM 的 “提交阶段” 不可中断，但此阶段耗时通常极短。

例如，`onClick` 触发一个列表渲染的更新，若此时用户快速输入文字（高优先级任务），React 会中断列表渲染的协调过程，优先处理输入事件，避免输入卡顿。

**三、如何避免 `onClick` 处理函数阻塞主线程？**

若 `onClick` 处理函数包含耗时操作（如复杂计算），即使其执行不可中断，也可通过以下方式避免阻塞：

1. 拆分耗时操作为异步任务：用  
```arduino  
setTimeout  
```  
或  
```txt  
requestIdleCallback  
```  
将同步计算拆分为小块，让主线程有间隙处理其他任务：  
```jsx  
function handleClick() {  
  // 异步执行耗时操作，避免阻塞  
  setTimeout(() => {  
    const result = heavyCalculation(); // 耗时计算  
    setData(result);  
  }, 0);  
}  
```
2. **使用 Web Workers**：将计算密集型任务放入 Web Worker 中执行（不阻塞主线程），完成后通过消息通知主线程更新状态。

**总结**

* **`onClick` 事件处理函数本身**：作为同步 JavaScript 代码，执行过程不可中断，耗时操作会阻塞主线程。
* **`onClick` 触发的更新渲染**：在 Fiber 架构下，更新的 “协调阶段” 可被高优先级任务中断，保证用户交互的流畅性。

实际开发中，应避免在 `onClick` 中编写过长的同步代码，通过异步化或多线程方案优化性能。

#### 可中断的事件是那些

注意：在 React 官方文档和源码中，“渲染阶段（Render Phase）” 通常是对「协调阶段（Reconciliation）」的另一种描述（或包含协调阶段的核心工作）。它强调的是 “计算需要更新什么” 的过程，而非 “实际更新 DOM”。

记忆点：

**协调阶段**

以下操作在协调阶段执行，因此可能被中断：

1. **组件的 `render` 方法**：计算并返回虚拟 DOM 结构的过程。
2. **函数组件的执行**：整个函数组件的逻辑（包括 Hooks 调用，如 `useState`、`useEffect` 的回调计算等）。
3. 生命周期方法（类组件）:
4. **虚拟 DOM 的 Diff 算法执行**：对比新旧 Fiber 树的差异。

**提交阶段（Commit）**

当协调阶段完成后，React 进入提交阶段（也叫 “提交阶段”），此阶段的工作是**将协调阶段计算出的差异应用到真实 DOM 上**，包括：

* 插入、更新、删除真实 DOM 节点
* 执行副作用（如 `useEffect` 的回调、类组件的 `componentDidMount`/`componentDidUpdate`/`componentWillUnmount`）

这个阶段**不可中断**，原因是：

1. **操作真实 DOM 是同步的，一旦开始就必须完成，否则会导致 DOM 状态不一致（如只插入了部分节点，导致 UI 错乱）。**
2. **副作用（如数据请求、事件监听）需要在 DOM 操作完成后执行，中断会导致逻辑错误（如监听还没绑定，用户操作就触发了）**。

在 React 中，**可中断的过程主要集中在 “协调阶段（Reconciliation）”**，这是 React 16 引入 Fiber 架构后实现的核心特性。其设计目的是让 React 能够在执行耗时任务时，响应更高优先级的操作（如用户输入、动画等），避免应用卡顿。

**一、可中断的核心阶段：协调阶段（Reconciliation）**

协调阶段（也叫 “渲染阶段”）的主要工作是：

* 找出前后两次虚拟 DOM（Fiber 树）的差异（Diffing）
* 确定哪些节点需要更新、新增或删除
* 为这些节点标记对应的操作（如 “插入”“更新”“删除”）

这个阶段的所有工作**都是 “可中断、可暂停、可恢复、甚至可放弃” 的**，原因是

1. Fiber 架构将整个任务拆分成了无数个小单元（Fiber 节点），每个单元对应一个组件或 DOM 节点的处理。
2. 每个小单元执行完成后，React 会检查是否有更高优先级的任务（如用户点击、键盘输入等）。如果有，就暂停当前任务，先处理高优先级任务；待高优先级任务完成后，再恢复之前的任务。
3. 此阶段不会直接操作真实 DOM，仅在内存中计算差异，因此即使中断也不会导致 UI 不一致。

**二、属于可中断阶段的具体操作**

以下操作在协调阶段执行，因此可能被中断：

1. **组件的 `render` 方法**：计算并返回虚拟 DOM 结构的过程。
2. **函数组件的执行**：整个函数组件的逻辑（包括 Hooks 调用，如 `useState`、`useEffect` 的回调计算等）。
3. 生命周期方法（类组件）:  
   * `shouldComponentUpdate`：判断组件是否需要更新的计算过程。  
   * `getDerivedStateFromProps`：从 props 推导 state 的过程。  
   * `getSnapshotBeforeUpdate`：在提交阶段前获取快照（严格来说属于协调阶段末尾，接近提交阶段，中断可能性低）。
4. **虚拟 DOM 的 Diff 算法执行**：对比新旧 Fiber 树的差异。

**三、不可中断的阶段：提交阶段（Commit）**

当协调阶段完成后，React 进入提交阶段（也叫 “提交阶段”），此阶段的工作是**将协调阶段计算出的差异应用到真实 DOM 上**，包括：

* 插入、更新、删除真实 DOM 节点
* 执行副作用（如 `useEffect` 的回调、类组件的 `componentDidMount`/`componentDidUpdate`/`componentWillUnmount`）

这个阶段**不可中断**，原因是：

1. **操作真实 DOM 是同步的，一旦开始就必须完成，否则会导致 DOM 状态不一致（如只插入了部分节点，导致 UI 错乱）。**
2. **副作用（如数据请求、事件监听）需要在 DOM 操作完成后执行，中断会导致逻辑错误（如监听还没绑定，用户操作就触发了）**。

**四、为什么需要 “可中断”？**

React 设计可中断的协调阶段，核心是为了**保证应用的响应性**。例如：

* 当用户在输入框打字时（高优先级任务），如果 React 正在执行一个复杂的列表渲染（低优先级任务），可以暂停渲染，先处理输入事件，避免用户输入卡顿。
* 动画帧更新（高优先级）可以打断耗时的组件计算，确保动画流畅。

**总结**

React 中**只有协调阶段（计算差异、生成新 Fiber 树）是可中断的**，而提交阶段（操作 DOM、执行副作用）不可中断。这种设计是 Fiber 架构的核心，通过 “时间切片”（Time Slicing）机制，让 React 能够在复杂场景下保持应用的响应性。

#### useEffect子组件重复渲染重复进行请求，怎么进行解决

在 React 中，子组件因`useEffect`导致重复渲染和重复请求，通常与依赖项处理、组件记忆化或数据缓存有关。以下是具体解决方法：

**1\. 优化`useEffect`的依赖项**

`useEffect`会在依赖项变化时重新执行。若依赖项是**每次渲染都会生成新引用的值**（如对象、数组、匿名函数），会导致不必要的重复执行。

**错误示例**：

```jsx
// 子组件
function Child({ id }) {
  // 每次渲染都会创建新对象，导致useEffect重复执行
  const params = { id: id }; 

  useEffect(() => {
    fetchData(params); // 重复请求
  }, [params]); // 错误：params引用每次都变
}

```

**解决方法**：

* 依赖项使用原始值（而非对象 / 数组）
* 用`useMemo`记忆复杂依赖项

```jsx
function Child({ id }) {
  // 用useMemo记忆对象，确保引用稳定
  const params = useMemo(() => ({ id }), [id]); 

  useEffect(() => {
    fetchData(params); 
  }, [params]); // 仅当id变化时执行
}

```

**2\. 防止子组件不必要的重渲染**

父组件重渲染时，子组件可能被连带重渲染，导致`useEffect`重复触发。可通过以下方式优化：

**（1）用`React.memo`记忆子组件**

`React.memo`会浅比较 props，若 props 未变化则阻止子组件重渲染。

```jsx
// 用React.memo包装子组件
const Child = React.memo(({ id, fetchData }) => {
  useEffect(() => {
    fetchData(id);
  }, [id, fetchData]);

  return <div>...</div>;
});

```

**（2）用`useCallback`记忆父组件传递的函数**

父组件的函数若未被记忆，每次渲染会生成新引用，导致子组件的`fetchData` props 变化，触发重渲染。

```jsx
// 父组件
function Parent() {
  // 用useCallback记忆函数，确保引用稳定
  const fetchData = useCallback((id) => {
    // 请求逻辑
  }, []); // 依赖项为空，函数仅创建一次

  return <Child id={id} fetchData={fetchData} />;
}

```

**3\. 缓存请求结果，避免重复请求**

即使`useEffect`执行，也可通过缓存避免重复请求相同数据（如用`useState`\+ 条件判断，或专门的缓存库）。

**示例：本地缓存请求结果**

```jsx
function Child({ id }) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(false);

  useEffect(() => {
    // 若已有数据，直接返回（缓存生效）
    if (data?.id === id) return;

    const fetchData = async () => {
      setLoading(true);
      try {
        const res = await api.get([`/data/${id}`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.id.md));
        setData(res.data);
      } catch (err) {
        console.error(err);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [id, data]); // 依赖id和当前数据

  return <div>{data?.content}</div>;
}

```

**4\. 清理未完成的请求**

组件卸载或依赖项变化时，若前一次请求未完成，可能导致内存泄漏或错误。需在`useEffect`的清理函数中取消请求。

**示例：用 AbortController 取消请求**

```jsx
useEffect(() => {
  const controller = new AbortController(); // 创建控制器
  const signal = controller.signal;

  const fetchData = async () => {
    try {
      const res = await fetch([`/data/${id}`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.id.md), { signal }); // 关联信号
      const data = await res.json();
      setData(data);
    } catch (err) {
      if (err.name !== 'AbortError') { // 忽略主动取消的错误
        console.error(err);
      }
    }
  };

  fetchData();

  // 清理函数：取消未完成的请求
  return () => controller.abort();
}, [id]);

```

**总结**

解决步骤优先级：

1. 检查并优化`useEffect`的依赖项（核心原因）
2. 用`React.memo`+`useCallback`防止子组件无效重渲染
3. 缓存请求结果（减少重复请求）
4. 清理未完成的请求（避免副作用残留）

通过以上方法，可有效避免子组件因`useEffect`导致的重复渲染和请求问题。

### 什么是next.js它的最大得特点

Next.js 是一个基于 React 的**全栈框架**，由 Vercel 开发并维护，主要用于构建高性能的 Web 应用（包括网站、App、后端服务等）。它在 React 的基础上扩展了一系列核心功能，解决了 React 单页应用（SPA）在实际开发中面临的痛点（如 SEO 优化、首屏加载速度、路由配置等），同时提供了更简洁的开发体验。

**Next.js 最大的特点（核心优势）**

1. **灵活的渲染策略（最核心特点）**支持多种渲染方式，可根据场景灵活选择，解决了传统 React SPA 因客户端渲染（CSR）导致的 SEO 差、首屏加载慢等问题：  
   * **服务器端渲染（SSR，Server-Side Rendering）**：每次用户请求时，在服务器端动态生成 HTML 并返回，确保首屏内容可被搜索引擎抓取，且加载速度快。  
   * **静态站点生成（SSG，Static Site Generation）**：构建时预渲染 HTML 页面，部署后直接复用，性能最优（适合静态内容，如博客、文档）。  
   * **增量静态再生（ISR，Incremental Static Regeneration）**：结合 SSG 和动态内容优势，预渲染的页面可在后台定期更新，无需重新部署整个站点（适合电商商品页等需动态更新的静态内容）。  
   * **客户端渲染（CSR）**：保留 React 传统的客户端渲染能力，适合交互密集型页面。
2. **基于文件系统的路由**无需手动配置路由规则，通过**文件和文件夹结构自动生成路由**，大幅简化路由管理：  
   * 在 `pages` 或 `app` 目录下创建文件（如 `about.js`），自动对应路由 `/about`；  
   * 支持动态路由（如 [`[id].js`](https://xplanc.org/primers/document/zh/10.Bash/90.%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/EX.id.md) 对应 `/post/123`）、嵌套路由（通过文件夹层级）、路由拦截等高级功能。
3. **全栈开发能力**内置 **API 路由**，允许在同一项目中直接编写后端接口（无需单独搭建服务器）：  
   * 在 `pages/api` 或 `app/api` 目录下创建文件（如 `user.js`），自动成为接口 `/api/user`；  
   * 可直接操作数据库、处理请求逻辑，轻松实现前后端一体化开发。
4. **性能优化开箱即用**内置多种性能优化机制，无需手动配置：  
   * **自动代码分割**：按路由拆分代码，只加载当前页面所需资源；  
   * **图像优化**：通过 `next/image` 组件自动优化图片（压缩、懒加载、WebP 格式转换等）；  
   * **字体优化**：通过 [`next/font`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.font.md) 优化字体加载，避免布局偏移；  
   * **缓存机制**：支持客户端缓存、服务器缓存、CDN 缓存等多层级缓存策略。
5. **开发体验友好**  
   * 内置热模块替换（HMR），开发时修改代码实时更新，无需手动刷新；  
   * 支持 TypeScript 开箱即用，类型检查更便捷；  
   * 与 Vercel 平台深度集成，部署流程简单（也支持其他平台如 AWS、Netlify 等）。

**总结**

Next.js 最大的价值在于**将 React 的组件化开发与灵活的渲染策略、简化的路由管理、全栈能力结合**，既保留了 React 的开发体验，又解决了实际生产中的性能、SEO、部署等核心问题，是构建现代 Web 应用的主流框架之一（尤其适合需要兼顾性能、SEO 和开发效率的场景）。

因为这边有最大字符限制

完整版本：[前端梳理体系从常问问题去完善-框架篇（react生态）-CSDN博客](https://link.juejin.cn?target=https%3A%2F%2Fblog.csdn.net%2Fnihaio25%2Farticle%2Fdetails%2F152733736%3Fspm%3D1001.2014.3001.5501 "https://blog.csdn.net/nihaio25/article/details/152733736?spm=1001.2014.3001.5501")

## 相关内容

[写下自己求职记录也给正在求职得一些建议-CSDN博客](https://link.juejin.cn?target=https%3A%2F%2Fblog.csdn.net%2Fnihaio25%2Farticle%2Fdetails%2F151066919%3Fspm%3D1001.2014.3001.5501 "https://blog.csdn.net/nihaio25/article/details/151066919?spm=1001.2014.3001.5501")

[从初中级如何迈入中高级-其实技术只是“入门卷”-CSDN博客](https://link.juejin.cn?target=https%3A%2F%2Fblog.csdn.net%2Fnihaio25%2Farticle%2Fdetails%2F151332526%3Fspm%3D1001.2014.3001.5501 "https://blog.csdn.net/nihaio25/article/details/151332526?spm=1001.2014.3001.5501")

[前端梳理体系从常问问题去完善-基础篇（html,css,js,ts）-CSDN博客](https://link.juejin.cn?target=https%3A%2F%2Fblog.csdn.net%2Fnihaio25%2Farticle%2Fdetails%2F151689735%3Fspm%3D1001.2014.3001.5501 "https://blog.csdn.net/nihaio25/article/details/151689735?spm=1001.2014.3001.5501")

[前端梳理体系从常问问题去完善-工程篇（webpack,vite）\_前端系统梳理-CSDN博客](https://link.juejin.cn?target=https%3A%2F%2Fblog.csdn.net%2Fnihaio25%2Farticle%2Fdetails%2F151935486%3Fspm%3D1011.2415.3001.5331 "https://blog.csdn.net/nihaio25/article/details/151935486?spm=1011.2415.3001.5331")

---

> 《[前端梳理体系从常问问题去完善-框架篇（react生态)](https://xplanc.online/ad7c118d63f83ac7e51cd5f68d48bdb4b1fb5286fe2c3779e7b68336cee4f1d7)》 是转载文章，[点击查看原文](https://juejin.cn/post/7558320134252494882)。