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
## ✏️ Directives

> **📝 ngFor | @for :** _Repeat a node for each item in a list_

component.ts code

```typescript
courses: Array<ICourse> = [
  {
    id: 1,
    title: "To Kill a Mockingbird",
    desc: "A classic novel depicting racial injustice in the American South.",
    imageURL: "https://fakeimg.pl/667x1000/cc6600",
    category: Categories.beginner,
  },
  {
    id: 2,
    title: "Pride and Prejudice",
    desc: "A classic novel exploring themes of love, marriage, and social norms.",
    imageURL: "https://fakeimg.pl/667x1000/cc6600",
    category: Categories.advanced,
  },
];
```

component.html code

```HTML
<!-- ===== Old Syntax  ===== -->

<ng-container *ngFor="let course of courses">
<div class="card card-item">
   <img src="/images/Book.png" class="card-img-top card-img" alt="..." />
   <div class="card-body">
      <h6 class="text-danger">{{ title }}</h6>
      <h5 class="card-title">{{ course.title }}</h5>
      <div>
         <p class="card-text">
              {{ course.desc }}
         </p>
      </div>
      <div>
         <button
              type="button"
              class="btn btn-outline-primary"
              (click)="viewData()"
         >
              Show Course
         </button>
      </div>
   </div>
</div>
</ng-container>

<!-- ===== New Syntax  ===== -->
 @for (course of courses; track trackCourse) {
    <div class="card card-item">
   <img src="/images/Book.png" class="card-img-top card-img" alt="..." />
   <div class="card-body">
      <h6 class="text-danger">{{ title }}</h6>
      <h5 class="card-title">{{ course.title }}</h5>
      <div>
         <p class="card-text">
              {{ course.desc }}
         </p>
      </div>
      <div>
         <button
              type="button"
              class="btn btn-outline-primary"
              (click)="viewData()"
         >
              Show Course
         </button>
      </div>
   </div>
</div>
}

```

> **📝 ngIf | @if :** _Conditionally creates or disposes of subviews from the template._

component.ts code

```typescript
  list: string[] = ['Eslam', 'Hossam', 'Mustafa'];
```

component.html code

```HTML
<!-- ===== Old Syntax  ===== -->
<ul>
  <ng-container *ngFor="let name of list; let i = index">
    <li *ngIf="i !== 0">
      {{ i + 1 }} - {{ name }}
    </li>
  </ng-container>
</ul>

<!-- ===== New Syntax  ===== -->
 <ul>
   <ng-container *ngFor="let name of list; let i = index">
   @if(i !== 0){
      <li>
         {{ i + 1 }} - {{ name }}
      </li>
   }@else {
       <li>
          <strong>First Item</strong>
       </li>
   }
  </ng-container>
</ul>

```

> **📝 ngSwitch | @switch :** _A set of directives that switch among alternative views._

component.ts code

```typescript
enum Categories {
  beginner = 1,
  intermediate = 2,
  advanced = 3,
  other = 4,
}
```

component.html code

```HTML
<!-- ===== Old Syntax  ===== -->
<div [ngSwitch] = "course.category">
   <span *ngSwitchCase="Categories.beginner" class="badge bg-warning">beginner</span>

   <span *ngSwitchCase="Categories.intermediate" class="badge bg-primary">intermediate</span>

   <span *ngSwitchCase="Categories.advanced" class="badge bg-success">advanced</span>

   <span *ngSwitchDefault class="badge bg-secondary">other</span>
</div>

<!-- ===== New Syntax  ===== -->
<div>
@switch (course.category) {
   @case (Categories.beginner) {
      <span class="badge bg-warning">beginner</span>
   } @case (Categories.intermediate) {
      <span class="badge bg-info">intermediate</span>
   } @case (Categories.advanced) {
      <span class="badge bg-success">advanced</span>
   } @default {
      <span class="badge bg-danger">other</span>
   }
}
</div>

```

> **📝 ngClass :** _adds and removes a set of CSS classes._

component.ts code

