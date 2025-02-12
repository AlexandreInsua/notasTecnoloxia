# ANGULAR

## 1. Introdución

Angular é unha plataforma de desenvolvemento (ou framework de frontend) construído en [Typescript](https://www.typescriptlang.org/). Angular estrutúrase en **components** (ficheiros typescript .ts) e **templates** (ficheiros html).
Un **component** e un bloque de codigo ts que inclúe unha clase e o decorador `@Component()` que especicifica un selector, un template e opcionalmente unha folla css.
Unha **template** inclúe codigo html, variables interpoladas (interpolation con `{{variable}}`), e vencelladas (property bindind con `[property]="value`), eventos vingulados (event binding con `(event)="funcion()"`), e directivas.
Angular funciona mercé ao principio de **inxección de dependencias** en virtude da cal se declaran esas dependencias correndo a súa instanciación por conta da plataforma.
**Angular cli** é unha interface de liña de comamndos propia que permite realizar múltiples accións.
Angular fornece de varias librerías propias como son: o Router, Forms, HttpClient, Animations, PWA, Schematics.

## 2. Angular cli

A interface de liña de comandos de Angular é unha ferramento que se empreggra para iniciar, levantar a estrutura básica, desenvolver e manter aplicaicón Angular desde a liña de comandos.

### 2.1. Instalar o CLI de Angular

Para crear aplicacións de Angular necesitamos instalar a utilidade da liña de comandos. Para isto córrese o seguinte comando

- `$ npm install -g @angular/cli`.

### 2.2. Fluxo de traballo básico

O fluxo de traballo básico consiste en ir crear un proxecto e levantalo nun servidor;

1. `ng new [project name] --prefix [prefix name] --skip-git=true --skip-install=true`. Crea un novo proxecto nun directorio co mesmo nome. O nome de proxecto debe ser válido como nome de directorio. Pódese setear que a utilidade use un prefixo para os seus componentes diferente dos estándar, tamén podemos ignorar a configuración de git e a instalación inicial dos paquetes npm.
2. `cd [project name]`. Cámbiase ao directorio do proxecto.
3. `ng serve`. Levántase un servidor.

### 2.3. Estrutura inicial do proxecto

<!-- TODO: comprobar que pasa na v16 -->

O proxecto está formado polos seguintes elementos:

- `.browserslistrc`. Configuración de navegadores soportados.
- `.editorconfig`. Configuración do editor de código.
- `.gitignore`. Ficheiro para ficheiros sen seguemento.
- `README.md`. Ficheiro de documentación.
- `angular.json`. Configuración do proxecto de Angular, build, server, e testing.
- `package.json`. Configuración de dependencias de npm e scripts npm.
- `package-lock.json`. Información das versións de `node_modules/`
- `src/`. Directorio de código fonte. Contén os seguites elementos:
  - `app/`. Contén os ficheiros das compoñentes da aplicación.
    `assets`. Contén ficheiros estáticos como imaxes e outros.
    `enviroment`. Contén a configuración para un entorno. En xeral dev e pro.
    `favicon.ico`.
    `index.html`. Punto de entrada da app. Chama os js compilados que se xeran no `build`.
    `polyfills.ts`. Fornece os scripts de polyfill para soporte de navegadores.
    `styles.css`. Folla de stilos globais.
    `test.ts`. Punto de entrada para os test unitarios.
- `node_modules/`. Paques de npm.
- `tsconfig.json`. Configuracón de typescript.
- `tslint.json`. Configuración de linter.

Dentro do directorio `src/app/` encóntrase a lóxica da app. Por defecto créase o compoñente principal da app que ten os seguintes ficheiros (o resto de compoñentes seguen a mesma estrutura):

- `app.component.ts`. Lóxica para o compoñente.
- `app.component.html`. Template html do compoñente.
- `app.component.css`. Folla de estilos asociada.
- `app.component.spec.ts`. Test unitarios.
- `app.module.ts`. Módulo da aplicación, configura os elementos que forman a app.

### 2.4. Lista básica de comandos

Esta é a lista dos comandos principais de angular. Todos admiten unha flag `--help` que mostra o manual.

| Comando     | Alias | Flags                                                     | Descrición                                         |
| ----------- | ----- | --------------------------------------------------------- | -------------------------------------------------- |
| ng add      |       |                                                           | Engade unha libraría externa ao proxecto           |
| ng build    | b     |                                                           | Compila a app para o seu despregue                 |
|             |       | --aot                                                     | Activa o modo aot                                  |
|             |       | --base-href                                               | modifica a base da url de deploy (./ para windows) |
|             |       | --dev                                                     | Compila para desenvolvemento                       |
|             |       | --prod                                                    | Compila para produción (deprecada)                 |
|             |       | --output-hashing none                                     | quita o número de hash nos ficheiros compilados    |
| ng e2e      | e     |                                                           | Corre os test                                      |
| ng doc      | d     |                                                           | Mostra a documentación da api de anguar            |
| ng generate | g     | c(component) , s(service) , m(odule), p(ipe), d(irective) | Xera ou modifica ficheiros                         |
| ng help     |       |                                                           | Lista os comandos dispoñibles                      |
| ng new      |       |                                                           | Crea o scalfolding do proxecto                     |
| ng serve    | s     |                                                           | Contrúe e serve a app en tempo real                |
|             |       | --check-host=enabled / disabled                           | habilita / deshabilita a comprobación do porto     |
|             |       | --host=localhost                                          | establece o host                                   |
|             |       | --port=0000                                               | establece o porto                                  |
| ng test     | t     |                                                           | Corre os test unitarios                            |
| ng version  | v     |                                                           | Mostra a versión de angular                        |

## 3. Módulos e compoñentes

### 3.1. O compoñente

En Angular un compoñente é un conxunto de recursos que se relacionan cun elmento visual da web. Considérase unha boa práctica buscar que os compoñentes sexan o máis pequenos e reusables que sexa posible. En Angular o compoñente típico estár formado por html, os estilos e on controlador en typescript. A estruura básica deste constrolador é a seguinte:

- **Importacións**. Permiten importar funcionalses e librarías para o funcionamento do compoñente. Com mínimo vaise importar a definición de liabraría de Anglular:
  `import { Component } from '@angular/core';`
- **Configuración do compoñente**. A configuración consiste en especificar os atributos que sexan necesarios para o seu funcionamento a través da directiva _Component_. Esta directiva recibe como parámetro un obxecto de configuración que pode recibir diferentes propieades:
  - **selector**: define a etiqueta html que se vai usar noutras partes da aplicación para invocar o compoñente.
  - **template**: string que contén o html do compoñente ou
  - **templateUrl**: ruta ao ficheiro html
  - **styles**: string coa definición de estilos do compoñente ou
  - **stylesUL**: array de strings de rutas que definen os stilos do compoñente
  - **directives**: define as directiva que se van usar o compoñente
  - **pipes**: define as pipes que se necesitan no compoñente.
  - **providers**: define os servizos que se necesitan usar no compoñente. Se o compoñente están incluído nun módulos, decláranse ntes.
  <!-- TODO: ver como queda con stand alone componet-->
- **Espeficiación do compoñente**. Define e exporta unha clase que define a lóxica de negocio.

Os compoñentes poden crearse co comando `ng generate component [name] [path] --module? --standalone?`. Cando se crea un compoñente seguindo a programación modular, agrégase nas declarations do módulo correspondente, pero para poder usalo fóra do módulo hai que agregalo manualmente ás exports.

### 3.2. Os compoñentes standalone

Un compoñente pode estar defindio sen necesidade de agegalo a ningún módulo. Na configuración do compoñente establécese a propiedade standalone a true:

```typescript
@Component({
	standalone: true,
	selector: 'my-component',
	templateUlr: ['./my-component.component.html'],
	stylesUlr:['./my-component.component.css']
})
```

A partir de aí pode usarse en calquera punto da aplicaión mediante o selctor. No caso de necesitar importar outro compoñente ou módulos neste tipo de compoñentes, úsase a propiedade imports:

```typescript
@Component({
	standalone: true,
	selector: 'my-component',
	templateUlr: ['./my-component.component.html'],
	stylesUlr:['./my-component.component.css'],
	imports: [OtherComponent, OtherModule, OtherService]
})
```

### 3.3. O módulo

Un módulo é un elemento superior que agrupa varios compoñentes e outras pezas de código. É un xeito de agrupar pezas de código (compoñentes, servizos, directivas ou pipes)
(**NOTA**: A partir da v14 son opcianais. A alternativa é unha aplicación sen módulos).
Angular non sxestiona todos os ficheiros ao mesmo tempo, senón que se ocupa de cada agrupación de maneira separada. Toda aplicación necesita como mínimo un módulo: o _AppModule_. A libraría estándar de Angular proporciona funcionalidades dentro de módulos como o _FormModule_ ou o _HttpClient_.

A estrutura básica dun módulo de Angular é a seguinte:

- **importacións**: Importa as funcionalidades, librerías e servizos que necesitamos utilizar nos compoñentes do módulo. Como mínimo inpor a directiva de definición do módulo **ngmodule**:
  `import { NgModule } from '@angular/core';`
- **configuración do módulo**: O decorador **NgModule({...})** recibe un obxecto de configuración coas seguintes propiedades:
  - **imports**: Importa outros módulos para usalos no contexto do módulo.
  - **exports**: Exporta as directivas e compoñentes que se poden unsar noutros módulos.
  - **declarations**: Declara compoñentes, directivas e pipes personalizadas que van usar os compoñentes do módulo.
  - **providers**: Declara os servizos e pipes que se usan no módulo.
  - **boostrap**: Atributo especial que define o módulo desde o que se vai empezar a cargar a aplicación.
  - **entryComponents**: Array onde se declaran os compoñentes que podden ser creados dinamicamente (especialmente usados para cadros de diálogo).
- **implementación**. Decláráse unha clase valeira:

```Typescript
export class MyModule {}
```

Por comvención hai un módulo inicial denominado `AppModule` que declara o compoñente inicial e a configuracion de inicio. Ademais tamén se soe incluír outr modulo para xestionar as rutas, denominado `AppRouterModule`. Necesita as dependencias RouterModule e Routes.

Os módulos creánse co comando `ng generate module [name] [path]`

#### 3.3.1. Uso de módulos

Os módulos que se importan nun módulo só funcionan dentro dese módulo, non se comparten. Por exemplo, se queremos usar un router-outlen nun módulo para xestionar rutas fillas, hai que improtan o RouterModule no módulo da características quea que recoñezan a directiva, caso contrari, pintará un erro. O mesmo aplica pra os módulos e formularios. A excepcción a esta regra son os servizos configurados no AppModule porque se fornecen na raíz do proceso.

#### 3.3.2. Módulos de rutas

Os módulos de rutas son módulos que xestionan as rutas e que se importa no módulo principal da funcionalidade. !! Hai que comprobar se as exportaciósn de elementos son realmetne necesarios nos módulos das funcionalidades.

#### 3.3.3. O módulo comportatido (shared)

Un módulo compoartido ten como finalidade evitar código duplicado. Neste módulos hai que exportar todo o que se importa ou declara para habilitar o acceso a estas funcionalidade alá onde se importa o módulo. Hai que ter en cota que os compoñentes, directivas, e Pipes só se poden declarar nun único módulo. Non se poden declarar o mesmo elemento en varios módulos.

#### 3.3.4. O módulo central (core)

O módulo central (core) ten como finalidade alixeirar o AppModule. Podemos mover servizos que non teñen que ser servidos na raíz da aplicación. Despois hai que importalo no AppModule.

#### 3.3.5. Lazy loading

O concepto de lazy loading consiste en cargar os módulos en función da navegación. Cando se carga a ruta principal, só se carga o AppModule e descargamos o código a medida que o vaiamos necesitando, así o inicio da aplicación é máis rápido.

Para usar a carga dinámica o módulo quen te xestionar as súas rutas, pque require facer unha adaptación para evitar un conflito de rutas. No módulo de rutas correspondente hai que setear unha ruta raíz con string valeiro que carga o compoñente pai dese módulo e no módulo de rutas principal da aplicación que se setar una ruta co path orixinal e carga o lazy loadingd. Este obxecto de rutas non carga un compñente, senón que usa a propiedade loadChildren para cargar o módulo cando se visita a páxina. A ruta quedaría así:

`{ path: 'about', loadChildren: './about/about.module', AboutModule }`

Hai que especificar o módulo.

Existen unha nova sintaxe para establecer isto. A propiedade `loadChildren` recibe unha función anónima de callback que executa un import dinámico. Este import dinámico devolve unha promesa que recibe un módulo que é o que se carga:

`{ path: 'about', loadChildren: () => import('./about/about.module').then(m => AboutModule) }`

O módulo lazy xan non se carga no móduloda aplicación. A carga lazy ten como desvantaxe unha certa demora para evitalo pódese setear unha pre carga no módulo aplicación así:

```
@NgModule({
	...
	imports: [RouterModule.forRoot(routes, { preloadStrategy, PreloadAllModules})]

})
```

#### 3.3.6. Servizos e módulos

Os servizos poden ser proveídos no AppModul, nos compoñentes, nos eager modules, nos lazy modules ou no obxecto de configuración do decorador @Injectable.
Cando se provee no AppModule ou en root, créase unha única instancia para toda a aplicación. En troca se se provee nun compoñente creará una instancia para esa xerarquía pero se se provee en varios compoñentes irmans crearase cadansúa instancia.
Se se proveen nun ou varios módulos eager creará unha única instancia porque están no bundle inicial, pero se se provee nalgún lazy module, non se inclúe dentro la bundle inicial, polo que se crearán varias instancias diferentes.

#### 3.3.7. Compoñentes dinámicos

Os compoñentes dinámicos son aqueles que se crean en tempo de execución, como por exemplo os modais e os toast. Hai que entender que dinámico quere dicir que non está non DOM inicialmente pero a raíz dun evento créase e insírese no DOM. Para isto temos varias aproximacións:

1. Usar a directiva \*ngIf. O Compoñente será incrustado mediante o selector (aproximación declarativa).
2. Cargar o compoñente desde o código. Implica crealo e inserilo no DOM mediante código. Necesitamso un método privado que o xestione desde o compoñente principal. En versións anteriores á 9 habia había que agregar o compoñetne dinámcio no módulo da aplicación como entryComponent (aproximación imperativa).

### 3.4. O ciclo de vida dos compoñentes

O ciclo de vida dos compoñents define os diferntes estados intermedios polos que pasa desde que se crea e se carga ata que se destrúe. Neses estados realizar accións a traves de eventos asociados. Son os seguintes:

- **ngOnChanges**. Este evento Execútase cada vez que se detecta cambios no compoñente, e antes de OnInit e OnCheck. Crea un obxecto cos valores previos e os actuais.
- **ngOnInit**. Execútase unha vez ao iniciarse o compoñente e só se executa unha vez. Non ten acceso ao DOM porque aínda non está cargado.
- **ngDoCheck**. Execútase despois de OnChanges e produce un obxecto cos novos valores pero non cos anteriores. Non se debe usar xunto con OnChanges.
- **ngAfterContentInit**. Execútase cando unha vez despois de se remate de iniciar o compoñente.
- **ngAfterContentChecked**. Execútase despois de que se chequee os cambios no compoñentes.
- **ngAfterViewInit**. Execútase de inicializar a vista do compoñente, cando se cargan view e viewchild.
- **ngAfterViewChecked**. Execútase despois de cada chequeo da vista do compoñente, cando se modifica view e viewchild.
- **ngOnDestroy**. Execútase inmediantemente antes de que se destrúa o compoñente.

Para configurar un evento impórtase a interface que manexa o evento:

`import { Component, OnInit } from '@angular/core';`

e despois impleméntase a interface:

```typescript
export class MyComponent implements OnInit {
  ngOnInit() {
    //....
  }
}
```

## 3B. Aplicacións sen módulos

A estruturación en módulos achega a Angular unha grande modularidade mais presenta como contraparte bastante código repetitivo. Ademais, a medida que os módulos se van reproducindo diminúe a covertura de test porque son meras importacións e exportacións.
Outros frameworks non usan algo como módulos polo que Angular ten unha desvantaxe. O elementos autónomos (standalone) intentan superar isto. O compoñentes standalone teñen unha flag no obxecto de configuración do compoñente onde o valor por defecto é false, daquela:

```typescript
@Component({
 standalone: true,
 selector: "app-home",
 templateUrl: "./home.component.html",
 styleUrls: ["./home.component.css"]
})
```

Un compoñente autónomo **non** pode ser declarado dentro dun módulo. Cando se migra un compoñente a un autónomo hai que ter ollo se é usado noutro compoñente se é usado notro compoñente. O consumidor non saberá onde buscalo, polo que hai que dicirllo mediante a propiedade imports no obxecto de configuración onde do importará (tamén pode importar módulos):

```typescript
import { DetailsComponent } from "./details.component";

@Component({
 standalone: true,
 imports: [DetailsComponent]
 selector: "app-home",
 templateUrl: "./home.component.html",
 styleUrls: ["./home.component.css"]
})
```

Pero isto só funcionará se o consumidor é tamén un compoñente standalone. Se non o é a solución transitoria é importar o compoñente no módulo correspondente. Se o _home.component_ non fose a propiedade standalone o módulo quedaría tal que así:

```typescript
@NgModule({
 declarations: [AppComponent, MainComponent],
 imports: [BrowserModule, DetailsComponent],
 boostrap: [AppComponent]
})
```

O mesmo ocorre coas directivas e as pipes. Poden ser convertidas en standalone coa flag e ser importadas por outros elementos standalone directamente ou ser importadas en módulos de Angular para ser consumidas en compoñentes modulares

A medida que se van transformando os compoñentes dun módulo en standalone este vai quedando máis valeiro e chega un momento en que se pode eleminar.

### 3B.1 O AppComponent

O AppComponent pode ser standalone pero implica un cambio adicionalmente. Com non ode ser declarado no AppModule non se pode usar a propiedade de arranque. Temos que cambiar a inicialización da aplicación e iso faise no ficheiro _main.ts_. Cambia a súa sintaxe para iniciar desde un compoñente en lugar dun módulo:

```typescript
import { enableProModule } from "@angular/core";
import { bootstrapApplication } from "@angular/platform-browser";
import { AppComponent } from "./app/app.component";
import { enviroment } from "./enviroment/enviroment";

if (enviroment.production) {
  enableProModule();
}

boostrapApplication(AppComponent);
```

### 3B.2 Servizos e compoñentes standalone

Hai varios esceanarios posibles:

- Cando un servizo ten seteadas a propiedade `provideIn: 'root'` xa é fornecido na raíz da app e pode ser inxectada en calquera compoñente autónomo. Por tanto, non se require facer ningún axuste.
- Caso de o servizo estar declarado no array de providers dun módulo. No compoñente (ou Pipe ou Directive) que usa o servizo póse engadir un array de providers. Como contrapartida, teremos unha instancia por cada declaración do servizo.
- O terceiro escenario é migrar o servizo do array de providers do _app.module.ts_ ao _main.ts_ A función _bootstrapApplication_ ten como segundo parámetro un obxecto de configuración que pode recibir un array de providers tal que:

```typescript
bootstrapApplication(AppComponent, { providers: [MyService] });
```

### 3B.3 Routing e compoñentes standalone

Dado que xa non hai AppModule, hai que habilitar o enrutado doutro xeito. Para isto impórtase o RouterModule no AppComponent (que agora é standalone). O segundo paso é pasarlle as rutas. Isto faiso no _main.ts_, incorporando nos providers a función _importProvidersFrom_ que recibe o módulo de rutas:

```typescript
bootstrapApplication(AppComponent, {
  providers: [importProvidersFrom(AppRoutingModule)],
});
```

Tamén se podes proveer de varlores e servizos para seren usados en toda a aplicación:

```typescript
bootstrapApplication(AppComponent, {
  providers: [
    importProvidersFrom(AppRoutingModule),
    { provide: BACKEND_URL, USEvaLUE: "https://backend-service.com/api/v1" },
  ],
});
```

As funcións con prefixo _provide_ poden seren usadas para configurar diferentes sistemas sen necesidade de importar módulos:

```typescript
bootstrapApplication(AppComponent, {
  providers: [provideRouter([ROUTES])],
});
```

Nas rutas hai que importar os compoñentes (ou módulos antigos) e iso pode facerse sincronicamente ou en modo lazy load:

sincronicamente:

```typescript
{
 path: 'about',
 component: AboutComponent
}
```

lazy load:

```typescript
{
 path: 'about',
 loadComponent: ()=> import('./about/about.component').then( c => c.AboutConmponent)
}
```

Como os módulos de rutas tamén desaparecen, necesitamos cambiar as rutas como unha constante exportada que despois se importa no AppRoutingModules:

```typescript
{
 path: 'dashboard',
 loadComponent: ()=> import('./dashboard/routes').then( r => r.DASHBOARD_ROUTES)
}
```

Se un routing module ten rutas fillas, o compoñente principal debe importar o router module para saber como xestionalas, porque está usando a directiva routerLink no html que esta definida nese módulo.

### 3B.4 varios

Se unha libraría de tercieros non foi actualizada para implementar unha función provide pódse usar a función importProvidersFroms para implamentala:

```typescript
import { LibraryModule } from "ng-moudule-based-library";

{
  bootstrapApplication(AppComponent, {
    providers: [MyService, importProvidersFrom(LibraryModule.forRoot)],
  });
}
```

### 3B.5 Referencias

Hai dúas guías de developing. Para facer a migración hai un schematics:
`ng generate @angular/core:standalone`

## 4. Enlazado de datos

### 4.1. Data binding (enlazado de datos) en Angular

Un compoñente está composto dunha template (patrón) HTML + CSS que se considera como a vista e un modelo e controlador que interactúan entre si mediante o enlazdo de datos (data binding), que é a técnica que conecta os dtos do modelo coa vista a través do controlador. Existen tres tipos de data binding.

#### 4.1.1. Property binding

Dado o seguinte código:

_hi-world.component.html_

```html
<div>Ola {{ userName }}</div>
<div>Ola <span [innerHtml]="userName"></span></div>
<button disabled="{{changed}}"></button>
<button [disabled]="changed"></button>
```

_hi-world.component.ts_

```typescript
import { Component } from '@angular/core';

@Component({
	selector: 'hi-world',
	templateUrl:: 'hi-world.component.html'
})
export clase HiWorldComponent {
	userName = "Alexandre";
	changed = false;
}
```

Este código ten como saída:

```
Ola Alexandre!
Ola Alexandre!
[botón desactivado] [botón activado]
```

Como se pode ver, hai dúas formas de declarar un property binding.

- {{expresión}}: coa sintaxe da sobre chave estamos asociado unha variable declarada no compoñente coa template.
- [propiedade]="expresión": coa sintaxe asociamos o valor dunha expresión cunha propidade do elemento html, da etiqueta.

#### 4.1.2. Atributos e propiedades

Un **atributo** forma parte da propia etiqueta, do elemento html, mentres que unha **propiedade** forma parte do obxecto correspondente no DOM. Dánse os seguintes casos:

- Relación 1:1 entre atributos e propiedades, como o id dun elemento, que existe como atributo da etiqueta o como propiedade do obxecto.
- Propiedades sen atributo, como o textContent.
- Atributos se propiedade, como colspan.
- Atributo que inicializa unha propiedade pero non a actualiza. Son a maior parte de casos.

O caso máis común é o de un atributo que fixo o valor inicial da propiedade con elemento do DOM pero que están desconectados, por exemplo o value dos input, que se inicializa co valor da etiqueta e se actualiza cos cambios no input.

O resultado do template anterior é

```html
<button disabled="false"></button> <button></button>
```

No primeiro caso, o atributo disabled fai caso omiso do valor que se lle asignar. Só con estar presente xa se deshabilita o elemento, polo que por debaixo a propiedade por debaixo ten o valor de true. No segundo caso, asignamos un valor false.

#### 4.1.3. Comunicación entre compoñentes usando o property binding

A property binding tamén se usan para comuncar compoñentes. O caso de uso é pasarlle variables dun compoñente pai a un compoñente fillo. Para isto utilización a sintaxe Pai -> [propiedade fillo]="valor no pai" -> Fillo. Onde especificamos a propiedade dun fillo e a asociamos co compoñente pai:

_componente-pai.component.ts_

```typescript
import { Component } from "@angular/core";
import { ComponenteFilloComponent } from "./component-fillo.component.ts";

@Component({
  selector: "componente-pai",
  template: `<componente-fillo [name]="userName"></componente-fillo>`,
})
export class ComponentePaiComponent {
  userName = "Alexandre";
}
```

_componente-fillo.component.ts_

```typescript
import { Component, Input } from "@angular/core";

@Component({
  selector: "componente-fillo",
  template: `<div>Ola {{ name }}</div>`,
})
export class ComponenteFilloComponent {
  @Input() name;
  string;
}
```

Para especificar que unah variable vai ser enviada desde un compoñente externo, úsase a directiva Input coa sintaxe @Input('alias) nome_da_variable: tipo, onde o alias é opcial e úsase para referise a variable no compoñente pai entre corchetes. Caso de non setearse, úsase o nome da variable.
Se o proxecto tes seteado o modo estrito, esta variable non pose ficar se inicializarse e dará mensaxe de erro. Para solucionar isto hai dúas sintaxes alternativas:

- `@Input name: string | null = nul;` para o caso de que poda se nula e
- `@Input name!: string;` para o caso de que nunca sexa nula.

#### 4.1.4. Event binding

É unha técnica que consiste en asociar un evento e unha expresión, de xeito que conectamos a template co compoñente. Sexa o seguinte código:

_say-hello.component.html_

```html
<button (click)"sayHello($event)" value="Ola!">Di Ola</button>
```

_say-hello.component.ts_

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "say-hello",
  templateUrl: "./say-hello.component.ts",
})
export class SayHelloComponent {
  sayHello(event: Event) {
    alert(event.target.value);
  }
}
```

Neste exemplo asoiacmos un evento de tipo click ao botón. Cando se producza este enento avaliarase a expresión, neste caso, executarase a función. O `$event` é un obxecto que simboliza o elemento do DOM, polo que podemos aceder a eles e interactuar coa súas propiedades. Convencionalmente úsase o signo de dolar ($) **antes** dos nomes de variables ou parámetros para indicrar que apuntan a un elemento do DOM.

#### 4.1.5. Comunicación enter compoñentes mediante event bindind

Para acutalizar o pia coas accións que ocorres no compoñente fillo, farémolo a traves de eventos coa sintaxe Pai <-- (eventoFillo)="listenerPai()" <--Fillo. Sexa o seguinte código.

_componente-pai.component.ts_

```typescript
import { Component } from '@angular/core';
import { ComponenteFilloComponent } from './component-fillo.component.ts';

