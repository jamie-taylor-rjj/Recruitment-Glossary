---
title: "What is Angular?"
description: "Just what is Angular, is it different to Angular.js, and what can developers do with it?"
lead: "Just what is Angular, and what can developers do with it?"
date: 2020-10-06T08:49:31+00:00
lastmod: 2023-12-04T11:30:00+01:00
draft: false
images: []
menu:
  docs:
    parent: "angular"
weight: 100
toc: true
---

## 10,000 ft Overview

Angular is a comprehensive [TypeScript]({{< relref "what-is-typescript" >}})-based web application framework developed by Google. It's designed for building dynamic, single-page applications (SPAs) and provides a complete solution including routing, forms, HTTP client, testing utilities, and more. Angular is fundamentally different from AngularJS (version 1.x) - it's a complete rewrite with a modern architecture.

Unlike [React]({{< relref "what-is-react" >}}), which is a library focused on UI components, Angular is a full framework that provides opinions and solutions for nearly every aspect of large-scale application development. It uses [TypeScript]({{< relref "what-is-typescript" >}}) by default, leverages dependency injection extensively, and follows a component-based architecture.

Angular applications are typically built using [Node.js]({{< relref "what-are-npm-and-nodejs" >}}) tooling and are particularly well-suited for enterprise applications where consistency, maintainability, and scalability are priorities. The framework includes powerful features like two-way data binding, directives, services, and a sophisticated CLI for development and deployment.

{{< alert icon="💡" text="Angular (version 2+) is completely different from AngularJS (version 1.x). Angular is a modern framework built with TypeScript, while AngularJS was a JavaScript framework. They are not compatible and serve different purposes, though Google provides migration paths for AngularJS applications." />}}

## Beginner Information

Angular uses a component-based architecture where applications are built as a tree of components, each managing its own template, logic, and styling.

**Basic Angular Component:**

{{< highlight typescript "linenos=inline">}}
import { Component } from '@angular/core';

@Component({
  selector: 'app-welcome',
  template: `
    <div>
      <h1>Hello, {{ name }}!</h1>
      <p>You clicked {{ count }} times</p>
      <button (click)="increment()">Click me</button>
    </div>
  `,
  styles: [`
    h1 { color: blue; }
    button { padding: 10px; margin: 5px; }
  `]
})
export class WelcomeComponent {
  name = 'Angular Developer';
  count = 0;

  increment() {
    this.count++;
  }
}
{{< /highlight >}}

**Angular Template Syntax:**

{{< highlight html "linenos=inline">}}
<!-- Data binding -->
<h1>{{ title }}</h1>
<img [src]="imageUrl" [alt]="imageAlt">

<!-- Event binding -->
<button (click)="onClick()">Click me</button>
<input (keyup)="onKeyUp($event)">

<!-- Two-way data binding -->
<input [(ngModel)]="username">

<!-- Structural directives -->
<div *ngIf="isVisible">This shows conditionally</div>
<ul>
  <li *ngFor="let item of items; let i = index">
    {{ i }}: {{ item.name }}
  </li>
</ul>

<!-- Template reference variables -->
<input #nameInput>
<button (click)="greet(nameInput.value)">Greet</button>
{{< /highlight >}}

**Services and Dependency Injection:**

{{< highlight typescript "linenos=inline">}}
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class UserService {
  private apiUrl = '/api/users';

  constructor(private http: HttpClient) {}

  getUsers(): Observable<User[]> {
    return this.http.get<User[]>(this.apiUrl);
  }

  getUserById(id: number): Observable<User> {
    return this.http.get<User>(`${this.apiUrl}/${id}`);
  }

  createUser(user: User): Observable<User> {
    return this.http.post<User>(this.apiUrl, user);
  }
}

// Using the service in a component
@Component({
  selector: 'app-user-list',
  template: `
    <div *ngFor="let user of users">
      <h3>{{ user.name }}</h3>
      <p>{{ user.email }}</p>
    </div>
  `
})
export class UserListComponent implements OnInit {
  users: User[] = [];

  constructor(private userService: UserService) {}

  ngOnInit() {
    this.userService.getUsers().subscribe(
      users => this.users = users
    );
  }
}
{{< /highlight >}}

