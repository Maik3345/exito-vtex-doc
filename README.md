



--- ---

# Administración de landings en Vtex

[Guía para la creación de una landing](https://github.com/grupo-exito-ecommerce/exito-vtex-doc/blob/master/directory/landing-creation/landing-creation.md)  
[Descarga](https://github.com/grupo-exito-ecommerce/exito-vtex-doc/blob/master/resources/examples/landing/new-landing.html) el archivo HTML base para la creación de una landing

# Éxito (Vtex IO)

Esta documentación es una guía para el desarrollo con **Vtex IO**

[Lineamientos desarrollo](#lineamientos-de-desarrollo)  
[Recursos necesarios](#recursos-necesarios)  
[Guía](#gu%C3%ADa)  
[Vtex Cli](#vtex-cli)  
[Trabajando con Vtex + React](#trabajando-con-vtex-y-react)  
[Integración continua](#integraci%C3%B3n-continua)

## Lineamientos de Desarrollo

### Estándar de manejo de Git
Referirse a [GitFlow](http://aprendegit.com/que-es-git-flow/)

### Recomendaciones merge Develop / Master
- Los pasos a Develop requieren de un Pull Request para la respectiva revisión par.
- Mantener las ramas de desarrollo actualizadas antes de realizar merge contra Develop/Master, por lo tanto debe constanemente revisarse cambios que se estén realizando sobre la rama a la cual se pasarán los cambios.
- Los warnings por errores de typescript deben estar corregidos antes de pasar los cambios a develop/master. De esta forma el comando vtex link -u que permite enlazar el proyecto contra el workspace de trabajo, solo es permitido para efectos de agilizar las pruebas de concepto del desarrollo que se esté llevando a cabo.

### Versiones
Seguir el estándar de Semantic Versioning [ver aquí](https://docs.npmjs.com/about-semantic-versioning)

### Publicación del store y componentes hijos
El vendor para el proyecto de store corresponde con la cuenta específica: exito, exitocol, carulla, carullaqa
Para el resto de componentes siempre se usa exito. Esto mientras los componentes puedan ser comunes entre cuentas.

## Recursos necesarios

1.  [Node js](https://nodejs.org/es/)
2.  [Yarn](https://yarnpkg.com/en/) Gestor de paquetes de Facebook
3.  [Visual Studio Code](https://code.visualstudio.com/) Editor  
    3.1 Extensiones Básicas:
    *   [ES7 React/Redux/GraphQL/React-Native snippets](https://marketplace.visualstudio.com/items?itemName=dsznajder.es7-react-js-snippets)
    *   [Beautify](https://marketplace.visualstudio.com/items?itemName=HookyQR.beautify)
    *   [Auto Import](https://marketplace.visualstudio.com/items?itemName=steoates.autoimport)
    *   [EsLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
    *   [Version Lens](https://marketplace.visualstudio.com/items?itemName=pflannery.vscode-versionlens)
4.  [Create React App Repo](https://github.com/facebook/create-react-app)
5.  [Create React App Npm](https://www.npmjs.com/package/create-react-app)
6.  [Vtex Cli](https://www.npmjs.com/package/vtex) Línea de comandos para vtex
7.  [Exito Cli](https://www.npmjs.com/package/exito-cli) Línea de comandos para éxito
8.  [CMDER](http://cmder.net/) Terminal Para windows
9.  [Iterm2](https://www.iterm2.com/) Terminal para Mac
10.  [Aws Cli](https://docs.aws.amazon.com/cli/latest/userguide/install-windows.html) Línea de comandos para Amazon

## Guía

### Cursos para iniciar

React Básico [Youtube CodeJobs](https://www.youtube.com/watch?v=bG53Pw17tog&list=PLeWI3XlFEVOX6jACDygzApsvigQiDrun8)  
React Curso Completo [Udemy](https://exito.udemy.com/react-the-complete-guide-incl-redux/learn/v4/overview)  
Graphql + React [Udemy](https://exito.udemy.com/graphql-with-react-course/learn/v4/content)  
Guía [Gitflow](http://aprendegit.com/que-es-git-flow/)

[React typescript tips](https://github.com/sw-yx/react-typescript-cheatsheet)

### Cómo manejar la versión de los componentes (Semantic versioning)

para manejar la versión de nuestros componentes emplearemos la siguiente guía [semantic-versioning](https://docs.npmjs.com/about-semantic-versioning)

### Como se deben de documentar el código en React

Para realizar la documentación en React se emplea el estándar definido por [react-styleguidist](https://react-styleguidist.js.org/docs/documenting.html) donde se definen diversas técnicas necesarias para documentar los componentes creados, además de esto permite generar una documentación automática que permite visualizar muy bien el contenido que hemos documentado. [demo](https://github.com/styleguidist/react-styleguidist/tree/master/examples/basic)

Se recomienda manejar el concepto de [jsDoc](http://usejsdoc.org/) para los comentarios de nuestros componentes.

Para la documentación emplearemos los archivos

*   [Changelog.md](http://Changelog.md)
*   [Readme.md](http://Readme.md)

### Ejemplos para documentar:

[Basic Changelog](https://github.com/grupo-exito-ecommerce/exito-vtex-doc/blob/master/resources/examples/components/documentation/CHANGELOG-BASIC.md)
[Basic Readme](https://github.com/grupo-exito-ecommerce/exito-vtex-doc/blob/master/resources/examples/components/documentation/README-BASIC.md)

### Definición para los workspace empleados en el desarrollo

Se plantea la siguiente estructura, donde **exito** es el workspace principal o productivo, el workspace **dev** es el workspace pre productivo y los workspaces **qa1, qa2, qa3** son los workspace destinados para los equipos de SQA para realizar las validaciones de los desarrollos que se planteen para el sprint. Cada desarrollador deberá de crear su workspace definiendo el equipo de SQA que realizará sus validaciones técnicas y el tipo de desarrollo que está realizando en ese momento.

#### Ejemplo:

*   **qa1_header–exito.myvtex.com**  
    **qa1** —> Equipo de SQA encargado de la validación técnica  
    **header** —> Desarrollo asignado

#### Jerarquia de los workspace



|  | [master]([https://exito.myvtex.com/](https://exito.myvtex.com/)) |  |
|--|--|--|
|  | **[dev](https://dev--exito.myvtex.com/)** |  |
| **qa_feature** | **qa_feature**  | **qa_feature** |
| feature | feature |feature  |

## Vtex Cli

*   [Instalación de dependencias para el Admin de Vtex](#instalaci%C3%B3n-de-dependencias-para-el-admin-de-vtex)
*   [Creación de un nuevo componente con Exito cli](#creaci%C3%B3n-de-un-nuevo-componente-con-exito-cli)

### Instalación de dependencias para el Admin de Vtex

Las siguientes dependencias permiten agregar comportamientos como el admin pages y el storefront en la página de vtex.

    vtex install vtex.pages-editor
    vtex install vtex.admin-pages

### Actualización de las dependencias de una cuenta en Vtex

    vtex deps update  
    vtex infra update

## Trabajando con Vtex y React

*   [Configuración para el StoreFront](#configuraci%C3%B3n-de-un-componente-editable-en-el-storefront-de-vtex)
*   [Promover workspaces a producción](#promover-un-workspace-a-producci%C3%B3n)

* * *

### Configuración de un componente editable en el StoreFront de Vtex

para la configuración necesaria para el storefront se necesitan tres métodos dentro de nuestro componente:

1.  _*getSchema_ : Define los diferentes atributos que se le pasarán al componente por medio de las propiedades.
```bash
    ClassName.getSchema = () => {
    return {}
    };
```

Ejemplos donde se emplean esquemas en los componentes:

*   [Vtex Carousel](https://github.com/vtex-apps/carousel)
*   [Vtex Minicart](https://github.com/vtex-apps/minicart)

Este método es empleado por Vtex para la creación de las opciones del storeFront

Ejemplo [aquí](https://github.com/grupo-exito-ecommerce/exito-vtex-doc/blob/master/resources/examples/components/schema-examples/basic-shecma-js.js)

## Promover un workspace a producción

los pasos para promover un workspace son:

1.  `vtex workspace production true` Cambiamos el modo producción del workspace a true

#### callback

    info: Workspace dev set to production mode
    info: You can now check your changes before publishing them
    info: If everything is fine, promote with vtex promote

1.  `vtex publish [path]` Publicar todos los componentes o los componentes que vayamos a emplear, para realizar la publicación de un componente debemos de tener en cuenta el orden de importancia de los componentes. de lo contrario obtendremos error al subir los componentes

1.  `vtex promote` Promovemos el workspace actual a ser una integración con el master, este paso eliminará el workspace actual.

## Cómo publicar una aplicación

1.  `vtex workspace production true` Cambiamos el modo producción del workspace a true

1.  `vtex publish [path]` Publicar todos los componentes o los componentes que vayamos a emplear, para realizar la publicación de un componente debemos de tener en cuenta el orden de importancia de los componentes. de lo contrario obtendremos error al subir los componentes, además se debe de tener en cuenta la versión de la aplicación.

1.  Luego de publicar los componentes, volvemos a indicar que el workspace está en modo desarrollo `vtex workspace production false`

_Nota_: Podemos realizar la publicación directa en el workspace master.

## Integración continua

#### Explicación del flujo que se realiza para publicar un componente.

![Flujo actual para realizar el proceso de integración continua](https://github.com/grupo-exito-ecommerce/exito-vtex-doc/blob/master/resources/images/Continuos%20Integration%20Vtex%20AWS.png?raw=true)

## Creación de los triggers para los proyectos:
1. `generate triggerConfig`: Comando que genera un archivo base con la configuración para los triggers.

``` json
[{
"name": "develop",
"customData": {
	"code_build": "exito-vtex-deploy-develop",
	"vendor": "exito",
	"workspace": "dev",
	"code_commit_branch": "develop",
	"url_to_clone": "https://git-codecommit.us-east-1.amazonaws.com/v1/repos"
	}
}]
```

Para crear diferentes triggers en un solo proyecto es necesario copiar la configuración base y reemplazar los puntos importantes, `name` `code_build` `vendor` `workspace`  `code_commit_branch` 

El atributo `url_to_clone` no se debe de cambiar, este es el endpoint para el repositorio de aws code commit

##### Ejemplo

``` json
[{
	"name": "develop",
	"customData": {
		"codeBuild": "exito-vtex-deploy-develop",
		"vendor": "exito",
		"workspace": "dev",
		"codeCommitBranch": "develop",
		"urlToClone": "https://git-codecommit.us-east-1.amazonaws.com/v1/repos",
		"linkCommand": "'vtex link'",
		"publishCommand": "'vtex workspace use master && vtex publish --verbose'"
	}
},
{
	"name": "master",
	"customData": {
		"codeBuild": "exito-vtex-deploy-master",
		"vendor": "exito",
		"workspace": "master",
		"codeCommitBranch": "master",
		"urlToClone": "https://git-codecommit.us-east-1.amazonaws.com/v1/repos",
		"linkCommand": "'vtex link'",
		"publishCommand": "'vtex workspace use master && vtex publish --verbose'"
	}
}]
```

Con esta configuración se generarán dos triggers apuntando a diferentes branchs y llamando a diferentes codebuild. además de realizar un proceso de login en un workspace llamado `dev` y otro `master`


2.  `generate trigger <arn>`: Comando que genera un archivo `.json` que contiene la configuración para agregar los trigger necesarios para realizar la comunicación con el CodeBuild de `develop` o `master`.

3.  `run triggers`: Comando que se encarga de leer el directorio actual y permitir realizar la ejecución de los archivos `.json` que contienen la configuración para actualizar o agregar los triggers de un repositorio.

### Como puedo verificar el build realizado cuando realice un push a los branchs `develop`y `master`

En el servicio de Amazon de CodeBuild pueden encontrar los siguientes proyectos para realizar el build de nuestros componentes

*   [exito-vtex-deploy-develop](https://console.aws.amazon.com/codesuite/codebuild/projects/exito-vtex-deploy-develop/history?region=us-east-1): Empleado para hacer el build del branch develop
*   [exito-vtex-deploy-master](https://console.aws.amazon.com/codesuite/codebuild/projects/exito-vtex-deploy-master/history?region=us-east-1): Empleado para hacer el build del branch master



## Proceso para la actualización de dependencias


1. Creación de un archivo con las ultimas versiones de las dependencias

`vtex deps list > current-dependencies.json`

Para estar seguros de tener las últimas versiones en este archivo, se recomienda previamente correr en el worskpace que se esté trabajando el comando `vtex deps update` con esto actualizamos todas las dependencias a su última versión

2. Creación del archivo de configuración que contendrá las últimas versiones a emplear en la actualización

`generate configDependencies <criteria>`: Comando que toma el archivo `current-dependencies.json` del directorio actual y genera un archivo  `update-dependencies.json` con las dependencias filtradas y el formato igual al de el atributo `dependencies` del archivo `manifest.json`

> ejemplo: `exito generate cd vtex.`: genera el archivo con todas la dependencias que coincidan con el criterio indicado `vtex.` 
> Nota: Cuando un proyecto posee mas de una versión empleada actualmente, se pasa a armar el nombre de la dependencia junto a sus posibles versiones separadas por un `-`  ejemplo: `"vtex.styleguide": "9.67.0-8.67.0",` donde las posibles versiones son `9.67.0` y `8.67.0`

3. Ejecución del proceso para actualizar las dependencias
`run overWriteDependencies <criteria> [lastVersion]`: Comando que toma el archivo `update-dependencies.json` en el directorio actual y luego se encarga de buscar todos los proyectos que hayan en el directorio para listarlos y permitir la selección de los proyectos a actualizar. luego de seleccionar los proyectos se pasa a realizar una validación para saber si poseen cambios a nivel de dependencias y de ser así se pasa a actualizar las dependencias encontradas. este proceso actualiza un dígito la versión del proyecto y genera un mensaje en el archivo `CHANGELOG.md` indicanto que cambios se realizaron.

>Nota: por defecto el comando trae la última versión de la dependencia que posee el proyecto. con el flag `--last` luego del criterio de búsqueda se pasa a emplear la última versión disponible de la dependencia.

  

> Ejemplo: `exito run ov vtex. --verbose`

> Ejemplo empleando la ultima versión: `exito run ov vtex. --last --verbose`

## Preparación del branch de los proyectos


#### Creación del branch en el que se realizarán los cambios

`aws runGitCommand <commandTouse>` comando que permite seleccionar los proyectos en el directorio actual y se encarga de correr el comando de git indicado.

Para realizar el proceso de creación de los branchs en todos los proyectos se corre el siguiente comando.

`exito aws rgc 'git checkout -b name-branch'`

Para pasar los comandos de git, encerramos los comandos en comillas simples para poder indicar los comandos a ejecutar.

Se puede indicar el nombre del branch de la siguiente forma:

`name-branch`
`feature/name-branch`
`hotfix/name-branch`

#### Cambiar entre branchs

Para realizar el cambio entre branchs de todos los proyectos puede emplear la combinación de comandos de git para hacerlo

`exito aws rgc 'git checkout develop &&  git pull'`

Si el branch que se indica no existe, puede emplear `-b` para realizar la creación
`exito aws rgc 'git checkout -b develop &&  git pull'`

#### Descartar los cambios realizados

Para remover todos los cambios realizados y volver a dejar los proyectos en su ultima versión puede correr la siguiente combinación de comandos

`exito aws rgc 'git reset --hard &&  git pull'`

#### Eliminar branchs de los proyectos

Para realizar la eliminación de un branch en todos los proyectos podemos emplear la siguiente combinación de comandos.
  
`exito aws rgc 'git branch -D feature/deps-update'`

#### Preparar los cambios realizados

para preparar los cambios realizados se puede emplear la siguiente combinación de comandos

`exito aws rgc 'git add . && git commit -m "Update dependencies"'`


#### Realizar merge entre el branch creado y un branch indicado

`exito aws rgc 'git add . && git commit -m "Merge feature/deps-update into develop" && git merge -X theirs feature/deps-update'`

#### Subir los cambios realizados

Pueden emplear la siguiente combinación

`exito aws rgc 'git  push'`

### Paso a paso


1.  ` vtex workspace reset`
2. `vtex deps list > current-dependencies.json`
3. `exito generate configDependencies vtex.`
4. `exito aws rgc 'git checkout -b feature/exito-cli-update-dependencies'`
5. ` exito run overWriteDependencies vtex. --verbose`
6. ` exito aws rgc 'git add . && git commit -m "Update all vtex dependencies in the current data 2019-07-22"'`
7. ` exito aws rgc 'git push --set-upstream origin feature/exito-cli-update-dependencies'`
8. `exito aws rgc 'git checkout develop && git pull'`
9. `exito aws rgc 'git merge -X theirs feature/exito-cli-update-dependencies && git add . && git commit -m "Merge feature/exito-cli-update-dependencies into develop"'`
10. ` exito aws rgc 'git push'` 

## Cambios que se deben de realizar en los proyectos

#### Cambios para el sonar.scanner

> Se deben de comentar las keys de login para sonarqube. ya que esto se agrega automaticamente con la cli de exito

#### La carpeta config ya no se usa y se debe eliminar

> El proceso de integración continua ya no necesita que se tenga la carpeta config con los archivos de configuración, por lo que se debe de eliminar del proyecto.

#### Cambios en jest Coverage

> Se debe de realiza la creación del archivo jest.config.js si no se posee en el proyecto, en este archivo debe de ir la configuración de jest que actualmente algunos projectos lo poseen en el package.json, sin este archivo el proceso de integración continua puede lanzar error.




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY5MDgxOTc2MSwtNDEyMjQ2MDAxLC0xMz
UwODgzNjM3LDE1ODg4Mjg1MTEsLTEwNzM5NzY1NTAsLTEwNTMz
NzMxMDIsLTQ4NjEwMDc0OCwzNTM4MDEwNiwyNTU3NzM3MjQsMT
MxNzAyNTk2NSw2NzE5NDcxOTksLTE1NDkxMTMwNTEsNTQ4MDQ0
MzI1LC0xNTA2NzQ0MTQ0LDMwMTA4NjIwMSwtMTMzMjE0NzI0MS
wtNTE0NzMxNDgzLDEwNTAxMDM0MSwxMTUzMzE0NTgyLC02Nzc5
MDg1NDhdfQ==
-->