@Component{(
	selector: 'pai',
	template: `	<div>{{frase}}</div>
				<fillo (eventoFillo)="listernerPai($event)"></fillo>`
)}
export class CompoenentePaiComponent {
	frase = "";

	listenerPai(event): void {
		this.frase = event;
	}
}
```

_componente-fillo.component.ts_

```typescript
import { Component, EventEmiter, Output } from "@angular/core";

@Component({
  selector: "fillo",
  template: `<button (click)="sayHello()">Di ola</button>`,
})
export class FilloComponent {
  @Output() eventoFillo = new EventEmmiter();

  sayHello() {
    this.eventoFillo.emit("Ola");
  }
}
```

Como se pode ver para comunicar os compoñentes temos que usar varias directivas adicionais. No compoñente fillo importamos as directivas Output, que indica que a variable vai "sair" do compoñente e a clase EventEmitter, que permite emitir eventos personalizados.

#### 4.1.6. Enlace bidireccional (two way data binding / banana in the box)

É posible establecer un enlace bidireccional mediante a técnica como Two-way Data Binding que pon a disposición ambas conexión ao mesmo tempo. Un case de uso é actualizar unha variable que se introduce nun input nun formulario. A sintaxe teórica seria

```html
<input [value]="userName" (input)="`userName" ="$event.target.value`" />
```

que se pode reescribir así:

```html
<input [(ngModel)]="userName" />
```

Coa sintaxe [(propiedade)]="expresion" estamos dicindo que se van usar ambos eventos ao mesmo tempo para mostrar a actualizar o valor. Coa propiedade ngModel estamos dicíndolle a Angular que vas usar a propiedade value para que a xestione. Para usal hai que importar o modelo de formularios de Angular (FormModule).

## 5. Pipes

En Angular as pipes permítennos modificar os datos que se van representar na vista e facleas máis lexibles. Non é tanto unha modificación dos datos senón unha máscara. O exemplo típico é a representación das datas. Angular proporciona varias pipes de base:

- Decimal Pipe: formatea números decimais.
- Slice Pipe: extrae un subconxunto dun array ou dun string.
- Currency Pipe: formatea números monetarios.
- Date Pipe: formatea datas

Algunhas destas soporta o uso dun sistema de internacionlización de Angular baseada no uso de "locales" correspondentes. Un localse é un identificador de tipo idioma-rexión. O locale configúrase no app module para facelo de xeito global: `providers: [{ provide: LOCALE_ID, useValue: 'gl' }]`

#### 5.1. Pipes personalizadas

Pódese crear pipes personalizadas. Unha pipe é un clase co decorador @Pipe e que implementa a interface PipeTransform. Créase co comando `$ ng generate pipe`. Por exemplo, a seguinte pipe normaliza número de teléfono e engade un prefixo:

_number-perefix.ts_

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
	name: 'phonePrefix'
})

export class PhonePreficePipe implements PipeTransform {
	transform {value: string, country?:string} {
		let prefix = '';
		switch(country){
			case 'es':
				prefix = '+34';
				break;
		}
		return prefix + value;
	}
}

```