**Getting Started:**

{{< highlight bash >}}
# Install Angular CLI globally
npm install -g @angular/cli

# Create a new Angular application
ng new my-angular-app
cd my-angular-app

# Start development server
ng serve

# Generate components, services, etc.
ng generate component user-profile
ng generate service user

# Build for production
ng build --prod
{{< /highlight >}}

**Key Angular Concepts:**

- **Components**: Building blocks with template, logic, and styling
- **Services**: Shared business logic and data access
- **Modules**: Organize application into cohesive blocks
- **Dependency Injection**: Automatic provision of dependencies
- **RxJS**: Reactive programming with Observables
- **Angular CLI**: Command-line tool for development

## Intermediary Information

Angular's architecture promotes scalable, maintainable applications through well-defined patterns and powerful features.

**Angular Modules and Lazy Loading:**

{{< highlight typescript "linenos=inline">}}
// App module
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { HttpClientModule } from '@angular/common/http';
import { FormsModule, ReactiveFormsModule } from '@angular/forms';

@NgModule({
  declarations: [
    AppComponent,
    HomeComponent,
    NavbarComponent
  ],
  imports: [
    BrowserModule,
    HttpClientModule,
    FormsModule,
    ReactiveFormsModule,
    AppRoutingModule
  ],
  providers: [
    UserService,
    AuthService
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }

// Feature module with lazy loading
@NgModule({
  declarations: [
    UserListComponent,
    UserDetailComponent,
    UserFormComponent
  ],
  imports: [
    CommonModule,
    FormsModule,
    ReactiveFormsModule,
    UserRoutingModule
  ]
})
export class UserModule { }

// Lazy loading in routing
const routes: Routes = [
  { path: '', component: HomeComponent },
  { 
    path: 'users', 
    loadChildren: () => import('./user/user.module').then(m => m.UserModule)
  }
];
{{< /highlight >}}

**Reactive Forms:**

{{< highlight typescript "linenos=inline">}}
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

@Component({
  selector: 'app-user-form',
  template: `
    <form [formGroup]="userForm" (ngSubmit)="onSubmit()">
      <div>
        <label for="name">Name:</label>
        <input id="name" formControlName="name">
        <div *ngIf="userForm.get('name')?.errors?.['required'] && userForm.get('name')?.touched">
          Name is required
        </div>
      </div>

      <div>
        <label for="email">Email:</label>
        <input id="email" type="email" formControlName="email">
        <div *ngIf="userForm.get('email')?.errors?.['email'] && userForm.get('email')?.touched">
          Please enter a valid email
        </div>
      </div>

      <div formGroupName="address">
        <h3>Address</h3>
        <input placeholder="Street" formControlName="street">
        <input placeholder="City" formControlName="city">
        <input placeholder="Zip Code" formControlName="zipCode">
      </div>

      <button type="submit" [disabled]="userForm.invalid">Submit</button>
    </form>
  `
})
export class UserFormComponent {
  userForm: FormGroup;

  constructor(private fb: FormBuilder) {
    this.userForm = this.fb.group({
      name: ['', [Validators.required, Validators.minLength(2)]],
      email: ['', [Validators.required, Validators.email]],
      address: this.fb.group({
        street: [''],
        city: [''],
        zipCode: ['', Validators.pattern(/^\d{5}$/)]
      })
    });
  }

  onSubmit() {
    if (this.userForm.valid) {
      console.log(this.userForm.value);
    }
  }
}
{{< /highlight >}}

**RxJS and Reactive Programming:**

{{< highlight typescript "linenos=inline">}}
import { Observable, combineLatest, map, filter, debounceTime } from 'rxjs';

@Component({
  selector: 'app-search',
  template: `
    <input #searchInput (keyup)="onSearch(searchInput.value)">
    <select #categorySelect (change)="onCategoryChange(categorySelect.value)">
      <option value="">All Categories</option>
      <option value="tech">Technology</option>
      <option value="business">Business</option>
    </select>

    <div *ngFor="let result of searchResults$ | async">
      {{ result.title }}
    </div>
  `
})
export class SearchComponent {
  private searchTerm$ = new Subject<string>();
  private category$ = new Subject<string>();
  
  searchResults$: Observable<SearchResult[]>;

  constructor(private searchService: SearchService) {
    this.searchResults$ = combineLatest([
      this.searchTerm$.pipe(
        debounceTime(300),
        filter(term => term.length >= 2)
      ),
      this.category$.pipe(startWith(''))
    ]).pipe(
      map(([term, category]) => ({ term, category })),
      switchMap(({ term, category }) => 
        this.searchService.search(term, category)
      )
    );
  }

  onSearch(term: string) {
    this.searchTerm$.next(term);
  }

  onCategoryChange(category: string) {
    this.category$.next(category);
  }
}
{{< /highlight >}}

**Angular Guards and Interceptors:**

{{< highlight typescript "linenos=inline">}}
// Route guard
@Injectable()
export class AuthGuard implements CanActivate {
  constructor(private auth: AuthService, private router: Router) {}

  canActivate(): boolean {
    if (this.auth.isAuthenticated()) {
      return true;
    }
    this.router.navigate(['/login']);
    return false;
  }
}

// HTTP Interceptor
@Injectable()
export class AuthInterceptor implements HttpInterceptor {
  constructor(private auth: AuthService) {}

  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    const token = this.auth.getToken();

    if (token) {
      const authReq = req.clone({
        headers: req.headers.set('Authorization', `Bearer ${token}`)
      });
      return next.handle(authReq);
    }
    
    return next.handle(req);
  }
}
{{< /highlight >}}

## Advanced Information

Enterprise Angular development involves sophisticated patterns, optimization techniques, and architectural considerations for large-scale applications.

**Advanced Component Patterns:**

{{< highlight typescript "linenos=inline">}}
// Custom directive
@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  @Input() highlightColor = 'yellow';
  @Input() appHighlight = '';

  @HostListener('mouseenter') onMouseEnter() {
    this.highlight(this.highlightColor || this.appHighlight || 'yellow');
  }

  @HostListener('mouseleave') onMouseLeave() {
    this.highlight('');
  }

  private highlight(color: string) {
    this.el.nativeElement.style.backgroundColor = color;
  }

  constructor(private el: ElementRef) {}
}