```typescript
interface Tech {
  name: string;
  logo: string;
  description: string;
  isActive: boolean;
}

techs: Tech[] = [
   {
      name: 'Angular',
      logo: 'favicon.ico',
      description: 'Course 01',
      isActive: true,
   },
   {
      name: 'NodeJs',
      logo: 'favicon.ico',
      description: 'Course 02',
      isActive: false,
   },
]
```

component.html code

```html
<div id="content">
  <div *ngFor="let tool of techs; let id = index" [ngClass]="tool.isActive ? 'active' : 'notActive'" class="item">
    <img [src]="tool.logo" alt="" srcset="" />
    <h3>{{ tool.name }}</h3>
    <p>{{ tool.description }}</p>
    <button type="button" (click)="deleteItem(id)">Delete</button>
    <button type="button" (click)="setActive(id)">{{ tool.isActive ? "Not Active" : "Set Active" }}</button>
  </div>
</div>
```

component.css code

```CSS
.active {
  background-color: lightcoral;
}

.notActive {
  background-color: lightblue;
}
```

> **📝 ngStyle :** _adds and removes a set of HTML styles._

component.ts code

```typescript

currentStyles: Record<string, string> = {
   'font-style': 'italic',
   'font-weight': 'bold',
   'font-size': '24px',
};

interface Tech {
  name: string;
  logo: string;
  description: string;
  isActive: boolean;
}

techs: Tech[] = [
   {
      name: 'Angular',
      logo: 'favicon.ico',
      description: 'Course 01',
      isActive: true,
   },
   {
      name: 'NodeJs',
      logo: 'favicon.ico',
      description: 'Course 02',
      isActive: false,
   },
]
```

component.html code

```html
<div id="content">
  <div *ngFor="let tool of techs; let id = index" [ngStyle]="currentStyles" class="item">
    <img [src]="tool.logo" alt="" srcset="" />
    <h3>{{ tool.name }}</h3>
    <p>{{ tool.description }}</p>
    <button type="button" (click)="deleteItem(id)">Delete</button>
    <button type="button" (click)="setActive(id)">{{ tool.isActive ? "Not Active" : "Set Active" }}</button>
  </div>
</div>
```
## ✏️ Pipes

> 📝 _To Format Data In Angular_

component.ts code

```typescript
data = {
  title: "course title",
  description: "course description",
  publishedAt: new Date().toLocaleString(),
  price: 200.4576,
  discount: 0.25,
};
```

component.html code

```HTML
<div class="container">
  <ul class="container" id="pipes-list">
   <!-- UpperCase Pipe -->
    <li>
      <span class="fw-bold text-danger">UpperCase:</span>
      {{ data.title | uppercase }}
    </li>

   <!-- LowerCase Pipe -->
    <li>
      <span class="fw-bold text-danger">LowerCase:</span>
      {{ data.title | lowercase }}
    </li>

   <!-- TitleCase Pipe -->
    <li>
      <span class="fw-bold text-danger">TitleCase:</span>
      {{ data.description | titlecase }}
    </li>

   <!-- Date Pipe -->
    <li>
      <span class="fw-bold text-danger">Date:</span>
      {{ data.publishedAt | date : "dd-MM-yyyy HH:mm:ss" }}
    </li>

   <!-- Decimal Pipe -->
    <li>
      <span class="fw-bold text-danger">Decimal:</span>
      {{ data.price | number : ".1-2" }}
    </li>

   <!-- Currency Pipe -->
    <li>
      <span class="fw-bold text-danger">Currency:</span>
      {{ data.price | currency }}
    </li>

   <!-- Percent Pipe -->
    <li>
      <span class="fw-bold text-danger">Percent:</span>
      {{ data.discount | percent }}
    </li>

   <!-- JSON Pipe -->
    <li>
      <span class="fw-bold text-danger">Json:</span>
      {{ data | json }}
    </li>

   <!-- KeyValue Pipe -->
    <li>
      <span class="fw-bold text-danger">KeyValue:</span>
      @for (item of data | keyvalue; track item) {
      <div>
        <span class="text-info">key: </span> {{ item.key }}
        <span class="text-info">value: </span> {{ item.value }}
      </div>
      }
    </li>
  </ul>
</div>
```