## 6. Directivas

As directiva son un tipo de elemento de Angular que nos permite modificar o comportamento do html en tempo de execución. Hai os seguintes tipos de directivas:

- Compoñentes. Son as que permiten crear compoñentes reutilizables.
- Atributos. Son as que modifican os propiedades ou atributos dun elemento html segundo o estado da aplicación.

### 6.1. Directivas estruturais

As directivas estruturais son aquelas que modifican a estrutura por defecto do html dun compoñente. Angular proporciona varias directivas estruturais de base, dentro do seu core,

- **Directiva ngIf**. üsase para engadir un elemento do DOM en función de se unha condición se cumpre ou non. Ten a seguinte sintaxe: `<tag *ngIf="expresion"></tag>`, onde a expresión deber ser unha válida para JS. Creará e mostrará o elemento no DOM se a expresión se avalía a verdadeiro e non o fará se se avalía a falso. O asterisco é obrigatorio porque é un alias a un template. O HTML real é o seguinte:
  ```html
  <template [ngIf]="expresion"><tag></tag></template>
  ```
  Esta directiva permite exoller entre diferentes bloques de código dependendo da condición facendo uso da sintaxe con 'else':
  ```html
  <tag *ngIf="expresion; else #elseBlock"></tag>
  <ng-template #elseBloack><></ng-template>
  ```
