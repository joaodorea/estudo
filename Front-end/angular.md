# Resumo sobre o curso de Angular 2+

Conteúdo:

1. [Overview](#overview):
    - Modules
    - Components
    - Services & Dependency

2. [Components & Templates](#components-and-templates):
    - Template Syntax
    - Lifecycle Hook
    - Component Interaction
    - Dynamic Component
    - Directives
    - Pipes
    - Animations

3. Forms:
    - Template driven
    - Reactive Forms
    - Form Validation
    - Dynamic Forms

4. Observables & RxJS

5. Styling

6. NgModules
    - Providers
    - Singleton
    - Lazy Load
    - Sharing NgModules

7. Dependency Injection

8. HttpClient

9. Routing & Navigation

10. Testing

11. [Angular CLI](#angular-cli)


## 1. Overview

    ### Modules

    Estrutura básica
    ```bash
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

    ### Component
    
    Para criar um component
    ```bash
    ng g c nome-do-component
    ```
    
    Estrutura básica
    ```bash
    import { Component } from '@angular/core';
    @Component({
        selector:'app-required',
        styleUrls:['required.component.scss'],
        templateUrl:'required.component.html',
    })
    export class RequiredComponent{}
    ```

    ### Pipes (wip)

## 2. Components and Templates

    ### Changing page Title
    ```bash
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

## 11. Angular CLI

    ### Install Globally
    ```bash
    npm install -g @angular/cli
    ```

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
    ```bash
    ng build
    ng build --prod # production build
    ng build --prod -aot # production plus ahead of time, removes the template compiler 
    ```

    ### Unit Testing
    ```bash
    ng test
    ```

    ### BoilerPlate
    ```bash
    git@github.com:CypherTree/angular4-boilerplate.git
    cd [...]
    npm install
    npm start
    ```
