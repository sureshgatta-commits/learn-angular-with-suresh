

````markdown
# 🌟 Pipes and Custom Pipes in Angular 13 — Real-Time Notes

## 🔹 What are Pipes in Angular?

**Pipes** in Angular are used to **transform data** directly in the template.  
They help you display data in a **user-friendly** or **formatted** way **without changing the actual data in the component**.

Pipes are **pure functions** that take input data, process it, and return a transformed output.

---

## 🔹 Syntax

```html
{{ data | pipeName }}
````

You can also chain multiple pipes:

```html
{{ data | pipe1 | pipe2 }}
```

You can even pass **arguments**:

```html
{{ dateValue | date:'short' }}
```

---

## 🔹 Built-in Pipes in Angular

Angular provides several **built-in pipes** out of the box.

| Pipe Name         | Purpose                               | Example   | Output              |                          |
| ----------------- | ------------------------------------- | --------- | ------------------- | ------------------------ |
| **DatePipe**      | Formats date values                   | `{{ today | date:'fullDate' }}` | Monday, October 13, 2025 |
| **UpperCasePipe** | Converts text to uppercase            | `{{ name  | uppercase }}`       | JOHN                     |
| **LowerCasePipe** | Converts text to lowercase            | `{{ name  | lowercase }}`       | john                     |
| **TitleCasePipe** | Capitalizes each word                 | `{{ title | titlecase }}`       | Angular Basics           |
| **CurrencyPipe**  | Formats numbers as currency           | `{{ price | currency:'USD' }}`  | $50.00                   |
| **DecimalPipe**   | Formats decimal numbers               | `{{ value | number:'1.2-2' }}`  | 3.14                     |
| **PercentPipe**   | Converts number to percentage         | `{{ marks | percent }}`         | 85%                      |
| **JsonPipe**      | Displays object data as JSON          | `{{ data  | json }}`            | `{ "name": "Suresh" }`   |
| **SlicePipe**     | Extracts a portion of an array/string | `{{ text  | slice:0:5 }}`       | Hello                    |

---

## 🔹 Real-Time Example: Displaying Data Nicely

### ✅ Component (TypeScript)

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-pipe-demo',
  templateUrl: './pipe-demo.component.html'
})
export class PipeDemoComponent {
  name = 'gatta suresh';
  salary = 45000;
  joinedDate = new Date(2022, 10, 15);
}
```

### ✅ Template (HTML)

```html
<h2>Employee Details</h2>
<p><strong>Name:</strong> {{ name | titlecase }}</p>
<p><strong>Salary:</strong> {{ salary | currency:'INR' }}</p>
<p><strong>Joined On:</strong> {{ joinedDate | date:'fullDate' }}</p>
```

🧠 **Real-time output:**

```
Employee Details
Name: Gatta Suresh
Salary: ₹45,000.00
Joined On: Tuesday, November 15, 2022
```

✅ Pipes make the data instantly formatted for users without needing extra logic in your component.

---

## 🔹 Chaining Multiple Pipes

You can use multiple pipes together:

```html
<p>{{ name | uppercase | slice:0:5 }}</p>
```

👉 Converts to uppercase and then slices the first five letters.

---

## 🔹 Using Parameters in Pipes

```html
<p>{{ salary | currency:'USD':'symbol-narrow':'1.2-2' }}</p>
```

* `'USD'` → Currency code
* `'symbol-narrow'` → Symbol display format
* `'1.2-2'` → Minimum 2 decimal digits, maximum 2

🧩 Output: `$45,000.00`

---

## 🔹 Custom Pipes in Angular

Sometimes built-in pipes aren’t enough — you can create **custom pipes** to fit real business needs.

Example: Suppose you want to **convert names to masked email usernames** for privacy.

---

### ✅ Step 1: Create a Custom Pipe

In the terminal:

```bash
ng generate pipe mask-email
```

---

### ✅ Step 2: Implement Logic

```ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'maskEmail'
})
export class MaskEmailPipe implements PipeTransform {
  transform(value: string): string {
    if (!value) return '';

    const [user, domain] = value.split('@');
    const maskedUser = user[0] + '****' + user.slice(-1);
    return `${maskedUser}@${domain}`;
  }
}
```

---

### ✅ Step 3: Use It in Template

```html
<p>Original Email: {{ 'gatta.suresh@gmail.com' }}</p>
<p>Masked Email: {{ 'gatta.suresh@gmail.com' | maskEmail }}</p>
```

🧠 **Output:**

```
Original Email: gatta.suresh@gmail.com
Masked Email: g****h@gmail.com
```

---

## 🔹 Real-Time Custom Pipe Example 2: Filtering Data

Let’s create a pipe that filters a list of users by name.

### ✅ Pipe: `filter.pipe.ts`

```ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'filter'
})
export class FilterPipe implements PipeTransform {
  transform(items: any[], searchText: string): any[] {
    if (!items || !searchText) return items;
    return items.filter(item =>
      item.name.toLowerCase().includes(searchText.toLowerCase())
    );
  }
}
```

---

### ✅ Template

