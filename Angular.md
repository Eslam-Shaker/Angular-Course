# 📝 Angular Course Notes

## ✏️ Data Binding

Data binding is a technique that allows you to bind data from a data source to a UI component.

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

## ✏️ Share Data Between Components

> 📝 _Share Data From Parent Component To Child Component_

childComponent.ts code

```typescript
interface Course {
  id: number;
  title: string;
  author: string;
  publication_year: number;
  genre: {};
  description: string;
  cover_image: string;
}

@Input({ required: true }) course: Course = {} as Course;
```

parentComponent.html code

```HTML
<div class="container">
  <div id="cards">
    @for (course of courses; track course.id) {
    <app-card [course]="course" />
    } @empty {
    <p>No courses found</p>
    }
  </div>
</div>
```

> 📝 _Share Data From Child Component To Parent Component_

childComponent.ts code

```typescript
interface Course {
  id: number;
  title: string;
  author: string;
  publication_year: number;
  genre: {};
  description: string;
  cover_image: string;
}

@Output('viewCourseData') viewCourseData = new EventEmitter<Course>();

viewCourse(): void {
   this.viewCourseData.emit(this.course);
}
```

parentComponent.ts code

```typescript
interface Course {
  id: number;
  title: string;
  author: string;
  publication_year: number;
  genre: {};
  description: string;
  cover_image: string;
}

onCourseClicked(course: Course): void {
    console.log('Course Clicked: ', course);
}
```

childComponent.html code

```HTML
<div class="card card-item">
  <img src="/images/Book.png" class="card-img-top card-img" alt="..." />
  <div class="card-body">
    <h5 class="card-title">{{ course.title }}</h5>
    <div>
      <p class="card-text">
        {{ course.description }}
      </p>
    </div>
    <div>
      <button
        type="button"
        class="btn btn-outline-primary"
        (click)="viewCourse()"
      >
        Show Course
      </button>
    </div>
  </div>
</div>
```

parentComponent.html code

```HTML
<div class="container">
  <div id="cards">
    @for (course of courses; track course.id) {
    <app-card
    [course]="course"
    (viewCourseData)="onCourseClicked($event)"
     />
    } @empty {
    <p>No courses found</p>
    }
  </div>
</div>
```

## ✏️ Lifecycle Hooks

Lifecycle hooks are methods that are called at specific points in the component's lifecycle. They are used to
perform setup and teardown tasks, such as initializing data, handling user input, and updating the DOM.

> **📝 ngOnInit:** _Runs once after Angular has initialized all the component's inputs._

component.ts code

```typescript
export class DirectivesComponent implements OnInit {
  title: string = "Main Title";

  ngOnInit(): void {
    console.log("OnInit Parent Component");
    timer(2000).subscribe(() => (this.title = "Changed Title"));
  }
}
```

component.html code

```HTML
<div class="container">
   <p class="text-danger">{{title}}</p>
</div>
```

> **📝 ngOnChanges:** _Runs every time the component's inputs have changed._

component.ts code

```typescript
export class DirectivesComponent implements OnChanges {
  index: number = 1101;

  ngOnChanges(changes: SimpleChanges): void {
    console.log(`%c ngOnChanges ${this.index}`, "color: red");
  }
}
```

> **📝 ngDoCheck:** _Runs every time this component is checked for changes._

component.ts code

```typescript
export class DirectivesComponent implements DoCheck {
  index: number = 1101;

  ngDoCheck(): void {
    console.log(`%c ngDoCheck ${this.index}`, "color: purple");
  }
}
```

> **📝 ngOnDestroy:** _Runs once before the component is destroyed._

component.ts code

```typescript
export class DirectivesComponent implements OnDestroy {
  index: number = 1101;

  ngOnDestroy(): void {
    console.log(`%c ngOnDestroy ${this.index}`, "color: blue");
  }
}
```

> **📝 ngAfterContentInit:** _Runs once after the component's content has been initialized._

component.ts code

```typescript
export class DirectivesComponent implements AfterContentInit {
  index: number = 1101;

  ngAfterContentInit(): void {
    console.log(`%c ngAfterContentInit ${this.index}`, "color: green");
  }
}
```