- **Directiva ngFor**. üsase para traballar con listas de elementos. Función igual que un bucle de iteración. A sintaxe é a seguinte: `<tag *ngFor="let element of collection">{{element.view}}</tag>`: O asterisco é obrigatorio pola mesma razón que o anterior. No caso de a colección ser moi grande e subre unha modificación, perderemos rendemento. Angular proporciona a funcionalidade trackBy que se asocia a unha función que xestionan o obxecto que cambia. Ten a seguinte sintaxe:
  ```html
  <div *ngFor="let e of elements; let i = index; trackBy: trackItems"></div>
  ```
  e a función asociada recibe o índice da lista e o item ta lista e devolve o seu id de forma que en lugar de actualizar toda a lista, só actulizará o elemento que recibe os cambios no seu estado.
  ```typescript
  trackItems(index:number, item: Item){
  	return item.id
  }
  ```
  A directiva ngFor pode recibir máis elementos, first, last, even e odd útiles para xestionar a lista.
- **Directiva ngSwitch**. Funciona igual que calquera estrutura de selección. Ten a seguinte sintaxe:

```html
<span [ngSwitch]="property">
  <span *ngSwitchCase="value1">Value 1</span>
  <span *ngSwitchCase="value2">Value 2</span>
  <span *ngSwitchCase="value3">Value 3</span>
</span>
Neste caso o binding faise de un dos caos obre o switch pai. O asterisco indica
onde hai un template funcionando por debaixo.
```

### 6.2. Directivas de atributo

As directivas de atributo son aquelas que modifican a apariencia ou o comportamento dun elemento. Angular proporciona dúas por defecto no seu core:

- **ngClass**. Con esta directiva podemos controlar o aspecto dos elementos engadindo ou eliminando clases css do seu atributo _class_. Podemos facelo de dous xeitos.
  - A primeira é modificando a propiedade dun elemento, usando o property binding `<div [class.active]="isActive">Estou activo<div>`.
  - De xeito alternativo temos a alternativa _ngClass_ é unha alternativa especialmente útil para manexar varios clases ao mesmo tempo. Pode recibir un string, un array ou un obxecto de configuración: - [ngClass]="'first'": un string só pode conter unha clase css. - [ngClass]="['first', 'active']": un array pode conter varias clases css. - [ngClass]="{'first: isFirst, 'active': this.item.isActive, 'decorated':true}": un obxecto recibe varios pares de chaves-valor. As chaves son string e son os nomes das clases css, os valores son expresións válidas.
    Hai máis opcións. Podemos facer que a directiva invoque unha función que devolve un obxecto de configuración, como por exemplo [ngClass]="objectConfiguration()", ou directamente a unha propiedade no componente.
- **ngStyle**. É unha directiva paralela á directiva ngClass. Coa directiva ngStyle podemos agregar ou quitar estilos. Tamén tempos varias alternativas:
  - Usar o property binding: `<div [style.color]=red>Está en vermello</div`.
  - Usar o obxector de configuración `<div [ngStyle]={'color': isRequired ? 'red': inherit'}>Está en vermello ou non</div`.

Ambas directivas son destrutivas. E caso de conflito dos estilos dun compoñente gaña o último que fose avaliados. As propiedades class e styles funciona como o css en orde de especificicade. Por exemplo style.color non sobrescribe todos os stilos, unicamente a propiedade color.

### 6.3. Directivas de atributo personalizadas

Angular permite crear directivas de atributos personalizadas. Créase co comando `$ ng generate directive`. Unha directiva personalizada é unha clase que implementa algúnha comportamento que pode ser aplicado a un elemento. Esta decorada con @Directive que recibe un obxecto de configuración que especifica a propiedade selector que será o nome da directiva que se lle engade ao html.

Exemplo que define unha directiva personalizada que escoita unha función de callback, se se confirma unha acción.
_my-custom-directive.ts_

```typescript
import { Directive, HostListener, Input } from '@angular/core';

@Directive({
	selector: 'my-custom-directive'
})
export class MyCustomDirective {
	@Input('confirm') fn:Function;
	@HostListener('click', ['$event']);

	onClick(){
		const confm window.confirm('Estás seguro?');
		if (confirm) {
			this.fn();
		}
	}
}
```

_my-component.ts_

```typescript
import { MyCustomDirective } from './my-custom-directive.ts';

save(){
	console.log('saved');
}
```

_my-component.html_

```html
<button [confirm]="save" my-custom-directive>Gardar</button>
```

Como se pode ver, no compoñente úsase a drectiva e selle pasa como input a referencia á función que se vai executar posteriormente.

### 6.4. HostListener

A anotación HostListener asocian unha función a un evento se se produce no host que usa a directiva. Ten a seguinte sintaxe:

```typescript
@HostListener('event', ['$event'])
nameFunction(){
	//... implementación
}
```

A anotación recibe dous parámetros. O primeiro é un string que representa o evento que se quere escoitas e que se produce no host que usa a directiva ou no documento en xeral. O segundo é un array de argumentos. No exemplo é unha referencia ao evento mesmo.

### 6.5. HostBinding

A anotación HostBinding detecta os cambios sufridos sobre unha propiedade de algún elemento. Para definila, hai que especificar a propiedade que se vai observar. Ten a seguinte sintaxe: `@Hostbinding('attr.role') role='main'`.

## 7. Servizos

Un servizo é unha peza de código que xestiona a lóxica máis complexa da aplicación de xeito que queda fóra dos compoñentes das vistas. O servizos xestionan comunicacións externas, sesión, logs, lóxica de negocio, etc... Son clases que adoitan implementar o decorador Injectable, que se importa do core de Angular. Este decorador habilita que a clase emita os datos necesarios para poder inxectar nos servizos as clases que foren necesarias.

### 7.1. Inxección de dependencias.

É un patrón de deseño a traves do cal podemos definir que outras clases van ser usadas por unha clase en concreto, no lugar de que sexa a propia clase a que crea explicitamente os obxectos no seu código.
Os servizos son declarados no módulo correspondente en providers ou a través da configuración do decorador Injectable.

### 7.2. Inxection de servizos en Angular

A inxeción de dependencias funcina de xeito xerárquico. O non se permiten duplicados dun servizo dentro dunha mesma xerarquía. Un módulo pode usar os servizos proveídos nos módulos superiores, pero non nos irmnáns.

### 7.3. O cliente http de Angular

Consultar unha API require usar algunha tecnoloxía. Actualmente JS dispón no nativo fetch pero adimi o uso de librarías como AJAX, Axios ou outras. Angular ten o seu propio cliente http de serie. Considérase unha boa práctica encapsular as peticions http dentro de servizos.
O procolo http establce as seguintes acctións:

- get: obtén un recurso que pode ser un elemento único ou unha collección de elementos.
- post: cre un recurso novo.
- put: actualiza un recurso por completo.
- patch: actualiza un recurso parcialmente.
- delete: elimna un recurso.
  Para usar o cliente http de Angular hai que importar o módulo HttpClientModule, normalmente no AppModule:

```typescript
import { Module } from "@angular/core";
import { HttpClientModule } from "@angular/common/http";

@NgModule({
  imports: [BrowserModule, HttpClientModule],
})
export class AppModule {}
```

Logo hai que importar a libraría HttpCliente no ser vizo que vai usar. O cliente proporciona observables e promesas.

#### 7.3.1. Consumindo unha API

Os observables requiren seren importados, mentres que as promesas nons. Aquí hai un exemplo de como usar ambos en Angular:

```typescript
import { Observable, throwError } from 'rxjs';
import { catchError, map } from 'rxjs/operators';
import { Injectable } from '@angular/core';

@Injectable()
export class AppService {

	constructor( private readondly http: HttpClient){}

	// Observable
	getItemsObservable(): Observable<Item[]>{
		return this.http.get( /* url */ )
			.pipe(
				map( /* procesar os datos */ ),
				catchError( /* procesar o erro */ )
			);
	}
	// Promesa
	getItemePromise(): Promise<Item[]>{
		return this.http.get( /* url */)
			.lastValue()
			.then( /* procesar os datos*/ )
			.catch( /* procesar o erro */);
	}
}
```

#### 7.3.2. Modificación de cabeceiras (headers)

As cabeceiras xestiónanse coas clases HttpHeaders e HttpParams que se engaden á petición:

```typescript
export class AppService {
	saveItem( item: Item): Observable: Item {
		let headers = new HttpHeaders.set('Authorization', token);
		let params = new HttpParams(). set('id', '1');
		return this.http.post(url, item, { headers, params})
			.pipe(
				map( /* procesar os datos */ ),
				catchError( /* procesar o erro */ )
			);
	}
}
```

#### 7.3.3. Peticións non json

O método http get pode recibir como segundo parámetro un obxecto de configuración que especifica o tipo de resposta.

```typescript
export class AppService {
  getSoap(): Observable<unknow> {
    return this.http.get(url, { responseType: "text" });
  }
}
```

## 8. Formularios en Angular

En Angular existen dous tipos de formularios. Os formularios xestiónanse a través de plantillas ou **template driven** e os formularios reactivos ou **reactive forms**.

### 8.1. Template driven forms

Son similares aos formularios convencionais. No controlador realízase un data binding dos coampos do formularios a´nosa plantilla, deixanso as validacións e modelos na vista.

#### 8.1.1. A directiva ngForm

Dado o seguinte formulario

```html
<form>
  <label>Nick:*</label>
  <input type="text" name="id" placeholder="Este é o identificador" />
  <label>Nome completo:*</label>
  <input type="text" name="fullName" placeholder="O teu nome de autor" />
  <label>Imaxe:</label>
  <input type="url" name="imaxe" />
  <button type="submit">Rexistrar</button>
</form>
```

Antes de trandormar este formulario, temos que importar o módulo FormsModule no módule, neste caso será no app.module:

```typescript
import { FormsModule } from "@angular/forms";

@NgModule({
  imports: [FormsModule, BrowserModule],
})
export class AppModule {}
```

para poder usar o formulario de Angular o primeiro que hai que facer é enlazar ese formulario coa directiva ngForm tal que `<form #form="ngForm">`. Así creamos unha variable form na template sobre a exportamos ngForm e coa que podemos acceder ao valor do formulario coa sintaxe `{{form.value}}`. Polo momento é un obxecto valeiro porque non ten un modelo asignado.

#### 8.1.2. As directivas ngModel e ngModelGroup

Para asignarlle un modelo ao formulario hai que usar a directiva ngModel que admite varias sintaxes:

- ngModel: non aplicar ningun tipo de binding entre a vista e o controlador pero busca a propiedade name e asígnalle o valor da propiedade do memos nome ao obxecto do formulario:

```html
<form #form="ngForm">
  <input type="text" name="id" placeholder="Este é o identificador" ngModel />
</form>
```

Produce este efecto no modelo `{{form.value}}` -> `{id: ''}`

- [ngModel]: Fai o binding unidireccional para asoaciar un valor desde unha variable do controlador á vista, pero non modifica o valor da variable cando se modifica o formulario.

```html
<form #form="ngForm">
  <input type="text" name="fullName" [ngModel]="author.fullName" />
</form>
```

Neste caso no controlador teremos un obxecto que se usará para inicializar o formulario:

```typescript
{
	id: '1',
	fullname: 'Author',
	image: 'resource/images/icon.png'
}
```

- `[(ngModel)]`: coñecido como two way data binding. Enlazado bidireccional. Cando se modifica un valor no formulario estase a modificar o obxecto correspondente no controlador. Engade complexidade á aplicación, porque está recollendo o valor do formulario en dous puntos, na variable form da template e na variable author do controlador.

```html
<form #form="ngForm">
  <input type="text" name="fullName" [(ngModel)]="author.fullName" />
</form>
```

A maiores tamén podemos crear obextos complexos mediante as directvas ngMoldelGroup ao formulario con esta sintaxe:

```html
<form #form="ngForm">
  <label>Nick:*</label>
  <input type="text" name="id" placeholder="Este é o identificador" ngModel />
  <div ngModelGroup="data">
    <label>Nome completo:*</label>
    <input
      type="text"
      name="fullName"
      placeholder="O teu nome de autor"
      ngModel
    />
    <label>Imaxe:</label>
    <input type="url" name="imaxe" ngModel />
  </div>
  <button type="submit">Rexistrar</button>
</form>
```

Esta sintaxe crea unha estrutura de datos complexa como a seguinte

```js
{
	id: '1',
	data: {
		fullName: 'Author',
		imaxe: 'resource/images/icon.png'
	}
}
```

#### 8.1.3. Validacións e contro de erros

#### Deshabilitar o botón submit

O primeiro que queremos é validar se o conxunto do formulario está preparado para pode se enviado. Ten a propiedade `invalid` de `form`:

```html
<form #form="ngForm">
  ...
  <button type="submit" [disabled]="form.invalid">Rexistrar</button>
</form>
```

Un formlario pode ser válido `valid` ou non `invalid`. Un formulario será válido cando pasa todas as validacións que establezamos.

#### Validar campos

As validacións neste tipo de formularios é moi doada porque séguese o estándar HTML5:

```html
<form #form="ngForm">
  <label>Nick:*</label>
  <input
    type="text"
    name="id"
    placeholder="Este é o identificador"
    ngModel
    required
  />
  <div ngModelGroup="data">
    <label>Nome completo:*</label>
    <input
      type="text"
      name="fullName"
      placeholder="O teu nome de autor"
      ngModel
      minlength="3"
      required
    />
    <label>Imaxe:</label>
    <input type="url" name="imaxe" ngModel />
  </div>
  <button type="submit" [disabled]="form.invalid">Rexistrar</button>
</form>
```

#### Control de erros

En caso de que falle algunha validación hai que detectala. Isto conséguese mediante o control de erros.
Un erro nun input determinado conségue declarando unha variable local nova co mesmo nome que o input e que terá un obxecto errors

```html
<form #form="ngForm">
  <label>Nick:*</label>
  <input
    type="text"
    name="id"
    placeholder="Este é o identificador"
    ngModel
    required
  />
  <div *ngIf="id.errors?.required && id.pristine" class="error-message">
    O nick é obrigatorio
  </div>
</form>
```

O atributo `pristine` é unha propiedade do campo que nos dí se se modificou ou non.

### 8.2 Reactive forms

Os formularios reactivos son unha implementación que soluciona problemas que presentan os formularios _template driven_.

#### 8.2.1 ReactiveFormsModule

A funcionalidade dos formularios reactivos impleméntase no módulo chamado ReactiveFormsModule que se debe importar nun módulo que corresponda. As principais librarías que se fan usar son FormBuilder, FormGroup e FormContro.

#### FormBuilder

Impos partir do fmulario anterior

```html
<form [formsGroup]="newUser">
  <label>Nick:*</label>
  <input
    type="text"
    name="id"
    placeholder="Este é o identificador"
    formControlName="id"
  />
  <div formGroupName="data">
    <label>Nome completo:*</label>
    <input
      type="text"
      name="fullName"
      placeholder="O teu nome de autor"
      formControlName="fullName"
    />
    <label>Imaxe:</label>
    <input type="url" name="image" formControlName="image" />
  </div>
  <button type="submit" [disabled]="form.invalid">Rexistrar</button>
</form>
```

No controlador contruímos una xerarquía correspondente:

```typescript
this.newUser = this.fb.group({
  id: [""],
  data: this.fb.group({
    fullName: [""],
    image: [""],
  }),
});
```

Como se pode ver hai unha correspondencia entre as directivas dos dos estilos

| template driven | reactive forms  |
| --------------- | --------------- |
| ngForm          | formGroup       |
| ngModel         | formControlName |
| ngModelGroup    | formGroupName   |

#### Validacións

As validacións realízanse do ldao do controlador, usando a clase validators na definición de cada campo:

```typescript
this.newUser = this.fb.group({
  id: ["", Validators.required],
  data: this.fb.group({
    fullName: ["", [Validators.required, Validators.minLenth(5)]],
    image: [""],
  }),
});
```

#### Control de erros

O control de erros realizase ean template pero accedemos ao campos a través do modelo do foormulario e os métods get e hasError.

#### submit

O envío realízase capturando o evento submite na template

```html
<form [formsGroup]="newUser" (ngSubmit)="onSubmit()">...</form>
```

### 8.3 Formularios estritamente tipados

As versións iniciais de Angular non eran completamente seguras en canto a tipado seguro polo que o valor emitido por un formulario era de tipo _any_ e o formulario non tiña moita información sobre o tipo de dato de cada control.

Por tanto era doad atopar erros típicos de seguridade de tipos ao escribir formularios de Angular. A partir de Angular 14 incluía unha funcionalidade de segguridade de tipo que permiten ter mensaxes de error útiles e de autocompletado traballando con valores. Non é necesario definir valores personalizados, senón con cambios pequenos no código.

O mellor xeito de usar formularios tipados

Tomamos como exemplo un formulario de login

```ts
export class LoginComponent {
	form = this.fb.group({
		email: ["", {Validators: {Validators.required, Valitadors.email}}],
		password: ["", {Validators: {Validators.required, Valitadors.minLenght(8)}}]
	})

	constructor(private fb: FormBuilder){}

	login(){}
}
```

Aquí declaramos un formulario. A seguridade de tipos xa está funcionando. Porque? porque o compilador de TypeScript ten un mecanismo de inferencia de tipos. Está a inforerir os nomes dos campos e os seus tipos a partir do valor inicial de cada campo. No caso anterior, considérase os campos nullable e tipo é string | null. Isto ocorre cando se usa o FormBuilder

Erros comúns nos fomrulario tipados.
Un erro moi común é delcara as variables com se tivesen un tipo FormGroup explícito, tal que:

```ts
export class LoginComponent implements OnInit {
	form: FormGroup;
	constructor( private fb: FormBuilder) {}

	ngOnInit(){
		this.form = this.fb.group({
			email: ["", {Validators: {Validators.required, Valitadors.email}}],
			password: ["", {Validators: {Validators.required, Valitadors.minLenght(8)}}]
		})
	}

}
```

Este patrón declara unha varialble tipada e inicializada no OnInit está ben establecida pero non funciona correctamente. O autocompletado nons está disponible e tampouco temos as mensaxes de error cando se asignar valores erróneos.

Por que non funciona?

Este xeito de declara o formuario está tipado como FormGroup<any> polo que se suspende a comprobación de tipso, polo que a seguridade de tipos está desactivada. Para resolverlo hai que declarar a variable com ao inicio da sección.

Por que non hai que declarar tipso extra?

Par facer formularios con tipado seguro, tampoco hai que declara un tipo como

```ts
form: FormGroup<{email: FormGroup<string<{email:FormControl<string|null>, passsword: FormControl<string|null>}>>}>
```

isto non é necesario. É máis flexibe e menos verboso confiar na inferencia de tipos.
Tampouco é necesario cambiar as API don constructor:

```ts
form = new formGroup({
	email: new FormGroup<string | null>("", {Validators: {Validators.required, Valitadors.email}}),
	password: new FormGroup<string | null("", {Validators: {Validators.required, Valitadors.minLenght(8)}})>
});
```

Isto non é incorrecto, para a api de builder é igual de segura pero menos verboso.

Como declarar campos nullos

Por defecto os camso son consideraros nulos. Cando se chama o método reset() de form Angular porá todos os camops como nulos. Tamén se pode setear un campo como non nullable mediante a propiedade nonNullbre a true. Cando se resetea o formulario o c campo será seteado ao valor inicial:

```ts
	email: new FormGroup<string | null>("", {Validators: {Validators.required, Valitadors.email}, nonNullable: true}),
```

ou mellor usar a apis de builder:

```ts
	form = this.fb.group({
		email: this.fb.nonNullable.control(["", {Validators: {Validators.required, Validators.email}}]),
		password: ["", {Validators: {Validators.required, Validators.minLenght(8)}}]
	})
```

O servico NonNullableFormBuilder
Para o caso de formularios longos onde todos sos campos son non nullos en lugar do builder habitual úsase o NonNullableFormbuilder:

```ts
	constructor(private fb: NonNullableFormbuilder);
```

### 8.4. Form array (formularios reactivos)

Técnica para engadir ou eliminar controis dun formulario en tempo de execución.

#### 8.4.1. Definición

Cada formulario ten un modelo definido a través das API de FormControl, FormGroup ou FormBuilder. Normalmente os campos son coñecidos de antemán polo que se pode definir estaticamente. Cand necesitamos construír un fomrulario dinámico, por exemplo, cando o formulario pode agregar ou quitar controis, reaccionar a datos do BE ou crear unha táboa editable. Para iso usamos un form array.

#### 8.4.2. Diferenzas entre Form Array e Form Group

