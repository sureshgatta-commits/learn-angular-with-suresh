
# 🌿 Structural Directives in Angular 13 — Real-Time Examples

## 🧩 What are Structural Directives?

**Structural directives** are Angular directives that **change the structure of the DOM** — they can **add, remove, or modify elements** dynamically based on conditions or data.

They always start with an asterisk (`*`) and are used in templates like this:

```html
<p *ngIf="condition">Hello!</p>
```

Angular provides three built-in structural directives:

1. `*ngIf` — Conditional rendering
2. `*ngFor` — Looping over lists
3. `*ngSwitch` — Multiple condition checks

---

## 🌱 1. `*ngIf` — Conditional Rendering

### ✅ Example

```html
<button id="btn" (click)="onShowButton()">
  {{ show ? 'Hide text' : 'Show text' }}
</button>

<p *ngIf="show">
  Lorem ipsum dolor sit amet consectetur, adipisicing elit...
</p>
```

### 💡 Explanation

* The `<p>` tag only renders if `show` is `true`.
* The button toggles the `show` property in the component:

  ```ts
  show: boolean = false;
  onShowButton() {
    this.show = !this.show;
  }
  ```

### 🧠 Real-Time Use

Show or hide a message, card, or popup dynamically — e.g., “Show more” or “Hide details” toggles.

---

## ⚡ `*ngIf` with `then` and `else`

### Example:

```html
<p *ngIf="isLoggedIn; then loggedin; else bye"></p>

<ng-template #loggedin>
  <h1>Thank you for logging in</h1>
</ng-template>

<ng-template #bye>
  <h1>Good Bye!</h1>
</ng-template>
```

### 💡 Explanation

* `isLoggedIn` is a boolean variable in the component.
* `then` and `else` reference two templates using **template reference variables** (`#loggedin` and `#bye`).
* Depending on `isLoggedIn`, Angular displays one template or the other.

### 🧠 Real-Time Use

Show different views for logged-in vs. logged-out users.

---

## 🧾 2. `*ngFor` — Looping Through Data

### Example:

```html
<table border="1px">
  <th>Fruit Name</th>
  <th>Even</th>
  <th>Odd</th>
  <th>Index</th>

  <tr *ngFor="let fruit of fruits; index as i; even as e; odd as o">
    <td>{{ fruit }}</td>
    <td>{{ e }}</td>
    <td>{{ o }}</td>
    <td>{{ i + 1 }}</td>
  </tr>
</table>
```

### 💡 Explanation

* Iterates through the array `fruits: string[] = ['Apple', 'Mango', 'Guava'];`
* Angular automatically provides local variables:

  * `index` — current index (starts at 0)
  * `even` — `true` for even rows (0, 2, 4, …)
  * `odd` — `true` for odd rows (1, 3, 5, …)

| Fruit | Index | Even | Odd |
| ----- | ----- | ---- | --- |
| Apple | 0     | ✅    | ❌   |
| Mango | 1     | ❌    | ✅   |
| Guava | 2     | ✅    | ❌   |

### 🧠 Real-Time Use

Rendering lists, tables, menus, dropdowns, etc.

---

## 🔄 3. `*ngSwitch` — Multiple Condition Rendering

### Correct Example:

```html
<ng-container [ngSwitch]="value">
  <h1 *ngSwitchCase="10">You Entered 10</h1>
  <h1 *ngSwitchCase="20">You Entered 20</h1>
  <h2 *ngSwitchDefault>This is a default value</h2>
</ng-container>
```

### Component:

```ts
value: number = 10;
```

### 💡 Explanation

* `[ngSwitch]="value"` evaluates the expression.
* `*ngSwitchCase="10"` → renders if `value === 10`.
* `*ngSwitchCase="20"` → renders if `value === 20`.
* `*ngSwitchDefault` → renders if no case matches.

### 🧠 Real-Time Use

Display different content based on user selection, roles, or numeric status codes.

---

## 🧱 4. `ng-container`

### Definition:

`<ng-container>` is an **invisible logical wrapper** that **doesn’t appear in the DOM**.
It’s used to group or control elements **without adding extra HTML tags**.

### Example:

```html
<ng-container *ngIf="isLoggedIn; then loggedin; else bye"></ng-container>
```

✅ Angular will switch templates dynamically,
🚫 but no `<ng-container>` tag will appear in the browser’s HTML.

### 🧠 Real-Time Use

Use `ng-container` when:

* You want to apply `*ngIf` or `*ngFor` without creating unnecessary `<div>` elements.
* You’re switching between templates or grouping multiple child elements under one condition.

---

## 🧩 5. `ng-template`

### Definition:

`<ng-template>` defines a **block of HTML that is not rendered by default**.
Angular renders it **only when explicitly referenced** (like with `then` / `else`).

### Example:

```html
<ng-template #loggedin>
  <h1>Thank you for logging in</h1>
</ng-template>
```

This template stays hidden until Angular explicitly uses it (via `*ngIf` or `ViewContainerRef`).

### 🧠 Real-Time Use

Reusable message blocks, skeletons, or alternate layouts.

---

## 🏷️ 6. Template Reference Variable

### Definition:

A **template reference variable** is declared with `#` and used to **refer to an element or template** in the same template file.

### Example:

```html
<ng-template #bye>
  <h1>Good Bye!</h1>
</ng-template>
```

Here, `#bye` is a template reference variable — it’s referenced in:

```html
<p *ngIf="isLoggedIn; then loggedin; else bye"></p>
```

### 🧠 Real-Time Use

Access DOM elements, directives, or templates dynamically in the same component.

---

## ⚙️ Summary Table

| Directive                     | Purpose                          | Example                                      |
| ----------------------------- | -------------------------------- | -------------------------------------------- |
| `*ngIf`                       | Conditionally render element     | `<p *ngIf="show">Hello</p>`                  |
| `*ngIf ... then ... else ...` | Show alternate templates         | `<p *ngIf="isLoggedIn; then a; else b"></p>` |
| `*ngFor`                      | Loop through array items         | `<tr *ngFor="let f of fruits">{{f}}</tr>`    |
| `*ngSwitch`                   | Multiple condition rendering     | `<div [ngSwitch]="value">...</div>`          |
| `ng-container`                | Invisible logical wrapper        | `<ng-container *ngIf="true"></ng-container>` |
| `ng-template`                 | Hidden reusable template block   | `<ng-template #block>...</ng-template>`      |
| Template ref var (`#`)        | Reference for elements/templates | `<ng-template #t></ng-template>`             |

---

## 🧠 Real-Time Summary

In your app:

* The **Show/Hide** button uses `*ngIf` for conditional visibility.
* The **table** uses `*ngFor` for looping with even/odd rows.
* The **login templates** use `*ngIf` with `then`/`else` and `ng-template`.
* The **switch block** uses `ngSwitch` to handle multiple values.
* `ng-container` helps avoid unwanted wrapper elements.
* Template reference variables (`#loggedin`, `#bye`) connect `*ngIf` to `<ng-template>` blocks.

All of these combine to create a **dynamic, real-time Angular UI**.

---

Would you like me to save this as a Markdown file (e.g. `structural-directives-notes.md`) for you?