> **📝 ngAfterContentChecked:** _Runs every time this component content has been checked for changes._

component.ts code

```typescript
export class DirectivesComponent implements AfterContentChecked {
  index: number = 1101;

  ngAfterContentChecked(): void {
    console.log(`%c ngAfterContentChecked ${this.index}`, "color: red");
  }
}
```

> **📝 ngAfterViewInit:** _Runs once after the component's view has been initialized._

component.ts code

```typescript
export class DirectivesComponent implements AfterViewInit {
  index: number = 1101;

  ngAfterViewInit(): void {
    console.log(`%c ngAfterViewInit ${this.index}`, "color: purple");
  }
}
```

> **📝 ngAfterViewChecked:** _Runs every time the component's view has been checked for changes._

component.ts code

```typescript
export class DirectivesComponent implements AfterViewChecked {
  index: number = 1101;

  ngAfterViewChecked(): void {
    console.log(`%c ngAfterViewChecked ${this.index}`, "color: blue");
  }
}
```

## ✏️ Angular Routing

Angular Routing is a powerful feature that allows you to navigate between different views or components in your application.

> **📝 router-outlet:** _A directive that marks the location where the router should display the component for the activated route._

appComponent.ts code

```typescript
@Component({
  selector: 'app-root',
  standalone: true,
  imports: [
    RouterOutlet,
    HeaderComponent,
  ],
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss'],
})
```

```HTML
<app-header />

<router-outlet></router-outlet>
```

> **📝 routerLink:** _A directive that generates an anchor element with the href attribute set to the route path._

app.routes.ts code

```typescript
export const routes: Routes = [
  {
    path: "courses",
    component: CoursesComponent,
  },
];
```

appComponent.html code

```HTML
<ul class="nav nav-tabs">
  <li class="nav-item">
    <a
      class="nav-link"
      routerLink="courses"
    >
      Courses
    </a>
  </li>
</ul>
```

> **📝 routerLinkActive:** _A directive that adds a CSS class to an element when the linked route is active._

appComponent.html code

```HTML
<ul class="nav nav-tabs">
  <li class="nav-item">
    <a
      class="nav-link"
      routerLink="courses"
      routerLinkActive="active"
    >
      Courses
    </a>
  </li>
</ul>
```

> **📝 routerLinkActiveOptions:** _A directive that allows you to customize the routerLinkActive directive._

app.routes.ts code

```typescript
export const routes: Routes = [
  {
    path: "courses",
    component: CoursesComponent,
  },
  {
    path: "courses/:id",
    component: CourseDetailsComponent,
  },
];
```

appComponent.html code

```HTML
<ul class="nav nav-tabs">
  <li class="nav-item">
    <a
      class="nav-link"
      routerLink="courses"
      routerLinkActive="active"
      [routerLinkActiveOptions]="{ exact: true }"
    >
      Courses
    </a>
  </li>
  <li class="nav-item">
    <a
      class="nav-link"
      routerLink="courses/5"
      routerLinkActive="active"
      [routerLinkActiveOptions]="{ exact: true }"
    >
      Course Details
    </a>
  </li>
</ul>
```

> **📝 Wildcard Notation:** _A notation used in route configuration to match any URL path._

app.routes.ts code

```typescript
export const routes: Routes = [
  {
    path: "courses",
    component: CoursesComponent,
  },
  {
    path: "courses/:id",
    component: CourseDetailsComponent,
  },
  {
    path: "**",
    component: PageNotFoundComponent,
  },
];
```

> **📝 Nesting Routing:** _A technique used to create nested routes in Angular applications._

app.routes.ts code

```typescript
export const routes: Routes = [
  {
    path: "account",
    component: AccountComponent,
    children: [
      {
        path: "login",
        component: LoginComponent,
      },
      {
        path: "register",
        component: RegisterComponent,
      },
      {
        path: "",
        redirectTo: "/account/login",
        pathMatch: "full",
      },
    ],
  },
  {
    path: "**",
    component: PageNotFoundComponent,
  },
];
```
