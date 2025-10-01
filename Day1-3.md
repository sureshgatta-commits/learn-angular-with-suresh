

```markdown
# 📘 TypeScript & Angular Notes: String Interpolation & setInterval()

Author: Suresh  
Last Updated: October 1, 2025  
Tags: `TypeScript`, `Angular`, `Real-Time`, `Live Examples`

---

## 🎯 Overview

This guide covers two essential concepts for building dynamic Angular applications:

- **String Interpolation**: Displaying dynamic data in templates.
- **`setInterval()`**: Running code repeatedly at fixed time intervals.

Each section includes syntax, real-time examples, and common mistakes.

---

## 🧵 1. String Interpolation in Angular

### ✅ What Is It?

**String interpolation** lets you embed dynamic expressions inside your HTML templates using double curly braces `{{ }}`.

### 🔧 Syntax

```html
{{ expression }}
```

- `expression` can be a variable, method call, or calculation.
- It must be valid TypeScript and return a value.

---

### 🧪 Real-Time Examples

```ts
export class AppComponent {
  name: string = 'Suresh';
  salary: number = 500;

  getBonus(): number {
    return this.salary * 0.1;
  }
}
```

```html
<h1>Hello {{ name }}</h1>
<h2>Your salary is ₹{{ salary }}</h2>
<h3>Your bonus is ₹{{ getBonus() }}</h3>
```

---

### ❌ Common Mistakes

| Mistake | Why It Fails |
|--------|--------------|
| `{{ if (x > 5) }}` | Control structures not allowed |
| `{{ console.log(x) }}` | Side effects not allowed |
| `{{ someUndefinedVar }}` | Throws runtime error |

---

## ⏱️ 2. `setInterval()` in TypeScript

### ✅ What Is It?

`setInterval()` is a built-in JavaScript function that runs a block of code repeatedly after a fixed delay.

### 🔧 Syntax

```ts
setInterval(callbackFunction, delayInMilliseconds);
```

- `callbackFunction`: Function to run.
- `delayInMilliseconds`: Time between executions (e.g., `1000` = 1 second).

---

### 🧪 Real-Time Angular Example

```ts
export class AppComponent implements OnInit {
  time: string = new Date().toLocaleTimeString();

  ngOnInit() {
    setInterval(() => {
      this.time = new Date().toLocaleTimeString();
    }, 1000);
  }
}
```

```html
<h3>Current Time: {{ time }}</h3>
```

---

### 🛑 Stopping the Interval

```ts
const id = setInterval(() => {
  console.log("Tick");
}, 1000);

clearInterval(id); // Stops the interval
```

---

### ❌ Common Mistakes

| Mistake | Fix |
|--------|-----|
| `setInterval(() => x = x + 1, 1000)` outside method | Move it inside `ngOnInit()` |
| `if (x = 5)` | Use `===` for comparison |
| `z: number = 0;` inside method | Use `let z = 0;` instead |

---

## 🎯 Challenge: Build a Live Clock

```ts
export class ClockComponent implements OnInit {
  currentTime: string = '';

  ngOnInit() {
    setInterval(() => {
      this.currentTime = new Date().toLocaleTimeString();
    }, 1000);
  }
}
```

```html
<h2>🕒 {{ currentTime }}</h2>
```

---

## 🧠 Bonus: `const` vs `let`

| Use Case | Keyword |
|----------|---------|
| Value never changes | `const` |
| Value changes over time | `let` |
| Avoid in modern code | `var` |

---

## ✅ Summary

- Use `{{ }}` for clean, readable dynamic content.
- Use `setInterval()` inside lifecycle hooks like `ngOnInit()` for real-time updates.
- Avoid reserved names like `Number`, and always declare variables properly.

---

