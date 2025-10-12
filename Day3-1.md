
# 🌀 Two-Way Data Binding in Angular

## 📘 Overview
Two-way data binding in Angular creates a **synchronization** between the **view (template)** and the **component (TypeScript code)**.  
This means:
- When the **user updates the view**, the **model (data)** is updated automatically.
- When the **model changes**, the **view** reflects those changes instantly.

In simple terms, it keeps both the **UI** and the **data** in sync.

---

## 🧩 Syntax
Angular provides the **`[(ngModel)]`** directive for two-way data binding.

```html
<input [(ngModel)]="propertyName" />
````

This is a combination of:

* **Property binding** → `[ngModel]="propertyName"`
* **Event binding** → `(ngModelChange)="propertyName = $event"`

So the shorthand:

```html
[(ngModel)]="propertyName"
```

is equivalent to:

```html
[ngModel]="propertyName" (ngModelChange)="propertyName = $event"
```

---

## ⚙️ Setup

To use `ngModel`, you need to import the `FormsModule`.

### Step 1: Import `FormsModule`

In your `app.module.ts` file:

```typescript
import { FormsModule } from '@angular/forms';
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, FormsModule],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

### Step 2: Use `[(ngModel)]` in your component template

```html
<!-- app.component.html -->
<h2>Two-Way Binding Example</h2>
<input [(ngModel)]="username" placeholder="Enter your name" />
<p>Hello, {{ username }}!</p>
```

### Step 3: Define the property in your component

```typescript
// app.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent {
  username: string = '';
}
```

---

## 🧠 How It Works

| Type                 | Syntax               | Direction        | Description                            |
| -------------------- | -------------------- | ---------------- | -------------------------------------- |
| **Property Binding** | `[property]="data"`  | Component → View | Passes data from component to template |
| **Event Binding**    | `(event)="handler"`  | View → Component | Sends event data to the component      |
| **Two-Way Binding**  | `[(ngModel)]="data"` | Both             | Keeps data in sync both ways           |

---

## 🧪 Example in Action

```html
<!-- two-way-binding.component.html -->
<div>
  <h3>Live Text Preview</h3>
  <input [(ngModel)]="message" placeholder="Type something..." />
  <p>You typed: {{ message }}</p>
</div>
```

```typescript
// two-way-binding.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-two-way-binding',
  templateUrl: './two-way-binding.component.html'
})
export class TwoWayBindingComponent {
  message: string = '';
}
```

---

## ⚠️ Notes

* `[(ngModel)]` works only with **template-driven forms**, not **reactive forms**.
* The `FormsModule` must be imported in any module that uses `ngModel`.
* Useful for **simple forms**, **input fields**, or **quick data updates**.

---

## 🚀 Summary

| Concept             | Description                              |
| ------------------- | ---------------------------------------- |
| **Directive**       | `ngModel`                                |
| **Binding Type**    | Two-way data binding                     |
| **Required Module** | `FormsModule`                            |
| **Use Case**        | Synchronize UI input with component data |

---