No caso de uso dunha táboa editable in situ, descoñecemos o número de controis de antem´n, porque non sabemos cantas filas via ter a táboa. O usuario pode engdir ou eliminar filas. Como non se pode definir un FormGroup, usamos un FormArray. Ao igual que o FormGroup, é un contenedor de controis que agrega os valores e estados de validez dos seus compoñentes fillos, pero non requires que coñezamos todos os controis, así como os seus nomes. Por ter un número indeterminado de contris empezando por cero. Os controis engádense ou elimínanse dinamicamente. Cada control ten un índice en lugar do nome.

#### 8.4.3. A API de FormArray

Estes son os métodos disponibles na api:

- controls: devolve un array que content todos os controis.
- lenght: devolve a lonxitude do array.
- at(index): devolve un controla nunha posición determinada.
- push(control): engade un control no final do array.
- getRowValue(): devolve o valor de todos os controis a traves da propiedade control.value de cada control.

#### 8.4.4. Exemplo de código

Definimos un modelo para o formulario

```typescript
@Component({
  //...
})
export class FormArrayExampleComponent {
  form = this.fb.group({
    lessons: this.fb.array([]),
  });

  cosntructor(private fb: FormBuilder) {}

  get lessons() {
    return this.form.controls["lessons"] as FormArrray;
  }
}
```

Como exemplo queresmo incluír na táboa dous controis, un para o título e outro para o nival das leccións. Queremos que estes campos fomen parte do formulario principal e afecten ao seu estado de validez. Para isto crearemos un FormGrupo para cada fila cos seus propios validadadores:

##### Engadindo controis

Creamos un botón para engadir un control

```html
<button mat-mini-fab (click)="addLesson()">
  <mat-icon class="add-course-btn">add</mat-icon>
</button>
```

e a continuación a función:

```typescript
addLesson(){
	// mantemos a constante por lexibilidade
	// pero se pode prescindir e optimizar
	const lesson = this.fb.group({
		title:['', Validators.required],
		level:['beginner', Validators.required]
	})

	this.lessons.push(lesson)
}

// refactorizado
	this.lessons.push(this.fb.group({title:['', Validators.required],level:['beginner', Validators.required]}))
```

eliminado o control

```typescript
deleteLesson(lessonIndex:number){
	this.lessons.removeAt(lessonIndex);
}
```

e aquí a template:

```html
<h3>Add course lessons</h3>
<div class="add-lessons-form" [formGroup]="form">
  <ng-container formArryName="leesons">
    <ng-container *ngForm="let lesson of lessons.control; let i=index">
      <div class="lesson-form-row" [formGroup]="lessonForm">
        <mat-form-field appearance="fill">
          <input mat-input formControlName="title" placeholder="Lesson title" />
        </mat-form-field>
        <mat-form-field appearance="fill">
          <mat-select formControlName="leven" placeholder="Lesson Level">
            <mat-option value="beginner">Beginner</mat-option>
            <mat-option value="intermediate">Intermediate</mat-option>
            <mat-option value="advanced">advanced</mat-option>
          </mat-select>
        </mat-form-field>
        <mat-icon class="detele-btn" (click)="deleteLesson()"
          >delete_forever</mat-icon
        >
      </div>
    </ng-container>
  </ng-container>
  <button mat-mini-fav (click)="addLesson">
    <mat-icon class="add-course-btn">add</mat-icon>
  </button>
</div>
```

Como se pode ver, estamos usando as directivas formArrayName e formControlName
para enlazaar o elemento html coa propiedade correspondente.

## 9. Rutas e navegación

O módulo **Router** é a libraría que usa Angular qu se usa para implementar a nevegación a través da url na barra das aplicacións ao estilo das Single Page Aplications. Con isto pódese crear aplicacións complexas e renderizar compoñentes en función do contexto da aplicación.

### 9.1. Rutas básicas

O concepto básico consiste en asociar unha url e o compoñente que se vai renderizar. A configuración inicial parte da ruta base que debe estar definida no index.html asi

```html
<base href="/" />
```

Para configurar as rutas debemos impotar o módulo de rutas e as rutas do paquete:

```typescript
import { RouterModule, Routes } from '@angular/router';

const routes = [
	{ path: '', component: HomeComponent};
	{ path: 'about', component: AboutComponent};
	{ path: '**', component: HomeComponent};
]
```

Cada ruta recibe un path que identifica o patrón url ao que se fai referencia e un component que identifica o compoñente que se vai renderizar. A última ruta usa os asteriscos com comodín para redireccionar des unha ruta non rexistrada, polo que se usa como páxina de erro. O renderizado conséguite mediante a etiqueta `<router-outlet>` no html que habilitasmo para esa ruta.

### 9.2. Enlazado a rutas

O enlazado a rutas pódese facer no html midiante a directiva `routerLink`:

```html
<a routerLink="/" routerLinkActive="active">Home</a>
```

A través do routerLink podemos especificer o nome da ruata á que queremos acceder. A direciva routerLinkActive é opcional e agrega o seu valor ás clases css.
Outra forma de dirixir a unha ruta é facelo programaticamente no compoñente ts:

```typescript
import { Router } from "@angular/router";
// ...
export class Component {
  constructor(private readonly router: Router) {}
  onClick(name: string) {
    this.router.navigate(["/hello"], name);
  }
}
```

A navegación coincide coa ruta "/hello/:name" on os ":" representa un parámetro

### 9.3. Snapshot e observables

Angular habilita un xeito de obert os datos a partir da ruta mediante os snapshots e observables

- Snapshots: usado cando se cambia du compoñente a outro. Tomamos o seguintes código:

```typescript
import { Component, Init } from '@angular/core';
import { ActivatedRoute,  Params, Router } from '@angular/router';

@Component(...)
export  class Component {
	id: string;
	constructor(private readonly route: ActivatedRoute , private readonly router: Router )

	ngOnInit() {
		this.id = this.route.snapshot.params['id'];
	}
}
```

ActivateRoute é una clase que inclúe os seguintes campos: - url: array cons fragmentos que conforman a ruta actual. - data: obxecto onde pode gardar información seteada no resolver. - params: array que contén os parámetros obrigatorios e optativos do path
No exemplo anterior estamos usando a propiedade params para obter o id cada vez que se inializa o compoñente, pero no é reactivo aos cambios.

- Observable: uar observables é necesario cando se produce cambios no compoñentes. Sexa o seguinte código:

```typescript
import { Component, Init } from '@angular/core';
import { ActivatedRoute,  Params, Router } from '@angular/router';
import { Observable } from 'rxjs';
import { switchMap } from 'rxjs/operators';

@Component(...)
private class Component {
	id: string;

	constructor(
		private readonly route: ActivatedRoute,
		private readonly router: Router
	)

	ngOnInit() {
		this.route.params
			.pipe(
				switchMap((params: Params)=>params['id'])
			)
			.subcribe(
				(id: string)=> this.id = id;
			)

	}
}
```

Neste caso a variable id actualízase cada vez que se modifique o id da ruta.

### 9.4. Redireccións

Cando unha aplicación está estructurada en módulos xa non se pode manter as rutas centralizadas e debemos crear rutas a partir doutra rutas. Crear redireccións ou establecer accesos seguindo roles. Dada a ruta

```typescript
{
	path: '',
	redirectTo: '/home',
	pathMatch: 'full'
}
```

redirectTo fai referencia á ruta que queremos redirxir, cuxo valor inclúe a barra. patchMatch pode definir dous valores:

- full: ten en conta a url tal cal e a compra co valor do path. Case de ser unha ruta filla hai que ter en cona a ruta pai.
- prefix: ten en conta o valor de redirectTo como prefixo que se engade á comparación.

### 9.5. Parámetros

Cado se necesita introducir un parámetro nunha ruta úsase a sintaxe dos puntos para definila para cada ruta dentro da propiedade path: 'author/:id'. Pra definir varios parámetros úsase a sintaxe do punto e coma da matriz da url: /author;id=1;status=active.
Para setear os parámetros no método navigate pásaselle un segundo parámetro con eles:

```typescript
this.router.navigate(["/author"], author.id);
this.router.navigate(["/author"], { id: author.id, status: "active" });
```

### 9.6. Módulo de rutas

Para manter a aplicación escalable convén centralizar a xestion das rutas nun módulo específico. Un módulo de rutas terá este aspecto:

```typescript
import { NgModule } from "@angular/core";
import { RouterModule, Routes } from "@angular/router";

const routes: Routes = [];
@NgModule({
  imports: [RouterModule.forRoot(routes)],
  export: [RouterModule],
})
export class RouterModule {}
```

Este módulo impóstase no módulo principal

### 9.7. Xestion independente de rutas

Cada módulo pode xestionar a súas propisas rutas mediante a utilización do método forChild() un módulo especifico.
imports: [RouterModule.forChild(dashboardRoutes)],
Este módulos de rutas impórtanse en cadanseu módulo da funcionalidade e estes no módulo principal.

### 9.8. Rutas fillas

Cando se necesia renderizar só unha parte de esta, pódse usar un segundo router-outlet. Para configuralo, hai que usar a propiedade children na módulo de rutas correspondente:

```typescript
{
	path: 'profile',
	component: ProfileComponent,
	children: [
		{
			path: 'details',
			component: DetailsComponent,
		},
		{
			path: 'grants',
			component: GrantsComponent,
		}

	]
}
```

Isto habilita colocar un router-outlet na template de ProfileComponent que reacciona illadamente ao cambio de ruta. Así obtemos un maior rendemento da aplicación.

### 9.9. Engadindo gardas

Para xestionar gardas de rutas hai que crar unha garda, que é un servizo que implementa a iterfaz CanActivate. Esta función devolve un booleano.
No ficheiro de configuración de rutas, para a ruta que se vai proterxer hai que setear a propiedade CanActive que recibe un array de gardas. A propiedade CanActivateChild aplícase ás rutas fillas. CanDeactivate é unha configuración especial que controla a saída duna ruta cara outra.

### 9.10. Resolves

resolve é un propiedade que proporciona datos e os carga na ruta antes de que se navegue a ela.

## Notas previas

RENDERER E LISTENER - Interactividade
Render - Obxecto que permite manexar elmentos do DOM.

OBSERVABLES / SUBSCRIPCIÓNS
Un observable é obxecto produto dunha petición (equivalen ao callback de js vainilla)

VIEWCHILD
ViewChild @angular/core
@ViewChild('selector') elemento;
Vistas herdadas. En Angular cada etiqueta de html considérase como unha vista. Cada elemento pódese identificar asignado un id coa sintaxe #selector.

