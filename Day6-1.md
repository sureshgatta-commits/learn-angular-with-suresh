
````markdown
# Angular Structural & Content Projection Practice  
**Concepts Covered:**  
- `ng-content` (Content Projection)  
- `ng-container`  
- `ng-template`  
- `*ngIf` and `*ngFor`  

---

## 🧩 Real-Time Scenario
Imagine a **Dashboard Component** (`AppComponent`) that uses a reusable **Card Component** (`HelloComponent`).  
Each card displays:
- A projected greeting (`ng-content`)
- A dynamic list of `clients` or `employees`
- Conditional rendering of numbers and templates.

---

## 📁 File: `app.component.ts`
```typescript
import { Component, VERSION } from '@angular/core';

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent  {
  name = 'Angular ' + VERSION.major;

  client = ["Client1", "Client2", "Client3"];
  employees = ["Employee1", "Employee2", "Employee3"];
}
````

### 🔍 Explanation:

* `name` → Passed to the child component.
* `client` and `employees` → Two different datasets to be displayed using the same child component.

---

## 📁 File: `hello.component.ts`

```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'hello',
  template: `
    <!-- Selective Content Projection -->
    <ng-content select=".Suri"></ng-content>
    <ng-content select="#Swathi"></ng-content>
    <ng-content></ng-content>

    <!-- Dynamic Data from Parent -->
    <h1>Hello {{ name }}!</h1>

    <ul>
      <li *ngFor="let e of values">{{ e }}</li>
    </ul>
  `,
  styles: [`h1 { font-family: Lato; }`]
})
export class HelloComponent  {
  @Input() name: string;
  @Input() values: string[];
}
```

### 🔍 Explanation:

* **`ng-content`** → Projects HTML content from the parent (`app.component.html`) into specific locations inside the child.

  * `select=".Suri"` → Projects elements with class `Suri`.
  * `select="#Swathi"` → Projects elements with id `Swathi`.
* **`*ngFor`** → Dynamically loops through `values` from the parent.

---

## 📁 File: `app.component.html`

```html
<!-- First Hello Component (Client Section) -->
<hello [name]="name" [values]="client">
  <h1 class="Suri">Hi, Suresh!</h1>
  <h1 id="Swathi">Hi, Swathi!</h1>
</hello>

<!-- Second Hello Component (Employee Section) -->
<hello [values]="employees">
  <h1 class="Suri">Hi, Suresh!</h1>
  <h1 id="Swathi">Hi, Swathi!</h1>
</hello>

<hr>

<!-- Example: *ngFor with *ngIf -->
<div *ngFor="let num of [10, 20, 30, 31]">
  <div *ngIf="num % 2 === 0">
    {{ num }}
  </div>
</div>

<!-- Example: ng-container with *ngFor -->
<ng-container *ngFor="let num of [10, 20, 30, 31]">
  <br>
  {{ num }}
</ng-container>

<hr>

<!-- Example: ng-template with else block -->
<ng-template #grt>
  Hello, Gym freak!
</ng-template>

<ng-container *ngIf="false; else grt">
</ng-container>
```

---

## 💬 Real-Time Explanation

### 🔹 `ng-content` — *Content Projection (Reusable UI)*

Used when a **parent component** needs to pass custom HTML content into a **child component**.

**Example:**
The `HelloComponent` is like a **dynamic card** that can show different greetings and lists depending on parent input.

---

### 🔹 `ng-container` — *Invisible Wrapper*

* It does **not render** any actual HTML element in the DOM.
* Commonly used with structural directives like `*ngIf` or `*ngFor` when you don’t want to create extra `<div>`s.

**Real-world use:**
When looping over data or conditionally displaying UI without disturbing layout structure.

---

### 🔹 `ng-template` — *Deferred or Conditional Content*

* Defines a block of HTML that is **not rendered by default**.
* Displayed conditionally using `*ngIf ... else templateRef`.

**Real-world use:**
Used for fallback messages, loaders, or alternate UIs when data is missing.

---

## ⚙️ Output Snapshot

✅ **Rendered Output When `*ngIf="false; else grt"`**

```
Hi, Suresh!
Hi, Swathi!
Hello Angular 17!
Client1
Client2
Client3
Hi, Suresh!
Hi, Swathi!
Hello !
Employee1
Employee2
Employee3
10
20
30
10
20
30
31
Hello, Gym freak!
```

---

## 🧠 Summary Table

| Directive / Concept | Purpose                                   | Real-time Use                                      |
| ------------------- | ----------------------------------------- | -------------------------------------------------- |
| `ng-content`        | Projects parent HTML into child component | Reusable, flexible UI components                   |
| `ng-container`      | Logical grouping without extra DOM nodes  | Conditional/loop rendering without `<div>` clutter |
| `ng-template`       | Defines hidden markup to be shown later   | Alternate templates (error, loading, empty state)  |
| `*ngIf`, `*ngFor`   | Structural directives                     | Conditional display and iteration                  |

---

### 🚀 Author Notes

This example simulates a **client–employee dashboard** that demonstrates reusable component design, conditional rendering, and template projection — all essential for **real-world Angular projects**.

```

---


