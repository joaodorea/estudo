# Resumo sobre o curso de Angular 2+

Conteúdo:

1. [Overview](#overview):
    - Modules Intro
    - Components Intro
    - Services & Dependency Intro

2. [Components & Templates](#components-and-templates):
    - Template Syntax
    - Lifecycle Hook
    - Component Interaction
    - Dynamic Component
    - Interactions
    - Directives
    - Pipes
    - Animations

3. [Forms](#forms):
    - Template driven
    - Reactive Forms
    - Form Validation
    - Dynamic Forms

4. [Observables & RxJS](#observables-and-rxjs)

5. [Styling](#styling)

6. [NgModules](#ngmodules)
    - Providers
    - Singleton
    - Lazy Load
    - Sharing NgModules

7. [Dependency Injection](#dependency-injection)

8. [HttpClient](#httpclient)

9. [Routing & Navigation](#routing-and-navigation)

10. [Testing](#testing)

11. [Angular CLI](#angular-cli)


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

## Forms

## Objservables and RxJS

## Styling

## NgModules

## Dependency Injection

## HttpClient

## Routing and Navigation

### Basics
The first step to use routers is import the RouterModule, and in declarations use the .forRoot() method to especifie an Array of Objects.
The Objects has an obligated property: 'path' that accepts a string containing the URL route, the orders of the objects (path) matters. After especifing a path, we need to especifie the component to be loaded, ou the path to be redirected to. In case we want a generic path, we can use path: **, so any path that doesn't math the previously ones, will trigger the ** path.
After the configuration of the for.Root() method, we use the sintax <router-outlet> on the view we want to load the paths.
To trigger the RouterModule system we need to use the routerLink attribute to load the component.
It's always a good pratice to use the routers outside the main module.

- Define Base Path
    - 'app/index.html'
- Import Router (RouterModule)
    - .forRoot([...]) - used only once, declares router directives
    - .forChild() - declares router directives, used in feature modules
- Configure Routes
    - [{ path: 'url', component: ComponentName[, pathMatch: 'full'] },...] - case sensitive, don't start with '/', the orders matters
- Place Template
    - <router-outlet></>
    - [routerLink]="['/pathUrl']" == routerLink="/pathUrl"
- Activate Routes
    - Import the Router service
    - Add the dependency in the constructor
    - use the methods avaliable by the service

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



## Testing

## Angular CLI

### Install Globally
```javascript
npm install -g @angular/cli
ng new my-new-app
cd my-new-app
ng serve
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
ng build
ng build --prod # production build
ng build --prod -aot # production plus ahead of time, removes the template compiler 
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