// Custom pipe
@Pipe({ name: 'exponentialStrength' })
export class ExponentialStrengthPipe implements PipeTransform {
  transform(value: number, exponent = 1): number {
    return Math.pow(value, isNaN(exponent) ? 1 : exponent);
  }
}

// Dynamic component loading
@Component({
  selector: 'app-dynamic-host',
  template: `<ng-template #dynamicHost></ng-template>`
})
export class DynamicHostComponent implements OnInit {
  @ViewChild('dynamicHost', { read: ViewContainerRef }) 
  dynamicHost: ViewContainerRef;

  constructor(private componentFactoryResolver: ComponentFactoryResolver) {}

  ngOnInit() {
    this.loadComponent();
  }

  loadComponent() {
    const componentFactory = this.componentFactoryResolver
      .resolveComponentFactory(DynamicComponent);

    this.dynamicHost.clear();
    const componentRef = this.dynamicHost.createComponent(componentFactory);
    componentRef.instance.data = { message: 'Hello Dynamic World!' };
  }
}
{{< /highlight >}}

**State Management with NgRx:**

{{< highlight typescript "linenos=inline">}}
// Actions
export const loadUsers = createAction('[User] Load Users');
export const loadUsersSuccess = createAction(
  '[User] Load Users Success',
  props<{ users: User[] }>()
);
export const loadUsersFailure = createAction(
  '[User] Load Users Failure',
  props<{ error: string }>()
);

// Reducer
const initialState: UserState = {
  users: [],
  loading: false,
  error: null
};

const userReducer = createReducer(
  initialState,
  on(loadUsers, state => ({ ...state, loading: true })),
  on(loadUsersSuccess, (state, { users }) => ({
    ...state,
    users,
    loading: false,
    error: null
  })),
  on(loadUsersFailure, (state, { error }) => ({
    ...state,
    loading: false,
    error
  }))
);

