# 📝 Angular Course Notes

## ✏️ Data Binding

> **📝 Interpolation Binding**

component.ts code

```typescript
title: string = "Angular Course";
```

component.html code

```html
<p>{{title}}</p>
```

> **📝 Property Binding**

component.ts code

```typescript
title: string = "Angular Course";
```

component.html code

```html
<input type="text" name="title" id="title" [value]="title" />
```

> **📝 Event Binding**

component.ts code

```typescript
title: string = 'First Component';

showMsg(): void {
this.title = 'Eslam Shaker';
console.log('Button Clicked');
}
```

component.html code

```html
<button (click)="showMsg()" type="button">Click Me</button>
```

> **📝 Two-Way Binding**

component.ts code

```typescript
title: string = "First Component";
```

component.html code

```html
<input type="text" [(ngModel)]="title" />
```

> **📝 Class Binding**

component.ts code

```typescript
isActive: boolean = true;
```

component.html code

```html
<div id="data" [class.active]="isActive">
  <p>My Text Here</p>
</div>
```

component.css code

```CSS
.active {
  background-color: lightblue;
  width: 300px;
  height: 150px;
}
```

> **📝 Style Binding**

component.ts code

```typescript
fontSize = "40px";
```

component.html code

```html
<div id="data">
  <p [style.font-size]="fontSize">Change Font Size</p>
</div>
```
