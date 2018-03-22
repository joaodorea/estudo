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
