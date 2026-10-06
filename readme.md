# JavaScript Execution Order Assignment

## Question

Predict the exact output and explain the execution order:

```javascript
console.log("A");

setTimeout(() => console.log("B"), 0);

Promise.resolve().then(() => console.log("C"));

console.log("D");
```

## Exact Output

```text
A
D
C
B
```

## Explanation

The JavaScript code executes in the following order:

### 1. `console.log("A")`

This is synchronous code, so it executes immediately.

Output:

```text
A
```

### 2. `setTimeout()`

The `setTimeout` callback is sent to the task/macrotask queue. Even though the delay is `0`, it does not execute immediately.

### 3. `Promise.resolve().then()`

The Promise callback is placed in the microtask queue.

### 4. `console.log("D")`

This is also synchronous code, so it executes immediately.

Output:

```text
D
```

After all synchronous code finishes, JavaScript executes the microtask queue before the task queue.

### 5. Promise callback

The Promise callback executes and prints:

```text
C
```

### 6. Timer callback

Finally, the `setTimeout` callback executes and prints:

```text
B
```

## Execution Order

1. `console.log("A")` → **A**
2. `setTimeout()` → waits in the task queue
3. `Promise.then()` → goes to the microtask queue
4. `console.log("D")` → **D**
5. Promise callback → **C**
6. Timer callback → **B**

## Final Answer

```text
A
D
C
B
```

## Key Concept

**Synchronous Code → Microtasks (Promises) → Tasks/Macrotasks (`setTimeout`)**