```html
<input type="text" placeholder="Search user" [(ngModel)]="searchText">

<ul>
  <li *ngFor="let user of users | filter:searchText">
    {{ user.name }}
  </li>
</ul>
```

### ✅ Component

```ts
export class UserListComponent {
  searchText = '';
  users = [
    { name: 'Suresh' },
    { name: 'Ravi' },
    { name: 'John' },
    { name: 'Anita' }
  ];
}
```

🧠 **Real-Time Behavior:**

* As the user types, the list **filters instantly** based on the input — a great real-time user experience.

---

## 🔹 Pure and Impure Pipes

Angular differentiates pipes based on **how often they are executed** and **when they are triggered**.

---

### ✅ Pure Pipes (Default)

A **pure pipe** runs **only when the input data changes** (by reference).

* ✅ **Default behavior** for all pipes
* ✅ **High performance**
* 🚫 Does **not** detect changes inside objects or arrays unless the reference changes

#### Example

```ts
@Pipe({
  name: 'filter',
  pure: true
})
export class FilterPipe implements PipeTransform {
  transform(items: any[], searchText: string): any[] {
    if (!items || !searchText) return items;
    return items.filter(item =>
      item.name.toLowerCase().includes(searchText.toLowerCase())
    );
  }
}
```

🧠 **Real-time behavior:**

* The pipe runs only when `searchText` or `items` **reference** changes.
* If you modify an existing array (like pushing new elements), the pipe won’t re-run unless a new array is assigned.

#### ✅ Example in Action

```ts
this.users.push({ name: 'New User' }); // Won’t trigger pure pipe
this.users = [...this.users]; // ✅ Will trigger pipe (new reference)
```

---

### ⚠️ Impure Pipes

An **impure pipe** runs **on every change detection cycle**, regardless of data reference change.

* ⚡ Runs very frequently (even for minor DOM updates)
* ⚠️ Can affect performance if used incorrectly
* ✅ Use only when working with **mutable data structures** or **frequent updates**

#### Example

```ts
@Pipe({
  name: 'filter',
  pure: false
})
export class FilterPipe implements PipeTransform {
  transform(items: any[], searchText: string): any[] {
    if (!items || !searchText) return items;
    return items.filter(item =>
      item.name.toLowerCase().includes(searchText.toLowerCase())
    );
  }
}
```

🧠 **Real-time behavior:**

* The pipe executes every time change detection runs (e.g., keypress, mouse move, etc.).
* Ideal for **real-time search filters**, **live dashboards**, or **mutable arrays** that change frequently.

---

### 🧩 Real-Time Comparison

| Feature          | Pure Pipe                          | Impure Pipe                            |
| ---------------- | ---------------------------------- | -------------------------------------- |
| Execution        | Only when input reference changes  | On every change detection              |
| Performance      | ✅ Fast                             | ⚠️ Slower                              |
| Suitable For     | Static / Immutable data            | Mutable / Dynamic data                 |
| Example Use Case | Format date, currency              | Real-time filtering, dashboard updates |
| Declaration      | `@Pipe({ name: 'x', pure: true })` | `@Pipe({ name: 'x', pure: false })`    |

---

### ✅ Real-Time Use Case

Let’s imagine you are building a **real-time dashboard** that updates every second:

```html
<ul>
  <li *ngFor="let stock of stocks | liveUpdate"></li>
</ul>
```

If your `stocks` array is **mutated** frequently (like stock prices updating per second), you’d need an **impure pipe** to re-render the values instantly.

---

## 🔹 Declaring Custom Pipes

All custom pipes must be declared in the `@NgModule` (inside `declarations`):

```ts
@NgModule({
  declarations: [
    AppComponent,
    MaskEmailPipe,
    FilterPipe
  ],
  ...
})
export class AppModule { }
```

---

## ✅ Summary

| Type               | Example                  | Use Case                            |                                             |                                  |
| ------------------ | ------------------------ | ----------------------------------- | ------------------------------------------- | -------------------------------- |
| Built-in Pipe      | `{{ price                | currency:'INR' }}`                  | Format standard data (date, currency, etc.) |                                  |
| Custom Pipe        | `{{ email                | maskEmail }}`                       | Apply business-specific formatting          |                                  |
| Pure Pipe          | `@Pipe({ pure: true })`  | Immutable or rarely changing data   |                                             |                                  |
| Impure Pipe        | `@Pipe({ pure: false })` | Mutable or frequently changing data |                                             |                                  |
| Chained Pipe       | `{{ name                 | titlecase                           | slice:0:5 }}`                               | Combine multiple transformations |
| Parameterized Pipe | `{{ date                 | date:'short' }}`                    | Customize output format                     |                                  |

---

## 🧘 Real-Time Insight

In Angular 13:

* Pipes are **lightweight, reusable transformation tools**.
* Use **pure pipes** for performance and stability.
* Use **impure pipes** only for **real-time dynamic data** (e.g., live search, dashboards).
* Always prefer **immutable data updates** with pure pipes for scalable apps.

---

**📘 Author’s Note:**
Understanding the difference between pure and impure pipes helps you write **efficient**, **real-time**, and **performance-optimized** Angular applications.
Choose wisely depending on whether your data is **static or dynamic**.

---

```


```
