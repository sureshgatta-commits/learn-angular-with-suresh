
📅 Date: 01 October 2025

# 🚀 Day 1 – Introduction to Angular & File Structure (Angular 13)

Angular is a powerful front-end framework for building dynamic, single-page web applications.  
It uses TypeScript, component-based architecture, and built-in tools for routing, forms, and HTTP communication.

---

## 📁 Angular Project Structure (Developer-Focused)

When you run `ng new project-name`, Angular generates a structured folder layout. Here's what developers focus on:

```
src/
├── app/
│   ├── app.module.ts         # Root module
│   ├── app.component.ts      # Root component logic
│   ├── app.component.html    # Root component template
│   ├── app.component.css     # Root component styles
│   ├── top-bar.component.ts  # Example child component
│   ├── product-list.component.ts # Example feature component
│   └── ... other components
├── assets/                   # Static files (images, icons)
├── environments/             # Dev/prod environment configs
├── index.html                # Main HTML shell
├── main.ts                   # App bootstrap entry
└── styles.css                # Global styles
```

---

## 🧠 Core Files with Real-Time Code

---

### 1️⃣ `app.module.ts` – Root Module

```ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { ReactiveFormsModule } from '@angular/forms';
import { RouterModule } from '@angular/router';

import { AppComponent } from './app.component';
import { TopBarComponent } from './top-bar.component';
import { ProductListComponent } from './product-list.component';

@NgModule({
  imports: [
    BrowserModule,
    ReactiveFormsModule,
    RouterModule.forRoot([
      { path: '', component: ProductListComponent },
    ])
  ],
  declarations: [
    AppComponent,
    TopBarComponent,
    ProductListComponent
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

---

### 2️⃣ `app.component.ts` – Root Component Logic

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'My Angular App';
}
```

---

### 3️⃣ `app.component.html` – Root Component Template

```html
<h1>{{ title }}</h1>
<app-top-bar></app-top-bar>
<router-outlet></router-outlet>
```

---

### 4️⃣ `top-bar.component.ts` – Example Header Component

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-top-bar',
  template: `<h2>Welcome to the Top Bar!</h2>`,
  styles: [`h2 { color: teal; text-align: center; }`]
})
export class TopBarComponent { }
```

---

### 5️⃣ `product-list.component.ts` – Example Feature Component

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-product-list',
  template: `
    <h3>Product List</h3>
    <ul>
      <li *ngFor="let product of products">{{ product }}</li>
    </ul>
  `
})
export class ProductListComponent {
  products = ['Laptop', 'Phone', 'Tablet'];
}
```

---

## 🧪 Real-Time Tip

- Use `ng generate component component-name` to auto-create files with boilerplate.
- Keep components small and focused.
- Use routing for navigation between views.

---

Let’s build dynamic apps—one component at a time!
