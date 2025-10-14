

````markdown
# 🧠 @ViewChild vs @ViewChildren in Angular (Real-Time Notes)

---

## 📘 What They Are

| Decorator | Purpose |
|------------|----------|
| `@ViewChild()` | Gets a **single element** or **component** from the template. |
| `@ViewChildren()` | Gets **multiple elements** or **components** (as a list). |

---

## 🧩 1️⃣ `@ViewChild` — Accessing a **Single Element or Child Component**

### ✅ Syntax
```ts
@ViewChild('p1') p2!: ElementRef;
````

### ✅ Example

**HTML**

```html
<p #p1>Lorem, ipsum dolor.</p>
<button (click)="showDetails()">Change DOM</button>
```

**TypeScript**

```ts
import { Component, ViewChild, ElementRef } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent {
  @ViewChild('p1') p2!: ElementRef;

  showDetails() {
    this.p2.nativeElement.innerText = 'Suresh changed the DOM!';
    this.p2.nativeElement.style.color = 'red';
  }
}
```

### 💡 Real-Time Use

* Accessing a **single DOM element** like an input or paragraph.
* Accessing a **child component instance** (like a reusable component).
* Changing styles, text, or reading values.
* Focusing a specific element (`input.focus()`).

---

## 🧩 2️⃣ `@ViewChildren` — Accessing **Multiple Elements or Components**

### ✅ Syntax

```ts
@ViewChildren('pa2') para2!: QueryList<ElementRef>;
```

### ✅ Example

**HTML**

```html
<p #pa2>Paragraph 1</p>
<p #pa2>Paragraph 2</p>
<button (click)="showDetails()">Change All</button>
```

**TypeScript**

```ts
import { Component, ViewChildren, ElementRef, QueryList } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent {
  @ViewChildren('pa2') para2!: QueryList<ElementRef>;

  showDetails() {
    this.para2.forEach((p, index) => {
      p.nativeElement.innerText = `Paragraph ${index + 1} changed by Suresh!`;
      p.nativeElement.style.color = 'blue';
    });
  }
}
```

### 💡 Real-Time Use

* Looping over multiple DOM elements.
* Applying bulk changes (like styling all `<p>` tags).
* Accessing multiple child components (like multiple `app-card` components).
* Dynamically manipulating lists of elements.

---

## 🧩 3️⃣ Major Difference — Summary Table

| Feature        | `@ViewChild`                       | `@ViewChildren`                                   |
| -------------- | ---------------------------------- | ------------------------------------------------- |
| Accesses       | One element/component              | Multiple elements/components                      |
| Return Type    | `ElementRef` or Component instance | `QueryList<ElementRef>` or `QueryList<Component>` |
| Use Case       | When you know there’s only one     | When you have multiple with same ref              |
| Access Syntax  | `this.p2.nativeElement`            | `this.para2.forEach()`                            |
| Lifecycle Hook | `ngAfterViewInit()`                | `ngAfterViewInit()` or `ngAfterViewChecked()`     |
| Example        | One `<p #p1>`                      | Many `<p #pa2>`                                   |

---

## 🧩 4️⃣ Real-Time Example: Combining Both

**HTML**

```html
<p #p1>Single Paragraph</p>

<p #pa2>Paragraph 1</p>
<p #pa2>Paragraph 2</p>

<button (click)="showDetails()">Change DOM</button>
```

**TypeScript**

```ts
import { Component, ViewChild, ViewChildren, ElementRef, QueryList } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent {
  @ViewChild('p1') p2!: ElementRef;
  @ViewChildren('pa2') para2!: QueryList<ElementRef>;

  showDetails() {
    // Single element
    this.p2.nativeElement.innerText = 'Suresh changed single DOM element!';
    this.p2.nativeElement.style.color = 'red';

    // Multiple elements
    this.para2.forEach((el, i) => {
      el.nativeElement.innerText = `Suresh changed para ${i + 1}`;
      el.nativeElement.style.fontWeight = 'bold';
    });

    console.log('Single:', this.p2);
    console.log('Multiple:', this.para2);
  }
}
```

---

## ⚙️ 5️⃣ Real-World Use Cases

| Scenario                                    | Use             | Example                                     |
| ------------------------------------------- | --------------- | ------------------------------------------- |
| Focus a single input field after page loads | `@ViewChild`    | `this.username.nativeElement.focus()`       |
| Change all form input borders on error      | `@ViewChildren` | Loop over `QueryList` of inputs             |
| Access a single child component             | `@ViewChild`    | `@ViewChild(ChildComponent) child;`         |
| Call method on multiple child components    | `@ViewChildren` | `this.cards.forEach(c => c.refreshData());` |

---

## 🧭 6️⃣ Important Tip: `QueryList` in `@ViewChildren`

`@ViewChildren` returns a **QueryList**, which is like an Angular-managed array.

You can:

```ts
this.para2.forEach(p => console.log(p.nativeElement));
```

Or even listen for changes:

```ts
this.para2.changes.subscribe(() => console.log('List updated!'));
```

---

## ✅ Summary

| Concept       | `@ViewChild`              | `@ViewChildren`                              |
| ------------- | ------------------------- | -------------------------------------------- |
| Purpose       | Single DOM or Component   | Multiple DOMs or Components                  |
| Returns       | ElementRef / Component    | QueryList<ElementRef> / QueryList<Component> |
| Use Hook      | ngAfterViewInit()         | ngAfterViewInit() / ngAfterViewChecked()     |
| Access Type   | Direct object             | Iterable list                                |
| Real-time Use | Focus, one element access | Style or update many elements                |
| Example       | Form field focus          | Highlight multiple rows                      |

---

## 🧠 TL;DR

> * Use **`@ViewChild`** when you want **one element** (or component).
> * Use **`@ViewChildren`** when you want **all elements** with the same reference variable.
> * Access them only **after the view initializes (ngAfterViewInit)**.

```

---

