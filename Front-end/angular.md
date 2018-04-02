# Resumo sobre o curso de Angular 2+

Conteúdo:

1. [Overview](#overview):
    - Modules Intro
    - Components Intro
    - Services & Dependency Intro

2. [Components & Templates](#components-and-templates):
    - Template Syntax
    - Lifecycle Hook
    - Directives
    - Component Interaction
    - Dynamic Component

3. [Services](#services)

4. [Forms](#forms):
    - Template driven
    - Reactive Forms
    - Form Validation
    - Dynamic Forms

5. [Observables & RxJS](#observables-and-rxjs)

6. [Styling](#styling)

7. [NgModules](#ngmodules)
    - Providers
    - Singleton
    - Lazy Load
    - Sharing NgModules

8. [Dependency Injection](#dependency-injection)

9. [HttpClient](#httpclient)

10. [Routing & Navigation](#routing-and-navigation)

11. [Testing](#testing)

12. [Angular CLI](#angular-cli)


## Overview

### Modules Intro

Estrutura básica
```javascript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
@NgModule({
    imports:      [ BrowserModule ],    # Modules externos
    providers:    [ Logger ],           # Serviços
    declarations: [ AppComponent ],     # Lista de components
    exports:      [ AppComponent ],     # Conteúdo exportado para ser usado em outros modulos
    bootstrap:    [ AppComponent ]      # Root da aplicação
})
export class AppModule { }
```
### Components Intro

### Services


## Components and Templates

Para criar um component
```javascript
ng g c nome-do-component
```

Estrutura básica
```javascript
import { Component } from '@angular/core';
@Component({
    selector:'app-required',
    styleUrls:['required.component.scss'],
    templateUrl:'required.component.html',
})
export class RequiredComponent{}
```

### Template Syntax (WIP)

- Interpolation
- Template Expressions
- Template Statements
- Bindings Syntax
- Property binding
- Attribute, class and style Binding
- Event Binding
- Two-way binding
- Built-in directives
- Built-in attribute directives
- Built-in Structural directive
- Template reference
- Template expression operators

#### Structural Directives (WIP)

Responsible for HTML layout, changes the shape of the DOM, add, remove or manipulate HTML elements.

- *ngFor
- *ngIf
- [ngSwitch]/*ngSwitchCase, *ngSwitchDefault
- [hidden]="boolean"

#### Attribute Directives (WIP)
- [ngClass]="{className: boolean, className2: boolean}" || [ngClass]="FunctionReturnsArray()"
- [ngStyle]="{color: 'red', backgroundColor: 'transparent'}"


### Component Interaction (WIP)

- @Input() varName;
    - To pass data from a parent component to a child component we use the Input decorator.
    ```javascript
    // parents.html
    <child-component [property]="valueToBePassed"></child-component>
    
    //child.component.ts
    import { ..., Input } from '@angular/core'

    export class ChildComponent {
        @Input('newName') property; // this variable will = 'valueToBePassed'
    }
    ```
- @Output() eventName;
- Template Variable
    - We can call a method in a child component class, by passing a template variable to it on its parent and then calling the method/property.
    ```javascript
    // parent.html
    <child-component #var></child-component>
    <button (click)="var.method()"></button>

    // child.component.ts
    export class ChildComponent {
        //...
        method() {
            /...
        }
    }
    ```

### Lifecycle Hook
- OnChanges
    - One or more of the component or directive properties have been changed
- OnInit
    - Component or directive properties have been initialized
    - Before those of the child directives
- OnDestroy
    - The instance of a component or directive is destroyed
- AfterContentInit
    - After the initialization of the content has finished
    - After OnInit
- AfterContentChecked
    - After the view has been fully initalized
    - Only for components
- AfterViewInit
    - After initializing both component view and any of its child views
- AfterViewChecked
    - After the check of the view has finished
    - Only for components
- DoCheck
    - Listen to changes on specified properties


## Services

A service is a class we export and can be shared with others components, and injected into others services. To use it we just need to especifie it on the providers array in the module, and then in the component we want to use its methods and properties.
@Injectable() is required when we inject a service, that gets others services as dependencies

Basic Structure:
```javascript
// name.service.ts
import { Injectable } from '@angular/core';

@Injectable()
export class NameService {
  constructor() { }
  /* Methods and properties */
}
```

```javascript
// Component
import { NameService } from './location/name.service.ts'
export class ComponentName {
    constructor(private refName: NameService) {} // Shothand call
}
```


## Forms


## Objservables and RxJS


## Styling


## NgModules


## Dependency Injection


## HttpClient


## Routing and Navigation

### Basics
A router is used to load a component without reloading the entire page, this process can make the navigation really fast.
The first step to use routers is import the RouterModule, and in declarations use the .forRoot() method to especifie an Array of Objects.
The Objects has an obligated property: 'path' that accepts a string containing the URL route, the orders of the objects (path) matters. After especifing a path, we need to especifie the component to be loaded, ou the path to be redirected to. In case we want a generic path, we can use path: **, so any path that doesn't math the previously ones, will trigger the ** path.
After the configuration of the for.Root() method, we use the sintax <router-outlet> on the view we want to load the paths.
To trigger the RouterModule system we need to use the routerLink attribute to load the component.
It's always a good pratice to use the routers outside the main module.

- Define Base Path
    - 'app/index.html' after the head tag
    ```javascript
    <base href="/">
    ```
- Import Router (RouterModule)
    - .forRoot([...]) - used only once, declares router directives
    - .forChild() - declares router directives, used in feature modules
- Configure Routes
    - [{ path: 'url', component: ComponentName[, pathMatch: 'full'] },...] - case sensitive, don't start with '/', the orders matters
- Place Template
    - <router-outlet></router-outlet>
    - [routerLink]="['/pathUrl']" == routerLink="/pathUrl"
- Activate Routes
    - Import the Router service
    - Add the dependency in the constructor
    - use the methods avaliable by the service
- RouterLinkActive
    - The Directive for adding/removing classes from an HTML element when an associated routerLink becomes active/inactive

```javascript
// component.html
routerLinkActive="active"                           // if this route is active the element will get the class 'active'
[routerLinkActiveOptions]="{exact: true}"           // (Optional) Only activated when the link match the exact path
```

### Feature Router
We use the .forChild([]) method instead of .forRoot([])
We need to be sure to do not import the services again
To use the router navigation on the component ts file, we need to import the Router, call it in the constructor, and then use the code:
```javascript
this.router.navigate(['/url-name']); // standard syntax
this.router.navigate('/url-name'); // short-cut syntax
this.router.navigateByUrl('/url-name'); // Complete url path
```
Any router definitions that are explicity configured in a external module are processed last. Always be careful with the '**' syntax, it needs to be called last.

- Import Router
- Configure Routes
- Activate Routes

### Route Parameters
To populate the router we can use the navigate methodt o pass more parameters to the array: this.router.navigate(['/url-name', 'parameter'])
To read a router parameter we need to import the ActivatedRoute, call it in the constructor, and then use the snapshot method or the observable. The snapshot reads the initial value of the params and has simpler code
```javascript
let id = this.routeService.snapshot.params['param'];
```
Or the observable method to read the value and listen to its changes:
```javascript
this.routeService.params.subscribe(
    params => {
        let id = params['id'];
    }
)
```
The optional params are passed as objects in the navigation and read as normal params. The queryParams is passed as [queryParams]="{key: 'value'}" in the template file and to maintain them when accessing other pages, we need to use the [perserveQueryParams]="true"
(v4+ queryParamsHandling = 'preserve').
To use the queryParams on the component ts file, we need to pass them as arguments of the navigate method:
```javascript
this.route.navigate(['/url-name'], {
    queryParams: { filterBy: 'er', showImage: true }
})
```

### Prefetching Data

Wait to retrive data before routing to the component, Prevents Display of a partial page, reuses code and imporves flow.
The app waited until the route was activated to fetch the respective data. This method allows us to handle errors before routing to the component. It's preferable to pre-fetch data from server so ir's ready the moment the route is activated. we do this using a *resolver*.

### Guards

- CanActivate
    - Used to restrict the access of the user to a determinated area.
    - Usually the user need to be authenticated or have a specific role.
- CanActivateChild
    - Used to protect a child route.
    - Similar to CanActivate. The key diference is that it runs before any child route is activated
- CanDeactivate
    - Prevent the user to leave the page.

### Lazing Loading

When a route is activated, we will load a module containing the routing and the component of that route. This technic is used to load those informations only when its necessary, speeding up load time.
To do that, we need to create a new module and a new routing to that route. We need to remember to use the .forChild() method in the Feature Module's RouterModule.

```javascript
// parent module
{path: 'routePath', loadChildren: 'path/to/the/module#NameOfModule'}, // On the routes const
```

### [Reference](https://angular.io/guide/router#summary):
Router Parte            | Meaning
----------------------  | ----------------------
Router                  |  	Displays the application component for the active URL. Manages navigation from one component to the next.
RouterModule            |  	A separate NgModule that provides the necessary service providers and directives for navigating through application views.
Routes                  |  	Defines an array of Routes, each mapping a URL path to a component.
Route                   |  	Defines how the router should navigate to a component based on a URL pattern. Most routes consist of a path and a component type.
RouterOutlet            |  	The directive (<router-outlet>) that marks where the router displays a view.
RouterLink              |  	The directive for binding a clickable HTML element to a route. Clicking an element with a routerLink directive that is bound to a string or a link parameters array triggers a navigation.
RouterLinkActive        |  	The directive for adding/removing classes from an HTML element when an associated routerLink contained on or inside the element becomes active/inactive.
ActivatedRoute          |  	A service that is provided to each route component that contains route specific information such as route parameters, static data, resolve data, global query params, and the global fragment.
RouterState             |  	The current state of the router including a tree of the currently activated routes together with convenience methods for traversing the route tree.
Link parameters array   |  	An array that the router interprets as a routing instruction. You can bind that array to a RouterLink or pass the array as an argument to the Router.navigate method.
Routing component       |  	An Angular component with a RouterOutlet that displays views based on router navigations.


## Testing


## Angular CLI

### Install Globally

```javascript
npm install -g @angular/cli
ng new my-new-app
cd my-new-app
ng serve
```
To change the deafult ports
```javascript
ng serve --port 4201 --live-reload-port 49153
```

Descrição   |   Comando
------------ | -------------
[Component](https://github.com/angular/angular-cli/wiki/generate-component) | `ng g component my-new-component`
[Directive](https://github.com/angular/angular-cli/wiki/generate-directive) | `ng g directive my-new-directive`
[Pipe](https://github.com/angular/angular-cli/wiki/generate-pipe)           | `ng g pipe my-new-pipe`
[Service](https://github.com/angular/angular-cli/wiki/generate-service)     | `ng g service my-new-service`
[Class](https://github.com/angular/angular-cli/wiki/generate-class)         | `ng g class my-new-class`
[Guard](https://github.com/angular/angular-cli/wiki/generate-guard)         | `ng g guard my-new-guard`
[Interface](https://github.com/angular/angular-cli/wiki/generate-interface) | `ng g interface my-new-interface`
[Enum](https://github.com/angular/angular-cli/wiki/generate-enum)           | `ng g enum my-new-enum`
[Module](https://github.com/angular/angular-cli/wiki/generate-module)       | `ng g module my-module`

### Build the project
```javascript
ng build == ng build --dev  // developer build
ng build --prod             // production build
ng build --prod -aot        // production plus ahead of time, removes the template compiler 
```

### Unit Testing
```javascript
ng test
```

### BoilerPlate
```javascript
git@github.com:CypherTree/angular4-boilerplate.git
cd [...]
npm install
npm start
```

### Using pre-processor
```javascript
// For a new Project
ng new my-project --style=sass
ng new my-project --style=less
ng new my-project --style=stylus

// For existing project
ng set defaults.styleExt scss
ng set defaults.styleExt less
ng set defaults.styleExt styl
```

***
## Others

### Changing page Title
```javascript
import { Title } from "@angular/platform-browser";
@Component({
    selector:'app',
    templateUrl:'./app.component.html',
    providers:[Title]
})
export class AppComponentimplements {
    constructor(private title:Title){
        this.title.setTitle('page title changed');
    }
}
```


References:
Angular 2 - Notes for professional
Angular Routing by: Deborah Kurata (Pluralsight)

App references:


More about Angular +2:
https://angular.io/guide/