ANIMÁCIÓNS
Similares ás animacións con css, pero se crean desde código ts. Deséñanse unha animación e cárgase no array animations na compoñente. Na vista establecese o trigger que o lanza.

    app.module
    	import { BrowserAnimationsModule } from '@angular/platform-browser/animations'
    	imports:
    component ts
    	import { trigger, state, style, animate, transition } from '@angular/animations';
    	@Component
    	animations: [
    	trigger('nome-do-trigger'),
    		state('nome do estado', style({ JSON })),
    		trasition('inicial => final ', animate('animacion')),
    		]
    	var estado: string;
    component html
    	[@nome-do-trigger]="estado"

ANIMÁCIÓNS CON KEYFRAMES
Os keyframes son puntos de ruptura nunha animacion. Para programar unha transición con keyframes úsase a seguinte sintaxe, onde a duración vai en ms e o offset indica a proporcion do tempo de 0 a 1:
transition('inactive => active', [animate(000, keyframes([
style({propiedade: 'valor', offset:0}),
style({propiedade: 'valor', offset:1}),
]))]),

ANGULAR ELEMENTS
Ferramenta de A6+ que permite xerar compoñentes web component/custom components para Angular.
Instálase a libraria
ng add @angular/elements
Compílanse a compoñente para independizalo de ng

ANGULAR MATERIAL
INTRO
Kit de compoñentes de deseño previamente testeadas. Impórtase como unha librería. Son módulos que se importan con npm.
Instalación de dependencias
OLLO é importante que coincida a version de angular @8.0.0
npm install --save @angular/material @angular/cdk @angular/animations
app module ts --> importación
import { BrowserAnimationsModule } from '@angular/platform-browser/animations'
styles css --> importación de estilos
@import '~@angluar/material/prebuilt-themes/indigo-pink.css';

    	As compoñentes impórtanse no app module e úsanse no html.

    CAMBIAR CORES Theming
    	Créase un ficheiro custom.scss (SAX) na raíz.
    	copy-paste de paleta de documentación.
    	Modifícanse os valores das variables seguindo o sistema predefinido.
    	en angular.json styles incluir o ficheiro  npm start

    CAMBIAR TIPOGRAFIAS
    	Class mat-typography chama ao valor definido en material
    	chamada index.html con link

    	En custom.scss pásaselle unha configuración de tipografía nunha función
    		$custom-typography: mat-typography-config{ $font-family: "serif",
    		$button: mat-typography-level{10px, 30px, 300}};

    MÚLTIPLES TEMAS
    	En appComponent class="alternative-theme"
    	En custom.scss
    	.alternative-theme {
    		/* Inclúese o código de tema COS NOMES DAS VARIABLES MODIFICADOS para que non se pisen. */
    	}

    BOOSTRAP 4
    	Incorporar boostrap
    		npm i --save bootstrap jquery popper.js
    		convertimos o styles.css a scss
    		mudamos o nome en angular.json -> npm install
    		en styles.scss importamos
    			@import '~boostrap/scss/bootstrap';
    			@import '~boostrap/scss/bootstrap-reboot';
    			@import '~boostrap/scss/bootstrap-grid';

    ANGULAR MATERIAL INTERACCIÓNS
    	As interaccións entre compoñentes programanse no ts da compoñente onde están programados.

RXJS

TESTING

LIBRERÍAS JS DE TERCEIROS
Para implementar unha libería de terceiros, por exemplo JQuery, hai varias alternativas:
1º.- Que esté incluída nos módulos de node
import { modulo } from 'modulo'
2º.- Que a libraría teña versión npm
npm install --save nome_libraria
import \* as modulo from 'modulo'
3º.- Gardar a librería js en assets
npm install @types/node --save-dev
configúrase tsconfig.ts en types ["node"]
const modulos = require('assets/modulo.js')
4º.- declarala en index.htlm
declare var modulo;

APACHE CORDOVA
Apache Cordova é un framework permite crear app multiplataformas con tecnoloxías web. Está pensado para dispositivos móbiles. O proxecto de Cordova créase dentro do proxecto de angular.

ANGULAR ELECTRON
Electron é un framework que permite crear app de escritorio con tecnoloxías web. A idea é desenvolver unha aplicación web en angular e logo compilala.

ANGULAR UNIVERSAL
Angular universal. Ferramenta que permite prerrenderizar as compoñentes de aplicación para seren vistos por boots. Angular 7 xa incorpora esta funcionalidade de xeito nativo.

SEO

BOAS PRÁCTICAS

## Probas unitarias

Karma + Jasmine

Seguindo a metodoloxía TDD, primeiro se escriben os test en base aos requirimentos que a app de debería ter e logo se escribe o código que satisfai os requisitos e pasan as probas.

As probas unitarias testean a funcións públicas dun compoñente. Estas deberían ser funcións puras de retorno de valor.
Xunto con cada compoñente hai un ficheiro .spec.ts que conten as probas unitarias.

### Filosofía dos 3 A

Preparar, actuar e verificar. (En inglés Arrange, Act, Assert).
Prepárase un escenario para unha batería, lánzase a función que queremos testar e verificamos o resultado.

1. Impórtase o ficheiro que se quere testear

```javascript
import { Component } from "./component";
```

2. As baterias de test agrúpanse mediante a sintaxe `describe`. Se a lóxica é moi complexa, dentro da bateria de probas de cada compoñente, cada función tería tamén o seu propio describe

```javascript
describe("Tests for AppComponent", () => {
  // Aquí van os diferentes test.

  describe("Tests for myFunction", () => {
    // Aquí van os diferentes test.
  });
});
```

3. Cada test vai dentro dunha delararcion **it** (de _item_) que inclúe unha descrición e unha función. Dentro da función instánciase o componente que inclúe a función, execútase a función e compróbase o resultado.

```javascript
it("should return nine", () => {
  // arrange
  let c = new Component();
  // act
  let result = c.myFunction(a, b);
  // assert
  expect(result).toEqual(9);
});
```

### beforeEach

Trátase dunha función de preparación para cada item.

por exemplo

```javascript
let c;
beforeEach(() => {
  c = new Component();
});
```

### Focus

Un foco é unha técnica que consiste en correr unicamente algunha batería de probas ou algún item en concreto. Para focar un elemento, agrégase un f ao describe ou ao item: `fdescribe` ou `fit`.

### Mocking

Simulación controlada de obxectos que imitan o comportamento dos obxectos reais.

### Api básica de Jasmine

#### Matchers (comparadores)

- expect(element).isNan(); é un non número
- expect(element).toBeDefined(); variable definida
- expect(element).toBeUndefined(); variable indefinida
- expect( 1 + 2 == 3).toBeTruthy(); é verdadeiro
- expect( 1 + 2 == 4).toBeFalsy(); é falso
- expect( 5 ).toBeLessThan(10); menor que
- expect( 5 ).toBeGreaterThan(10); maior que
- expect( 'string' ).toMatch(/regex/); contén a regex
- expect( collection ).toContain(element); o array conten o elemento ? que pasa cos obxectos.

### Testear servizos (implica mockear un http )

### Comando de probas

`npm test` - Corre `ng test`.
`ng test`- Corre as probas, abrindo un navegador e mantén o navegador aberto.
`ng test --watch=false` - Corre as probas, abrindo un navegador e pecha o navegador aberto
despois da execución.
`ng test --single-run` - deprecado

`ng test --code-coverage` - xenera o reporte de cobertura de test (crea a carpeta de coverage)

`http-server coverage` - lanza un servidor para mostrar o informe html (require ter instalado o paquete de ndoe http-server)

PROBAS DE INTEGRACIÓN

PROBAS E2E

## ACTUALIZAR VERSIÓN ANGULAR (GLOBAL)

1. Desinstalar os paquetes anteriores de Angular Cli. `npm uninstall -g @angular/cli`

2. Borrar a caché `npm cache clean --force`

3. Instalar a última versión de angular `npm install -g @angular/cli@latest`

   2020.07.30. Actualizo a versión 12.1.4. Saen 3 warnings. Creo un proxecto de cero parace ir ben.

## ACTUALIZAR PROXECTO

Para actualizar un proxecto o mellor é ir actualizando de versión a versión. A web de Angular ten unha sección específica.

2020.07.30.

Actualizo un proxecto da 9 á 10.
Hai que borrar o package-lock.json
O ng update require un repositorio limpo.
`ng update @angular/cli @angular/core`
Hai que facer un `npm install --force` para faga a instalación de dependencias.
Actualizo un proxecto de 10 a 11.

Actualizao un proxcto de 11 a 12.
Na versión 12 cambia a compilación a produción a `ng build --configuration production`.

## NOTAS ANGULAR

## Actualizar Angular

Actualizar Angular globalmente

`npm install -g @angular/cli@latest`

