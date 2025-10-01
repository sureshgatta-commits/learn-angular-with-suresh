

```markdown
📅 Date: 01 October 2025

# 📁 Angular 13 Folder Structure – Real-Time Developer Notes

This guide explains the key folders and files in an Angular 13 project, with real-time examples and code snippets to help developers understand how each part is used.

---

## 🔹 `src/` – Main Application Folder

Everything you build lives inside `src/`. It contains your app logic, templates, styles, and configuration files.

---

### 📂 `app/` – Core Application Code

This is where your components, modules, services, and routing live.

#### 🔸 `app.module.ts` – Root Module

Registers components and sets up routing.

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

#### 🔸 `app.component.ts` – Root Component Logic

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

#### 🔸 `app.component.html` – Root Component Template

```html
<h1>{{ title }}</h1>
<app-top-bar></app-top-bar>
<router-outlet></router-outlet>
```

---

#### 🔸 `top-bar.component.ts` – Example Header Component

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

#### 🔸 `product-list.component.ts` – Example Feature Component

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

### 📂 `assets/` – Static Files

Used for images, icons, fonts, and other static resources.

💡 Real-time use: Store logos, product images, downloadable PDFs.

---

### 📂 `environments/` – Environment Configs

Contains:
- `environment.ts` → development settings
- `environment.prod.ts` → production settings

💡 Real-time use: Switch API URLs, enable/disable features based on environment.

---

### 📄 `index.html` – Main HTML Shell

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>AngularApp</title>
</head>
<body>
  <app-root></app-root>
</body>
</html>
```

💡 Real-time use: Loads Angular and sets up the root component.

---

### 📄 `main.ts` – App Bootstrap Entry

```ts
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { AppModule } from './app/app.module';

platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
```

💡 Real-time use: Starts the Angular app by loading `AppModule`.

---

### 📄 `styles.css` – Global Styles

Used for global styling across all components.

```css
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}
```

💡 Real-time use: Apply resets, fonts, layout rules.

---

### 📄 `polyfills.ts` – Browser Compatibility

Includes polyfills to support older browsers.

💡 Real-time use: Ensures Angular features work across different environments.

---

### 📄 `test.ts` – Unit Test Entry Point

Used by Karma and Jasmine to run tests.

💡 Real-time use: Configure and run automated unit tests.

---

### 📄 `favicon.ico` – Browser Tab Icon

💡 Real-time use: Branding and polish for your app.

---

## 🧪 Real-Time Developer Tips

- Use `ng generate component component-name` to scaffold components quickly.
- Organize features into folders: `products/`, `users/`, `admin/`
- Create shared modules for reusable components and pipes.
- Use `app-routing.module.ts` to keep routing clean and scalable.

---

Let’s build Angular apps that are clean, modular, and ready for real-world deployment!
```

Let me know when you're ready for Day 2—I’ll prep notes on **Components, Templates, and Data Binding** with real-time examples!
