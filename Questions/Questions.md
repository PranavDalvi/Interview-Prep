***
## React (Version: 18 and 19)
1. **What is useMemo**
	- `useMemo` is a React Hook used to **memoize the result of an expensive computation** so that it is **recomputed only when its dependencies change**.
	```const memoizedValue = useMemo(() => expensiveFn(a, b), [a, b]);```
	- **Why it exists:**
		- Prevents unnecessary recalculations    
		- Optimizes performance
		- Does **not** prevent re-renders, only recomputation
	- **Key clarification (interview trap):**
		- > `useMemo` is a **performance optimization**, not a correctness tool.
		
2. **what is useCallback**
	- `useCallback` memoizes a **function reference** so that the same function instance is reused unless dependencies change.
	``` javascript
	const handleClick = useCallback(() => {
		  doSomething(id);
	}, [id]);
	```
	- **Why it exists:**
		- Prevents unnecessary re-renders of child components
		- Especially useful with `React.memo`
	- **Difference vs useMemo (must say this):**
		- `useMemo` → memoizes **values**
		- `useCallback` → memoizes **functions**

3. **Define stages of react life cycle**
	- React lifecycle has **three main phases**:
		1. **Mounting** – component is created and inserted into DOM
		2. **Updating** – state or props change
		3.  **Unmounting** – component is removed from DOM
	- In **functional components**, lifecycle behavior is handled using `useEffect`.
	```javascript
	useEffect(() => {
		// componentDidMount + componentDidUpdate
		return () => {
			// componentWillUnmount
		  };
	}, [deps]);
	```
	
4. **Define Hooks**
	- Hooks are **functions introduced in React 16.8** that allow functional components to:
		- Manage state
		- Handle lifecycle
		- Access React features **without classes**
	- Rules of Hooks (interview MUST):
		1. Call hooks at the **top level**
		2. Call hooks **only inside React functions**
	
5. **What is useRef Hook**
	- Persist mutable values across renders **without causing re-renders**
	- Access DOM elements directly
	```javascript
	const inputRef = useRef(null);	
	```
	- **Key distinction (important):**
		- Updating `ref.current` **does not trigger re-render**
		- Unlike `useState`
	
6. **What are functional components and non-functional components in react**
	- **Functional components** are plain JS functions that return JSX
	- **Non-functional components** generally refer to **class components**

7. **What is class components and functional component in react**

| Properties           | Class Component   | Functional Component |
| -------------------- | ----------------- | -------------------- |
| State management     | Uses `this.state` | Uses hooks           |
| Lifecycle management | Lifecycle methods | `useEffect`          |
| Code length          | More boilerplate  | Cleaner, concise     |
| style                | Legacy pattern    | Modern standard      |
	- **Interview signal line:**
		- React is moving towards **functional components + hooks** as the primary paradigm.

8. **What is props drilling and how to prevent it**
	- Props drilling is passing props through multiple intermediate components that **don’t need the data**, just to reach a deeply nested component.
	- **Problems:**
		- Tight coupling
		- Hard to maintain
		- Poor scalability
	- **Solutions:**
		- React Context API 
		- State management libraries (Redux, Zustand)
		- Component composition
9. **what is promise and observables?**
	1. A **Promise** represents a **single asynchronous value** that will either:
	- resolve (success)
	- reject (failure)
	- It is **eager** — execution starts immediately when the promise is created.
	```javascript
	const p = new Promise((resolve, reject) => {
	  resolve(42);
	});
	```
	**Key properties:**
	- Emits **only one value**
	- Cannot be cancelled
	- Once settled, state is immutable

	2. An **Observable** represents a **stream of asynchronous values over time**.  
	- It is **lazy** — execution starts only when someone subscribes.
	```javascript
	observable.subscribe(value => console.log(value));
	```
	**Key properties:**
	- Can emit **multiple values**
	- Can be cancelled (unsubscribe)
	- Supports operators like `map`, `filter`, `retry`
    Commonly used with **RxJS** and **Angular**.
    
    ## Promise vs Observable (must know table)

| Feature      | Promise          | Observable             |
| ------------ | ---------------- | ---------------------- |
| Values       | Single           | Multiple               |
| Execution    | Eager            | Lazy                   |
| Cancellation | ❌ No             | ✅ Yes                  |
| Operators    | Limited (`then`) | Rich (`map`, `filter`) |
| Use case     | One-time async   | Streams / events       |
## Real-world usage (this scores points)
### Use Promise when:
- HTTP request returning one response
- DB query
- File read
### Use Observable when:
- WebSocket data
- User events
- Live data streams
- Retry / cancel / debounce scenarios
***
## Backend
1. **When to use PUT and when to use PATCH HTTP**

| PUT                      | PATCH                     |
| ------------------------ | ------------------------- |
| Replaces entire resource | Updates partial resource  |
| Idempotent               | Usually idempotent        |
| Requires full payload    | Sends only changed fields |
	- **Example:**
		- PUT → replace user object
		- PATCH → update only email
	- **Interview line:**
		- Use PUT when client controls full resource state; PATCH for partial updates.
***

***
## Django
1. **What is serialization in django?**
	- Serialization converts complex Django objects (QuerySets, Models) into formats like:
		- JSON, XML
	- Used in:
		- APIs, Data exchange
	- Django Rest Framework provides serializers to:
		- Validate input, Transform output.

2. **How to create custom middleware in django**
	- Create a middleware class with `__init__` and `__call__`.
```python
class CustomMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        response = self.get_response(request)
        return response

```
***
## SQL
1. **In SQL how to get the second highest age**
```sql
SELECT MAX(age)
FROM users
WHERE age < (SELECT MAX(age) FROM users);
```
- **Alternative (better for duplicates):**
```sql
SELECT DISTINCT age
FROM users
ORDER BY age DESC
LIMIT 1 OFFSET 1;
```
***
## JavaScript
1. **Is arr1 = [] and arr2 = [] is equal in javascript similarly what about obj1 = {} and obj2 = {}**
	- No. Arrays and objects are compared **by reference**, not value.
	```javascript
	[] === []      // false
	{} === {}      // false
	```
	-   Each literal creates a new memory reference.
***
## HTML
1. **Is HTML stateless or stateful.**
	- HTML is **stateless**.
	- It does not remember previous interactions
	- State is managed via: JavaScript, Cookies, LocalStorage, Sessions (server-side)
    **Interview clarity:** HTML only defines structure; state lives outside it.
***