

````markdown
# 🧩 Template-Driven Forms in Angular

## 📘 Introduction

Template-driven forms are one of the two approaches provided by Angular to handle forms (the other is **Reactive Forms**).  
They are mainly used for **simple forms** where much of the logic and form structure is handled directly in the **HTML template**, and Angular automatically manages the underlying form model.

---

## 🧠 Key Concepts & Definitions

| Concept | Description |
|----------|--------------|
| **NgForm** | A directive that Angular automatically attaches to `<form>` elements to create a form object. It provides properties like `value`, `valid`, and `controls`. |
| **ngModel** | Used for **two-way data binding** between the form field and the component class property. It keeps the UI and data in sync. |
| **name Attribute** | Mandatory for every form control when using `ngModel`. It is used to register the control with the parent `NgForm`. |
| **#templateRef (Template Reference Variable)** | Used to access form control or form instance in the template. Example: `#loginForm="ngForm"` or `#username="ngModel"`. |
| **ngModelGroup** | Groups multiple form controls under one logical name to manage complex forms. |
| **Validation** | Angular provides built-in validators like `required`, `minlength`, `maxlength`, `email`, and also supports custom validation. |

---

## 🧩 Example: Simple Login Form

```html
<form #loginform="ngForm" (ngSubmit)="submit(loginform)">
  <input type="text" ngModel name="username" required minlength="4" #un="ngModel" placeholder="Username">
  <div *ngIf="un.touched && un.invalid">
    <p *ngIf="un.errors?.['required']">Username is required</p>
    <p *ngIf="un.errors?.['minlength']">Minimum 4 characters required</p>
  </div>

  <input type="password" ngModel name="password" required #ps="ngModel" placeholder="Password">
  <div *ngIf="ps.touched && ps.invalid">
    <p>Password is required</p>
  </div>

  <button [disabled]="loginform.invalid">Submit</button>
</form>
````

### ✅ Component (TypeScript)

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
})
export class AppComponent {
  submit(form) {
    console.log('Form Data:', form.value);
  }
}
```

---

## 💼 Real-Time Example: Employee Registration Form

Let’s design a real-world form for an HR system.

### 🧱 Form Features:

* Capture employee details (Name, Email, Department, Salary)
* Validate user input
* Display validation errors dynamically
* Submit and reset form

---

### 🧾 HTML Template (`employee-form.component.html`)

```html
<h2>🏢 Employee Registration Form</h2>

<form #empForm="ngForm" (ngSubmit)="registerEmployee(empForm)">
  <div ngModelGroup="employeeInfo" #info="ngModelGroup">
    
    <label>Full Name:</label><br>
    <input type="text" ngModel name="fullName" required minlength="4" #fullName="ngModel" placeholder="Enter full name">
    <div *ngIf="fullName.touched && fullName.invalid">
      <small *ngIf="fullName.errors?.['required']">Full name is required.</small>
      <small *ngIf="fullName.errors?.['minlength']">Name should be at least 4 characters long.</small>
    </div>
    <br>

    <label>Email:</label><br>
    <input type="email" ngModel name="email" required email #email="ngModel" placeholder="Enter email">
    <div *ngIf="email.touched && email.invalid">
      <small *ngIf="email.errors?.['required']">Email is required.</small>
      <small *ngIf="email.errors?.['email']">Enter a valid email address.</small>
    </div>
    <br>

    <label>Department:</label><br>
    <select ngModel name="department" required #dept="ngModel">
      <option value="">Select Department</option>
      <option>HR</option>
      <option>Engineering</option>
      <option>Sales</option>
      <option>Finance</option>
    </select>
    <div *ngIf="dept.touched && dept.invalid">
      <small>Department selection is required.</small>
    </div>
    <br>

    <label>Salary:</label><br>
    <input type="number" ngModel name="salary" required min="10000" #salary="ngModel" placeholder="Enter salary">
    <div *ngIf="salary.touched && salary.invalid">
      <small *ngIf="salary.errors?.['required']">Salary is required.</small>
      <small *ngIf="salary.errors?.['min']">Minimum salary should be ₹10,000.</small>
    </div>
  </div>

  <br>
  <button type="submit" [disabled]="empForm.invalid">Register Employee</button>
  <button type="button" (click)="resetForm(empForm)">Reset</button>
</form>
```

---

### ⚙️ TypeScript (`employee-form.component.ts`)

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-employee-form',
  templateUrl: './employee-form.component.html',
  styleUrls: ['./employee-form.component.css']
})
export class EmployeeFormComponent {

  registerEmployee(form) {
    if (form.valid) {
      console.log('✅ Employee Registered:', form.value);
      alert(`Employee ${form.value.employeeInfo.fullName} added successfully!`);
      form.reset();
    } else {
      console.log('❌ Form Invalid');
    }
  }

  resetForm(form) {
    form.reset();
  }
}
```

---

### 🎨 CSS (`employee-form.component.css`)

```css
form {
  width: 350px;
  margin: 20px auto;
  padding: 15px;
  border: 1px solid #ccc;
  border-radius: 10px;
  background: #f9f9f9;
}

input, select {
  width: 100%;
  padding: 6px;
  margin-top: 5px;
  margin-bottom: 10px;
}

button {
  margin-right: 10px;
  padding: 6px 12px;
  border-radius: 5px;
  border: none;
  background-color: #1976d2;
  color: white;
}

button[type="button"] {
  background-color: #757575;
}

small {
  color: red;
  font-size: 0.8em;
}
```

---

## 🧭 Flow Summary

1. The form is registered automatically as an `NgForm` instance.
2. Each control with `ngModel` is registered inside it.
3. Angular tracks each control’s state (`touched`, `dirty`, `valid`, `invalid`).
4. Validation messages appear dynamically using `*ngIf`.
5. On form submission, Angular provides the form object (`form.value`, `form.valid`, etc.).
6. The component handles business logic (e.g., sending data to a service).

---

## ✅ Advantages of Template-Driven Forms

* Simple and declarative (less boilerplate)
* Great for small to medium-sized forms
* Automatic form model creation
* Easy integration with built-in validators

---

## ⚠️ Limitations

* Not ideal for very large or dynamic forms
* Harder to test programmatically
* Limited control over form state compared to Reactive Forms

---

## 🧾 Real-Time Use Cases

| Use Case                  | Example                                  |
| ------------------------- | ---------------------------------------- |
| **Employee Registration** | Collecting employee info in an HR portal |
| **User Login**            | Simple authentication form               |
| **Feedback Form**         | User feedback in websites or apps        |
| **Contact Form**          | Collecting customer inquiries            |

---

## 🏁 Conclusion

Template-driven forms are perfect for **small to medium projects** where simplicity and readability are important.
They rely heavily on Angular’s directives and **template-based validation**, making form creation quick and intuitive.

---

**Author:** Gatta Suresh
**Topic Practiced:** Template-Driven Forms in Angular
**Date:** October 2025

```
```
