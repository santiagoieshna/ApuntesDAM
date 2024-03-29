# App.component
Un componente esta formado por varias partes que ya vimos en el [[02 Explicación de cada archivo#app|directorio app]], y estos son los archivos app.component.\*.

1. _app.component.css_ : Archivo para CSS

2. _app.component.html_: Archivo para HTML

3. _app.component.spec.ts_: Archivos de pruebas (.spec o .test para testing)

4. _app.component.ts_ ___A___: Archivo ts, el mas importante. Explica como funciona el componente, que dependencias tiene etc. Los demás son digamos que formas para que no todo estuviera dentro de este (Mejor legibilidad).


En el archivo .ts viene definido cada uno de los archivos:

```ts title='app.component.ts'
import { Component } from '@angular/core';
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrl: './app.component.css'
})
export class AppComponent {
  title = 'bases-angular';
}
```

_@Component_ -> Decorador typescript para angular. tiene varias propiedades:
_templateUrl_: es la sección para el archivo html.
_styleUrl_: es la sección para el archivo CSS.

También podemos definir en el propio archivo el html y CSS con las propiedades:
_template_: Para insertar el HTML
_style_: Para definir el CSS.

_selector_: 'app-root', -->  Si nos vamos al index.html del proyecto veremos que: 

```html hl:11 title='index.html'
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>BasesAngular</title>
  <base href="/">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
</head>
<body>
  <app-root></app-root>
</body>
</html>
```

La línea 11 tiene la etiqueta app-root, ahí es donde se renderiza el componente o modulo de angular.

## app.component.html

En este archivos podemos insertar variables de Typescript, este mecanismo se llama [[04 Interpolación|interpolación]], para ello vamos a modificar un poco el archivo .ts:

```ts title='app.component.ts'
import { Component } from '@angular/core';
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrl: './app.component.css'
})
export class AppComponent {
  title = 'bases-angular';
  public variable:string = 'Cervantes era una pájaro'
}
```

Ahora vamos a borrar el html y le ponemos solo un `{html}<h1>` y un `{html}<p>`

```html title='app.component.html'
<h1> {{variable}} </h1>
<hr>
<p>
  Bienvenidos a mi aplicación
</p>
```

Y si [[02 Paquete @angular_cli#Levantar servidor|levantamos]] el servidor, veremos los cambios:

![[ts-en-html.png]]

# Componente

Por convención un componente tendrá el nombre:
`{python}nombreComponente.component.extension`

_Ejemplo_: usando HTML interno sin CSS.

```ts title='counter.component.ts'
import { Component } from '@angular/core';
@Component({
    selector: 'app-counter',
    template: `
            <h1>Hola</h1>
            <button (click)="incrementar()">1</button>
            <button (click)="reset()">Reset</button>
            <button (click)="decrementar()">-1</button>
            <h2>{{contador}}</h2>`
})
export class CounterComponent {
    public contador : number = 0;
    incrementar():void{
        this.contador ++;
    }
    decrementar(): void{
        this.contador --;
    }
    reset():void{
        this.contador = 0;
    }
}
```

Una vez creado cualquier componente, queremos verlo como es evidente.

Para ello lo llamaremos en app.component, ya que es nuestro punto principal de partida para visualizar la aplicación.

Llamaremos al componente en el HTML.

```html hl:6 title='app.component.html'
<h1> {{ variable }} </h1>
<hr>
<p>
  Bienvenidos a mi aplicación
</p>
<app-counter></app-counter>
```

Si guardamos y el servidor esta [[02 Paquete @angular_cli#Levantar servidor|levantado]] arroja error. Pues para que un componente sea visible tiene que esta importando en _app.module.ts_.

### app.module.ts

Este archivo tendrá el registro de los componentes que han sido utilizados en su componente. 

En el importaremos la Clase de CounterComponent y lo declararemos en el Decorador _@NgModule_:

```ts hl:6,11 title='app.module.ts'
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { CounterComponent } from './counter/counter.component';

@NgModule({
  declarations: [
    AppComponent,
    CounterComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})

export class AppModule { }
```

Una vez hecho esto ya funciona nuestra aplicación (reiniciar server o vsCode si persiste el error, si no, algo hiciste mal prro).
## Directorios

Una convención es por cada Componente o Modulo tener una carpeta.

Ejemplo de los directorios del ejemplo de [[02 Paquete @angular_cli#Generar componentes|heroes]]. 

![[directorios-estructura-components.png]]


