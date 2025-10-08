```markdown
# Angular Class Binding - Complete Guide

A comprehensive guide to dynamic class binding in Angular for real-time applications.

## 📋 Table of Contents
- [Basic Syntax](#basic-syntax)
- [ngClass Directive](#ngclass-directive)
- [Real-Time Use Cases](#real-time-use-cases)
- [Performance Optimization](#performance-optimization)
- [Best Practices](#best-practices)
- [Common Patterns](#common-patterns)

## 🎯 Basic Syntax

### Single Class Binding
```html
<!-- Conditional class application -->
<div [class.active]="isActive"></div>
<div [class.error]="hasError"></div>
<div [class.loading]="isLoading"></div>

<!-- Multiple static classes (recommended approach) -->
<div class="div1 div2"></div>

<!-- Dynamic string binding -->
<div [class]="'btn btn-primary'"></div>
<div [class]="isActive ? 'active' : 'inactive'"></div>
```

## 🔧 ngClass Directive

### Object Syntax (Most Common)
```html
<div [ngClass]="{
  'active': isActive,
  'error': hasError,
  'disabled': isDisabled,
  'highlighted': isSelected
}"></div>
```

### Array Syntax
```html
<div [ngClass]="['base-class', 'common-class', condition ? 'conditional-class' : '']"></div>
```

### Method-based Classes
```typescript
// component.ts
getButtonClasses() {
  return {
    'btn': true,
    'btn-primary': this.type === 'primary',
    'btn-loading': this.loading,
    'btn-disabled': this.disabled
  };
}
```

```html
<!-- template -->
<button [ngClass]="getButtonClasses()">Click</button>
```

## ⚡ Real-Time Use Cases

### Form Validation
```html
<input 
  type="email"
  [class.valid]="email.valid && email.touched"
  [class.invalid]="email.invalid && email.touched"
  [class.pending]="email.pending"
  [class.typing]="isTyping">
```

### User Interface States
```html
<!-- Navigation -->
<nav [class.sticky]="scrollY > 100"
     [class.transparent]="scrollY < 50">
</nav>

<!-- Loading states -->
<div [class.skeleton]="!dataLoaded"
     [class.fade-in]="dataLoaded">
  {{ content }}
</div>
```

### Live Data Applications
```html
<!-- Stock market dashboard -->
<div [class.price-up]="currentPrice > previousPrice"
     [class.price-down]="currentPrice < previousPrice"
     [class.volatile]="volatility > 0.05">
  ${{ currentPrice }}
</div>

<!-- Server monitoring -->
<div [class.status-online]="serverStatus === 'online'"
     [class.status-offline]="serverStatus === 'offline'"
     [class.status-warning]="serverStatus === 'degraded'">
  {{ serverName }}
</div>
```

### Game/Action States
```html
<div [class.attacking]="isAttacking"
     [class.defending]="isDefending"
     [class.damaged]="health < 30"
     [class.power-up]="hasPowerUp">
  Player
</div>
```

## 🚀 Performance Optimization

### Use TrackBy with Lists
```html
<div *ngFor="let item of items; trackBy: trackById"
     [class.updated]="item.updated"
     [class.selected]="item.id === selectedId">
  {{ item.name }}
</div>
```

### Avoid Complex Template Logic
```typescript
// ❌ Don't (complex logic in template)
[class.special]="user?.profile?.settings?.theme === 'dark' && isPremium"

// ✅ Do (move to component)
getSpecialClass() {
  return this.user?.profile?.settings?.theme === 'dark' && this.isPremium;
}
```

### Debounce Rapid Updates
```typescript
// For real-time search inputs
fromEvent(searchInput, 'input')
  .pipe(
    debounceTime(300),
    distinctUntilChanged()
  )
  .subscribe(() => {
    this.isSearching = true;
  });
```

## 📝 Best Practices

### Naming Conventions
```html
<!-- Use consistent naming -->
<div [class.button--primary]="type === 'primary'"
     [class.button--loading]="loading"
     [class.button--disabled]="disabled">
</div>

<!-- State-based classes -->
<div [class.is-active]="isActive"
     [class.has-error]="hasError"
     [class.is-loading]="isLoading">
</div>
```

### Conditional Logic Management
```typescript
// Complex conditions in component
getStatusClasses() {
  return {
    'status-success': this.status === 'completed',
    'status-warning': this.status === 'pending',
    'status-error': this.status === 'failed',
    'status-processing': this.status === 'processing'
  };
}
```

### Responsive Design
```typescript
getResponsiveClasses() {
  const screenSize = this.getScreenSize();
  return {
    'mobile-layout': screenSize === 'mobile',
    'tablet-layout': screenSize === 'tablet', 
    'desktop-layout': screenSize === 'desktop'
  };
}
```

## 🔄 Common Patterns

### State Machine Pattern
```html
<div [class.state-initial]="currentState === 'initial'"
     [class.state-loading]="currentState === 'loading'"
     [class.state-success]="currentState === 'success'"
     [class.state-error]="currentState === 'error'">
</div>
```

### Theme Switching
```html
<div [class.theme-light]="currentTheme === 'light'"
     [class.theme-dark]="currentTheme === 'dark'"
     [class.theme-high-contrast]="currentTheme === 'high-contrast'">
</div>
```

### Feature Flags
```html
<div [class.feature-new-ui]="featureFlags.newUI"
     [class.feature-beta]="featureFlags.betaFeatures"
     [class.feature-premium]="user.isPremium">
</div>
```

### Animation States
```html
<div [class.entering]="animationState === 'entering'"
     [class.leaving]="animationState === 'leaving'"
     [class.idle]="animationState === 'idle'">
</div>
```

## 💡 Key Takeaways

1. **Use `[class.className]`** for simple conditional classes
2. **Use `[ngClass]`** for complex multiple class logic
3. **Prefer `class="static-class"`** for always-applied classes
4. **Keep template logic simple** - move complex conditions to component
5. **Use descriptive class names** that reflect state/condition
6. **Consider performance** with frequent real-time updates
7. **Follow consistent naming conventions**

## 🎯 When to Use Which Approach

| Scenario | Recommended Approach |
|----------|---------------------|
| Static classes | `class="class1 class2"` |
| Single conditional class | `[class.active]="isActive"` |
| Multiple conditional classes | `[ngClass]="{object}"` |
| Mixed static + dynamic | `class="static" [class.dynamic]="condition"` |
| Complex logic | Method returning class object |

---

**📚 Pro Tip:** Always prefer the simplest approach that meets your requirements. Static classes are more performant than dynamic binding when the classes don't change.