// Effects
@Injectable()
export class UserEffects {
  loadUsers$ = createEffect(() =>
    this.actions$.pipe(
      ofType(loadUsers),
      mergeMap(() =>
        this.userService.getUsers().pipe(
          map(users => loadUsersSuccess({ users })),
          catchError(error => of(loadUsersFailure({ error: error.message })))
        )
      )
    )
  );

  constructor(
    private actions$: Actions,
    private userService: UserService
  ) {}
}

// Selectors
export const selectUserState = createFeatureSelector<UserState>('user');
export const selectUsers = createSelector(selectUserState, state => state.users);
export const selectUsersLoading = createSelector(selectUserState, state => state.loading);
{{< /highlight >}}

**Testing Angular Applications:**

{{< highlight typescript "linenos=inline">}}
// Unit test for component
describe('UserComponent', () => {
  let component: UserComponent;
  let fixture: ComponentFixture<UserComponent>;
  let userService: jasmine.SpyObj<UserService>;

  beforeEach(() => {
    const spy = jasmine.createSpyObj('UserService', ['getUsers']);

    TestBed.configureTestingModule({
      declarations: [UserComponent],
      providers: [{ provide: UserService, useValue: spy }]
    });

    fixture = TestBed.createComponent(UserComponent);
    component = fixture.componentInstance;
    userService = TestBed.inject(UserService) as jasmine.SpyObj<UserService>;
  });

  it('should load users on init', () => {
    const mockUsers = [{ id: 1, name: 'John' }];
    userService.getUsers.and.returnValue(of(mockUsers));

    component.ngOnInit();

    expect(userService.getUsers).toHaveBeenCalled();
    expect(component.users).toEqual(mockUsers);
  });
});

// Integration test
describe('UserListComponent', () => {
  let component: UserListComponent;
  let fixture: ComponentFixture<UserListComponent>;

  beforeEach(() => {
    TestBed.configureTestingModule({
      declarations: [UserListComponent],
      imports: [HttpClientTestingModule]
    });

    fixture = TestBed.createComponent(UserListComponent);
    component = fixture.componentInstance;
  });

  it('should display user names', async () => {
    component.users = [{ id: 1, name: 'John' }, { id: 2, name: 'Jane' }];
    fixture.detectChanges();

    const compiled = fixture.nativeElement;
    expect(compiled.textContent).toContain('John');
    expect(compiled.textContent).toContain('Jane');
  });
});
{{< /highlight >}}

**Performance Optimization:**

{{< highlight typescript "linenos=inline">}}
// OnPush change detection
@Component({
  selector: 'app-user-card',
  changeDetection: ChangeDetectionStrategy.OnPush,
  template: `
    <div>
      <h3>{{ user.name }}</h3>
      <p>{{ user.email }}</p>
    </div>
  `
})
export class UserCardComponent {
  @Input() user: User;
}

// TrackBy function for *ngFor
@Component({
  template: `
    <div *ngFor="let item of items; trackBy: trackByFn">
      {{ item.name }}
    </div>
  `
})
export class ItemListComponent {
  items: Item[] = [];

  trackByFn(index: number, item: Item): number {
    return item.id;
  }
}

// Async pipe for automatic subscription management
@Component({
  template: `
    <div *ngFor="let user of users$ | async">
      {{ user.name }}
    </div>
  `
})
export class UserListComponent {
  users$ = this.userService.getUsers();
  
  constructor(private userService: UserService) {}
}
{{< /highlight >}}

**Enterprise Angular Features:**

- **Angular Universal**: Server-side rendering for SEO and performance
- **Angular PWA**: Progressive Web App features with service workers
- **Angular Elements**: Custom elements for micro-frontends
- **Schematics**: Code generation and project scaffolding
- **Workspace**: Multi-project development with shared libraries
- **Ivy Renderer**: Modern rendering engine with tree-shaking

Angular's comprehensive ecosystem and opinionated architecture make it particularly suitable for large enterprise applications where consistency, maintainability, and developer productivity are key concerns.

## External Links

- [Angular Documentation](https://angular.io/docs) @ Angular
- [Angular CLI](https://angular.io/cli) @ Angular
- [RxJS Documentation](https://rxjs.dev/) @ RxJS