Actualizar proxecto de Angular. Seguir as instrucións da guía de actualización oficial en
[Angular Update Guide](https://update.angular.io/).

## REFERENCIAS

Moldeo Interactive Angular en español
://www.youtube.com/watch?v=k1uM6YeEx6g&list=PLHgpVrCyLWApLDoezmOfrUXb-IMoDs5Ls&index=1

Validadores personalizados para formularios reactivos
https://blog.angular-university.io/angular-custom-validators/?utm_source=newsletter&utm_medium=email&utm_campaign=angular_custom_form_validators_complete_guide&utm_term=2021-06-12

Estratexia de captura de erros en observables e funcionamento do retryWhen
https://blog.angular-university.io/rxjs-error-handling/?utm_source=newsletter&utm_medium=email&utm_campaign=rxjs_error_handling_complete_practical_guide&utm_term=2021-06-21

Guías de angular
https://blog.angular-university.io/
ngIf
https://blog.angular-university.io/angular-ngif/?&utm_source=newsletter&utm_medium=email&utm_campaign=did_you_know_about_all_these_features_of_angular_ngif&utm_term=2021-08-18

importar un mapa de leaflet
https://www.digitalocean.com/community/tutorials/angular-angular-and-leaflet

## INXECCIÓN DE DEPENDENCIAS

### A función inject

A partir da versión 14 (xuño 22) hai un novo xeito de inxectar dependencias nos compoñentes: trátase de usar a función `inject()` que se importa do core.

Para usala créase unha referencia ao elemento que se vai inxectar e no coro na do constructor faise a inicialización:

```Typescript
import { Component, inject } from '@angular/core';
import { Myservice } from './my.service';

@Component({...})

export class My component {
	private myService?: MyService;

	constructor(){
		this.myService = inject(MyService);
	}
}
```

Podemos prencidir da función constructora mediante esta nova sinxtaxe:

```Typescript
private readonly myService = inject(MyService);
```

As clases fillas non necesitan pasarlle as dependencias ao `super()` no seu construtor. Os tests simplificanse.

## CONTENT PROJECTION

### A directiva ng-content e a Content Projection

A Proxección de Contido (_Content Projectio_) é unha característica do framework Angular que permite a transferencia de contido dinámico dun componente pai a un componente fillo.

En Angular, os compoñentes son os bloques de construción básicos da aplicación. Están compostos por unha estrutura de marcado HTML, estilos CSS e lóxica específica. Nalgúns casos, é necesario que un compoñente pai proporcione contido adicional ao compoñente fillo para que este poida renderizalo nun lugar específico.

A Proxección de Contido entra en xogo neste punto. Permite definir un marcador de espazo nun compoñente fillo, indicando onde o contido proporcionado polo compoñente pai debe ser inserido. O compoñente pai pode entón pasar ese contido ao fillo usando as etiquetas <ng-content> ou <ng-content select="...">.

A etiqueta <ng-content> no compoñente fillo define o lugar onde se proxectará o contido. Se tiver varios lugares de proxección no compoñente fillo, pódese utilizar o selector opcional "select" para especificar qué contido debe ser inserido en cada lugar.

A Proxección de Contido é útil cando se necesitan crear compoñentes reutilizables que poidan recibir contido personalizado en diferentes contextos. Permite crear compoñentes flexibles e modulares, facilitando a composición de interfaces de usuario complexas.

Para enente o problema tomemos un exemplo de deseño clásico. Trátase dun formulario cuxos inputs son un compoñente personalizado que implementan input nativos.

Vexamos o código:

_form.component.ts_

```Typescript
@Component({
	selector: 'app-form',
	template: `
		<h1>FA imput></h1>
		<fa-input icon="envelope" (value)="onNewValue($event)"></fa-input>
		<fa-input icon="look" (value)="onNewValue($event)"></fa-input>
	`
})
export class FormComponent{
	onNewValue(val){
		console.log(vale)
	}
}
```

Aquí temos un elemento HTML personalizado chamado <fa-input> que toma o nome do icono e mostra os valores nunha caixa de texto. É unha aproximación inicial pero ten varios problemas. A implementación deste compoñente é a seguinte:

_fa-imput.component.ts_

```Typescript
@Component({
	selector: 'fa-input',
	template: `
		<i class="fa" [ngClass]="clasess"></i>
		<input (focus)="inputFocus=true"
				(blur)="inputFocus=false"
				(keyup)="value.emit(input.value)"
				#input></input>
	`,
	styleUrls: ['./fa-input.componente.css']
})
export class FaInputComponent{
	@input() icon: string;
	@Output() value = new EventEmmiter<string>();
	inputFocus = false;

	get clases(){
		const cssClasses = {
			fa: true
		}
		cssClasses['fa-' + this.icon] = true;
		return cssClases
	}

	@HostBinding('class.focus')
	get focus{
		console.log(this.inputFocus);
		return this.inputFocus;
	}
}
```

_fa.input.component.css_

```css
:host {
  border: 1px solid grey;
}
input {
  border: none;
  outline: none;
}
:host(.focus) {
  border: 1px solid blue;
}
```

Vemos que o input ten os bordes e os contidos eliminados e que se engadiu un borde semellante no host para crear a ilusión no HTML. O foco tamén está simulado. O compoñente ten unha propiedade `icon` que define o iconoque se vai mostrar. Para detectar o foco usamos o input nativo e usamos un Hostbindind para engadir a clase no host.

Esta arquitectura ten os seguines problemas:

1. Problema de deseño. Debemos manter todas as propiedades do input nativo. O compoñente `fa-input` debe simular o comportamento dun input nativo pero non soporta propiedades estándar como `type`, `autocomplete`, `placeholder` ata as 31 estándar sen incluír as propiedades de accesibilidade. A solución posaría por reenviar as propiedades que necesitamos ao input nativo oe que é molesto, pero factible.
2. A integración cos formuladios de Angular. Para poder incluír este input nun formuladio deberáimso incluir os atributos do formulario tamén no input nativo, como `FormControlName`.
3. A detección de eventos estándar no navegador. Para poder detectar os eventos e pasarllo ao compoñente pai.
4. Propiedades personalizadas de 3ª parte. Hai sistemas de terceiros que esperan ceras propiedades, como datos `data-` que necesitan ser soportadas.
5. O **quid** é que estamos ocultando o input nativo dentro da template do compoñente. Estamos creando unha barreira entre a template externa que coñece as propiedades personalizadas e o input nativo que as debe utilizar.

### Uso da proxección de contido

Para poder proxecta o contido, refactorizaremos o compoñente pai para que inclúa o contido que se proxectará no compoñente fillo. Por tanto, incluímos o input nativo como elemento de contido (_content element_):

_form.component.ts_ (refactorizado paso 1)

```Typescript
@Component({
	selector: 'app-form',
	template: `
		<h1>FA imput></h1>
		<fa-input icon="envelope" (value)="onNewValue($event)">
			<input type="email" placeholder="Email"></input>
		</fa-input>
		<fa-input icon="look" (value)="onNewValue($event)"></fa-input>
	`
})
export class FormComponent{ //...
}
```

Neste caso, o input agregouse como parte do contido do elemento personalizado `fa-input`. Isto tamén é habitual en elementos html nativos.

Podemos consultar calquera cousa dos contido dunha etiqueta dun compoñente usando dos decoradores `@ContenChild` e `@ContenChildren`.

Ademáis podemos tomar calquera cousa e usala directamente dentro do compoñente usando a directiva `ng-content`.

_fa-imput.component.ts_ (refactorizado paso 2)

```Typescript
@Component({
	selector: 'fa-input',
	template: `
		<i class="fa" [ngClass]="clasess"></i>
		<ng-content></ngcontent>
	`,
	styleUrls: ['./fa-input.componente.css']
})
export class FaInputComponent{

	get clases(){
		const cssClasses = {
			fa: true
		}
		cssClasses['fa-' + this.icon] = true;
		return cssClases
	}
}
```

Esta versión accede directamente ao input html, peor non resolver a simulado do foco e rompe os estilos css.

### Aplicar estilos a elementos proxectados

Os estilos do input nativo déixanse de aplicar porque están establecidos dentro do alcance do compoñente `fa-input`, polo que o selector input aplícase dentro da templates dese compoñente.

Cando Angular usa a proxección de contido crea un identificador para o elemento proxectado. A template en tempo de execución queda así:

```html
<fa-input icon="envelope" _nghost-c0="">
  <i _ngcontent-c0="" class="fa fa-envolope"></i>
  <input placeholder="Email" type="email" />
</fa-input>
```

para aplicar os estilos hai que modificar o selector polo seguinte:

```css
:host /depp/ input {
  border: none;
  outline: none;
}
```

Introducimos o prefixo `:host` para que os estilos se apliquen dentro deste compoñente. Aplicamos o modificador `/depp/` para que afecte non só aos elementos html deste compoñente, senón tamén a elementos descendentes. Así, o css en tempo de execución será o seguinte:

```css
[_nghost-c0]input {
  border: none;
  outline: none;
}
```

Deste xeito os estilos manteñen o alcance do compleñent `fa-input` pero se filtrán a calquera input dentro do compoñente en tempo de execucion, incluíndo o input nativo proxectado.

### Interacción con contido proxecto

Para simular a funcionalidade do foco necesitamos que o fa-input coñesa se o input proxecto ten o foco ou non. Como non se pode interactuar directamente coa etiqueta ng-content, aplicamos unha directiva personalizada (que chamaremos inputRef) no input orixinal.

O html quedaría así:
_form.component.ts_ (refactorizado paso 3)

```Typescript
@Component({
	selector: 'app-form',
	template: `
		<h1>FA imput></h1>
		<fa-input icon="envelope" (value)="onNewValue($event)">
			<input inputRef type="email" placeholder="Email"></input>
		</fa-input>
		<fa-input icon="look" (value)="onNewValue($event)"></fa-input>
	`
})
export class FormComponent{ //...
}
```

A directiva esá definida así:

```Typescript
@Directive({
	selector: '[ipnutRef]'
})
export class InputRefDirective {
	focus = false;

	@HostListener("focus")
	onFocus(){
		this.focus = true;
	}

	@HostListener("blur")
	onBlur(){
		this.focus = false;
	}
}
```

Agora podemos interactuar co contido proxectado. O compoñente `fa-input` queda así:

_fa-input.component.ts_ (refactorizado paso 4)

```Typescript
@Component({
	selector: 'fa-input',
	template: `
		<i class="fa" [ngClass]="clasess"></i>
		<ng-content></ngcontent>
	`,
	styleUrls: ['./fa-input.componente.css']
})
export class FaInputComponent{
	@Input() icon: string;

	@ContentChild(InputRefDirective)
	input: inputRefDirective;

	@HostBinding("class.focus")
	getFocus(){
		return this.input ? this.input.focus : false;
	}

	get clases(){
		const cssClasses = {
			fa: true
		}
		cssClasses['fa-' + this.icon] = true;
		return cssClases
	}
}
```

Como se pode ver, úsase o decorador `@ContentChild` para inxectar a directiva dentro do compoñente polo que o valor do campo input obtense desa directiva. Por outra parte, o decorador `@HostBinding` estamos seteando a clase css `focus` que define o estilo para o evento onFocus. Con esta implementación temos un compoñente funcional, que sopora as propiedades nativas hatem, a accesibilidade, as propiedades de terceiros e a integración con formularios de Angular.

### Proxección de contido multiliña

Como deberíamos facer para facer a proxección non só do input, senón tamén do icono? Podemos sleccionar varios tipos de contido.

_form.component.ts_

```html
<fa-input icon="envelope" (value)="onNewValue($event)">
	<i class="fa fa-envelope">
	<input inputRef type="email" placeholder="Email">
</fa-input>
```

_fa-input.component.ts_
_fa-input.component.ts_ (refactorizado paso 4)

```Typescript
@Component({
	selector: 'fa-input',
	template: `
		<ng-content select="i"></ngcontent>
		<ng-content select="input"></ngcontent>
	`,
	styleUrls: ['./fa-input.componente.css']
})
export class FaInputComponent{}
```

Cada un dos selectores buca un elemento concreto, pero tamén se poderían usar outros selectores css válidos. En caso de que son se estableza a select, capturará o contido que non coincida con ningún selector. GGG
