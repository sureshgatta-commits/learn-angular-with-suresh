

```markdown
# 🔗 Angular Attribute Binding: Real-Time Guide

Author: Suresh  
Last Updated: October 2, 2025  
Tags: `Angular`, `Attribute Binding`, `Live Examples`, `TypeScript`

---

## 🎯 What Is Attribute Binding?

**Attribute binding** in Angular lets you set HTML attributes dynamically using component data. It uses the syntax:

```html
[attr.attributeName]="expression"
```

This is different from **property binding** (`[property]="value"`) because it targets **HTML attributes**, not DOM properties.

---

## 🧪 Real-Time Example 1: Dynamic `disabled` Attribute

```ts
export class AppComponent {
  isSubmitDisabled: boolean = true;
}
```

```html
<button [attr.disabled]="isSubmitDisabled ? true : null">Submit</button>
```

- If `isSubmitDisabled` is `true`, the button is disabled.
- If `false`, the attribute is removed (not just set to `"false"`).

---

## 🧪 Real-Time Example 2: Dynamic `colspan` in Table

```ts
export class AppComponent {
  columnSpan: number = 2;
}
```

```html
<td [attr.colspan]="columnSpan">Merged Cell</td>
```

- Dynamically sets how many columns the cell spans.

---

## 🧪 Real-Time Example 3: Dynamic `aria-label` for Accessibility

```ts
export class AppComponent {
  labelText: string = 'Submit your form';
}
```

```html
<button [attr.aria-label]="labelText">Submit</button>
```

- Improves accessibility by binding ARIA attributes.

---

## 🧪 Real-Time Example 4: Dynamic `src` for Image

```ts
export class AppComponent {
  imageUrl: string = 'https://picsum.photos/300';
}
```

```html
<img [attr.src]="imageUrl" alt="Dynamic Image">
```

- You can use `[src]` for property binding, but `[attr.src]` ensures the raw attribute is set.

---

## ❌ Common Mistakes

| Mistake | Why It Fails |
|--------|--------------|
| `[disabled]="true"` | This is **property binding**, not attribute binding |
| `[attr.disabled]="false"` | Still disables the element—use `null` to remove the attribute |
| `[attr.src]="null"` | Removes the image source—results in broken image |

---

## 🧪 Real-Time Example 5: Toggle Attribute with Button

```ts
export class AppComponent {
  isImageVisible: boolean = true;

  toggleImage() {
    this.isImageVisible = !this.isImageVisible;
  }
}
```

```html
<button (click)="toggleImage()">Toggle Image</button>
<img [attr.hidden]="isImageVisible ? null : true" src="https://picsum.photos/200" alt="Toggle Image">
```

- Clicking the button toggles the `hidden` attribute.
- When `hidden` is present, the image is not shown.

---

## ✅ Summary

- Use `[attr.attributeName]` to bind raw HTML attributes.
- Use `null` to **remove** an attribute dynamically.
- Attribute binding is essential for accessibility, layout control, and dynamic rendering.

---

## 🙌 Credits

Crafted by Suresh — passionate about teaching Angular with clarity and real-time examples.
```

---
