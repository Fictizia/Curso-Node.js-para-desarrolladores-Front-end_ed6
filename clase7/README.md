# Clase 7


### Bower

![Bower Logo](http://image.slidesharecdn.com/bower-phxjs-140515152011-phpapp02/95/bower-phoenix-javascript-meetup-1-638.jpg?cb=1400167728)

> Web sites are made of lots of things — frameworks, libraries, assets, utilities, and rainbows. Bower manages all these things for you.

- [Bower](http://bower.io/)
- [Tendencias Bower](http://bower.io/stats/)
- [Buscador Bower](http://bower.io/search/)


**Bower**
Instalamos Bower globalmente

```
  sudo npm install -g bower
```

Dependencias
```
  /home/ubuntu/.nvm/versions/node/v4.1.1/bin/bower -> /home/ubuntu/.nvm/versions/node/v4.1.1/lib/node_modules/bower/bin/bower
  bower@1.6.6 /home/ubuntu/.nvm/versions/node/v4.1.1/lib/node_modules/bower
  ├── is-root@1.0.0
  ├── destroy@1.0.3
  ├── stringify-object@1.0.1
  ├── junk@1.0.2
  ├── chmodr@1.0.2
  ├── user-home@1.1.1
  ├── q@1.4.1
  ├── abbrev@1.0.7
  ├── opn@1.0.2
  ├── bower-endpoint-parser@0.2.2
  ├── bower-logger@0.2.2
  ├── lockfile@1.0.1
  ├── archy@1.0.0
  ├── graceful-fs@3.0.8
  ├── nopt@3.0.6
  ├── lru-cache@2.7.3
  ├── retry@0.6.1
  ├── tmp@0.0.24
  ├── semver@2.3.2
  ├── md5-hex@1.1.0 (md5-o-matic@0.1.1)
  ├── fs-write-stream-atomic@1.0.4 (graceful-fs@4.1.2)
  ├── p-throttler@0.1.1 (q@0.9.7)
  ├── request-progress@0.3.1 (throttleit@0.0.2)
  ├── shell-quote@1.4.3 (array-filter@0.0.1, array-reduce@0.0.0, jsonify@0.0.0, array-map@0.0.0)
  ├── chalk@1.1.1 (escape-string-regexp@1.0.3, supports-color@2.0.0, ansi-styles@2.1.0, strip-ansi@3.0.0, has-ansi@2.0.0)
  ├── bower-json@0.4.0 (intersect@0.0.3, deep-extend@0.2.11, graceful-fs@2.0.3)
  ├── promptly@0.2.0 (read@1.0.7)
  ├── fstream@1.0.8 (inherits@2.0.1, graceful-fs@4.1.2)
  ├── which@1.2.0 (is-absolute@0.1.7)
  ├── bower-registry-client@1.0.0 (async@0.2.10, graceful-fs@4.1.2, request-replay@0.2.0, mkdirp@0.3.5)
  ├── mkdirp@0.5.0 (minimist@0.0.8)
  ├── glob@4.5.3 (inherits@2.0.1, inflight@1.0.4, once@1.3.3, minimatch@2.0.10)
  ├── fstream-ignore@1.0.3 (inherits@2.0.1, minimatch@3.0.0)
  ├── rimraf@2.4.4 (glob@5.0.15)
  ├── insight@0.7.0 (object-assign@4.0.1, async@1.5.0, tough-cookie@2.2.1, lodash.debounce@3.1.1, configstore@1.3.0, os-name@1.0.3)
  ├── bower-config@1.2.2 (graceful-fs@4.1.2, osenv@0.1.3, optimist@0.6.1)
  ├── github@0.2.4 (mime@1.3.4)
  ├── tar-fs@1.8.1 (pump@1.0.1, tar-stream@1.3.1)
  ├── request@2.53.0 (forever-agent@0.5.2, aws-sign2@0.5.0, caseless@0.9.0, tunnel-agent@0.4.1, oauth-sign@0.6.0, isstream@0.1.2, stringstream@0.0.5, json-stringify-safe@5.0.1, tough-cookie@2.2.1, qs@2.3.3, node-uuid@1.4.7, form-data@0.2.0, mime-types@2.0.14, combined-stream@0.0.7, http-signature@0.10.1, bl@0.9.4, hawk@2.3.1)
  ├── cardinal@0.4.4 (ansicolors@0.2.1, redeyed@0.4.4)
  ├── update-notifier@0.3.2 (is-npm@1.0.0, string-length@1.0.1, semver-diff@2.1.0, latest-version@1.0.1)
  ├── decompress-zip@0.1.0 (mkpath@0.1.0, touch@0.0.3, readable-stream@1.1.13, binary@0.3.0)
  ├── handlebars@2.0.0 (optimist@0.3.7, uglify-js@2.3.6)
  ├── inquirer@0.10.0 (strip-ansi@3.0.0, ansi-regex@2.0.0, figures@1.4.0, ansi-escapes@1.1.0, cli-width@1.1.0, rx-lite@3.1.2, through@2.3.8, readline2@1.0.1, cli-cursor@1.0.2, run-async@0.1.0, lodash@3.10.1)
  ├── mout@0.11.1
  └── configstore@0.3.2 (object-assign@2.1.1, xdg-basedir@1.0.1, uuid@2.0.1, osenv@0.1.3, js-yaml@3.4.5)
```

Arrancamos bower.json
```
  bower init
```

```javascript
  {
    "name": "pruebas_bower",
    "homepage": "https://github.com/UlisesGascon/Curso-in-company-NexTReT",
    "authors": [
      "ulisesgascon"
    ],
    "description": "",
    "main": "",
    "moduleType": [],
    "license": "MIT",
    "private": true,
    "ignore": [
      "**/.*",
      "node_modules",
      "bower_components",
      "test",
      "tests"
    ]
  }
```

Buscamos paquetes
```
  bower search <paquete>
  bower search jquery
```

Instalando Paquetes
```
  bower install <paquete>
  bower install jquery
```

Instalando versiones especificas del paquete
```
  bower install <package>#<version>
```

Instalando Paquetes y guardandolos en bower.json
```
  bower install <paquete> -save
  bower install bootstrap -save
```

```
  ulisesgascon:~/workspace/profe/pruebas_bower (master) $ bower install bootstrap -save
  bower jquery#~2.1.4             cached git://github.com/jquery/jquery.git#2.1.4
  bower jquery#~2.1.4           validate 2.1.4 against git://github.com/jquery/jquery.git#~2.1.4
  bower bootstrap#*           not-cached git://github.com/twbs/bootstrap.git#*
  bower bootstrap#*              resolve git://github.com/twbs/bootstrap.git#*
  bower bootstrap#*             download https://github.com/twbs/bootstrap/archive/v3.3.5.tar.gz
  bower bootstrap#*              extract archive.tar.gz
  bower bootstrap#*             resolved git://github.com/twbs/bootstrap.git#3.3.5
  bower jquery#~2.1.4            install jquery#2.1.4
  bower bootstrap#~3.3.5         install bootstrap#3.3.5
```

```javascript
  // bower.json
  {
    "name": "pruebas_bower",
    "homepage": "https://github.com/UlisesGascon/Curso-in-company-NexTReT",
    "authors": [
      "ulisesgascon"
    ],
    "description": "",
    "main": "",
    "moduleType": [],
    "license": "MIT",
    "private": true,
    "ignore": [
      "**/.*",
      "node_modules",
      "bower_components",
      "test",
      "tests"
    ],
    "dependencies": {
      "jquery": "~2.1.4",
      "bootstrap": "~3.3.5"
    }
  }
```

Borrando paquetes
```
  bower uninstall <paquete>
  bower uninstall jquery
```

Borrando paquetes  y guardandolos en bower.json
```
  bower uninstall <paquete>
  bower uninstall jquery
```

Verificando los paquetes instalados y sus dependencias
```
  bower list
```

```
  ulisesgascon:~/workspace/profe/pruebas_bower (master) $ bower list
  bower check-new     Checking for new versions of the project dependencies...
  pruebas_bower /home/ubuntu/workspace/profe/pruebas_bower
  ├─┬ bootstrap#3.3.5 (latest is 4.0.0-alpha)
  │ └── jquery#2.1.4 (3.0.0-alpha1+compat available)
  └── jquery#2.1.4 (latest is 3.0.0-alpha1+compat)
```

Actualizando todo
```
  bower update
```

Actualizando un paquete específico
```
  bower update <package>
```

Usando Bower
```
  bower list -paths
```

```
  ulisesgascon:~/workspace/profe/pruebas_bower (master) $ bower list -paths

    bootstrap: [
      'public/vendor/bootstrap/less/bootstrap.less',
      'public/vendor/bootstrap/dist/js/bootstrap.js'
    ],
    jquery: 'public/vendor/jquery/dist/jquery.js'
```

```html
  <!DOCTYPE html>
  <html lang="es">
    <head>
      <meta charset="utf-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1">
      <!-- The above 3 meta tags *must* come first in the head; any other head content must come *after* these tags -->
      <title>Bootstrap 101 Template</title>

      <!-- Bootstrap -->
      <link href="public/vendor/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet">

    </head>
    <body>
      <h1>Hello, world!</h1>

      <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
      <script src="public/vendor/jquery/dist/jquery.js"></script>
      <!-- Include all compiled plugins (below), or include individual files as needed -->
      <script src="public/vendor/bootstrap/dist/js/bootstrap.js"></script>
    </body>
  </html>
```

**Bower (Entendiendo el funcionamiento)**

bower.json. ¿Qué necesitamos?
```javascript
  {
      "name": "Mi Aplicación",
      "version": "1.0.0",
      "dependencies": {
          "modernizr": "*",
          "jquery": "~2.0.2",
          "bootstrap": "*",
          "requirejs": "*"
      }
  }
```

.bowerrc ¿Donde lo necesitamos?
```javascript
  {
      "directory": "public/vendor",
      "json": "bower.json"
  }
```

Instalamos todo lo anterior
```
  bower install
```


**Bower (Trucos)**

- Se puede instalar componentes aislados primero y luego hacer *bower init* para generar el *bower.json* con todo incluido.
- Ignoramos la carpeta *bower_components* con *.gitignore*. Recuerda que haciendo *bower.init* se instala todo de nuevo.
- Instalación de paquetes más alla de los definidos en search:

- Paquetes registrados:
```
  $ bower install jquery
```

- Acesso directo -> GitHub:
```
  $ bower install desandro/masonry
```

- .git:
```
  $ bower install git://github.com/user/package.git
```

- URLs:
```
  $ bower install http://example.com/script.js
```

### Los problemas de BOWER

![img](https://i.stack.imgur.com/zo1N0.png)

**Limitaciones**
- Gestión de conflictos manual
- Fiarnos del patrón SEMVER por parte de otr@s developers
- Sistema de paquetes propio
- Redundancia respecto a NPM
- Maravillo mundo del [Dependency hell](https://en.wikipedia.org/wiki/Dependency_hell)


### Bower ha muerto

![img](https://rules.ssw.com.au/PublishingImages/package3.jpg)

> BOWER is dead. Only use it for legacy reasons.

**Literatura al respecto**

- [Bower/bower #2298: Consider deprecating Bower](https://github.com/bower/bower/issues/2298#issuecomment-289846310)
- [Bower is dead, long live npm. And Yarn. And webpack in snyk.io/blog by Assaf Hefetz](https://snyk.io/blog/bower-is-dead/)
- [Reddit: Is bower dead? Should we start using other dependency managers?](https://www.reddit.com/r/javascript/comments/5ls30m/is_bower_dead_should_we_start_using_other/)
- [Quora: Is Bower dying?](https://www.quora.com/Is-Bower-dying?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)

### La nueva generación

**Paso 1: Tus herramientas son las de siempre**
- [NPM](https://www.npmjs.com/features)
- [YARN](https://yarnpkg.com/en/)
- [webpack](https://webpack.js.org/concepts/)

**Paso 2: Pasar del `bower.json` al `package.json`**

**Paso 3: Deja de usar `wiredep` y empieza a usar solamente `require()`**

_Nota: Esto es al estilo Browserify exclusivamente_

- [wiredep: Wire Bower dependencies to your source code](https://github.com/taptapship/wiredep)
- [browserify: browser-side require() the node.js way](https://github.com/browserify)
- Debes instalar browserify de forma global con `npm install -g browserify`
- Ejemplo de carga de dependencias
  ```javascript
  var $ = require('jquery'),
      _ = require('lodash'),
      angular = require('angular');
  //..
  ```
- Puedes comprimir y unificar todo el JS en un solo comando `browserify app.js -o bundle.js` y en un único fichero `<script src="bundle.js"></script>`
- Si ademas instalas [watchify](https://github.com/substack/watchify) con `watchify app.js -o bundle.js` refescas los cambios en tiempo real.

**Extra 1: Cosas Interesantes**
- [Usar el campo `browser` en el `package.json`](https://github.com/substack/node-browserify#browser-field)

**Extra 2: Un mundo de información te espera**

- [Why We Should Stop Using Bower – And How to Do It](https://gofore.com/stop-using-bower/)
- [Browserify VS Webpack - JS Drama](http://blog.namangoel.com/browserify-vs-webpack-js-drama)
- [npm and front-end packaging](http://blog.npmjs.org/post/101775448305/npm-and-front-end-packaging)
- [The jQuery Module Fallacy](https://www.evernote.com/shard/s93/sh/390d6836-8797-4f0c-a7c2-fc77fbb0a9b8/649f084e90bae42f)




### Gulp

![Gulp](https://www.escael.com/wp-content/uploads/2015/06/gulpjs.jpg)
![Gulp_anatomy](http://i2.wp.com/joellongie.com/wp-content/uploads/2015/02/web-gulp-anatomy.jpg)
- **Caractísticas**
  - Filosofía de código sobre configuración
  - Basado en stream
  - No es necesario usar archivos temporales
  - Claridad en creación de tareas y seguimiento de procesos
  - Gran cantidad de Plugins
  - Cuenta con una comunidad sólida y madura
  - El sistema de `streams` y `Promises`no es sencillo para developers juniors

- **Instalación**
  - Instalamos Gulp global
  ```
  npm install --global gulp
  ```

  - Incluimos la dependencia en *package.json*
  ```
  npm install --save-dev gulp
  ```

- **Tareas por defecto**
  - Creamos *gulpfile.js* y agregamos dependencias y la primera tarea por defecto
  - Definición
  ```javascript
    var gulp = require('gulp');

    gulp.task('default', function() {
      console.log("Estas en la tarea por defecto!")
    });
  ```
  - Lanzamiento
  ```
    gulp
  ```

- **Más tareas**
  - Creamos una tarea nueva para gestionar la concatenación y minificación de los archivos js.
  - Definición
  ```javascript
  var gulp = require('gulp');
  var concat = require('gulp-concat');
  var uglify = require('gulp-uglify');

    gulp.task('concat-ugly', function() {
      console.log("Estas en la tarea de concatenación!")  
      gulp.src('js/sources/*.js')
      .pipe(concat('app.min.js'))
      .pipe(uglify())
      .pipe(gulp.dest('dist/js'))
    });
  ```
  - Instalamos las nuevas dependencias
  ```
    npm install -save gulp-concat && npm install -save gulp-uglify
  ```
  - Lanzamiento
  ```
    gulp concat-ugly
  ```

- **Agrupando tareas**
  - Definición
  ```javascript
    gulp.task('distro-lista', ['imagenes', 'css', 'js']);
  ```
  - Lanzamiento
  ```
    gulp distro-lista
  ```


- **Concatenando tareas**
  - Definición
  ```javascript
    gulp.task('css-paso-2', ['css-paso-1'], function(
      console.log("css-paso-2 empieza solo cuando... css-paso-1 haya termiando!")
    ));
  ```
  - Lanzamiento
  ```
    gulp css-paso-2
  ```

- **[Ejemplo de gulpfile.js](https://gist.github.com/torgeir/8507130)**


**Entendiendo Gulp**
- gulp.src() y gulp.dest()
  - Un solo archivo
  ```javascript
    gulp.src('client/templates/index.jade')
    // .pipe(...)
  ```
  - Múltiples archivos
  ```javascript
    gulp.src(['client/*.js', '!client/b*.js', 'client/bad.js'])
    // .pipe(...)
  ```
  - Múltiples archivos y carpetas
  ```javascript
    gulp.src('client/templates/**/*.jade')
    // .pipe(...)
  ```
  - Exclusión
  ```javascript
    !js/secreto-config.js
  ```
  - Especificando la extensión
  ```javascript
    publico/*.+(js|css)
  ```
  - [Más opciones](https://github.com/isaacs/minimatch)
- gulp.watch()
  - Monitoriza de manera activa uno o varios archivos y dispara tareas específicas cuando se hayan modificado
  ```javascript
    gulp.watch('js/source/*.js', ['js']);
  ```

### [Gulp: Plugins](http://gulpjs.com/plugins/)
- [gulp-debug](https://www.npmjs.com/package/gulp-debug): BÁSICO para debugear las tareas de GULP y los ficheros en scope de la tarea
- [gulp-concat](https://github.com/contra/gulp-concat): Concatenación de archivos
- [gulp-uglify](https://github.com/terinjokes/gulp-uglify): Comprime javascript usando [UglifyJS2](https://github.com/mishoo/UglifyJS2)
- [gulp-stylus](https://www.npmjs.com/package/gulp-stylus): Compilar de .styl a .css
- [gulp-coffee](https://www.npmjs.org/package/gulp-coffee): Compilar de .coffee a .js
- [gulp-jade](https://www.npmjs.org/package/gulp-jade): Compilador de .jade a .html
- [gulp-if](https://www.npmjs.org/package/gulp-if): Control adiccional para el flujo de subtareas
- [gulp-imagemin](https://www.npmjs.org/package/gulp-imagemin): Minificación de imágenes con formato .png, .jpeg, .gif y .svg, [más opciones](https://github.com/sindresorhus/gulp-imagemin#imageminoptions)
- [gulp-jshint](https://www.npmjs.com/package/gulp-jshint): JSHint
- [gulp.spritesmith](https://www.npmjs.com/package/gulp.spritesmith): Crea Sprites y el css adiccional en diversos formatos (.css, .json, Sass, Less)
- [gulp-zip](https://github.com/sindresorhus/gulp-zip): Compresor ZIP
- [gulp-csslint](https://www.npmjs.com/package/gulp-csslint/): CSS Linter
- [gulp-eslint](https://www.npmjs.com/package/gulp-eslint/): [ESLint](http://eslint.org/)
- [gulp-gh-pages](https://www.npmjs.com/package/gulp-gh-pages/): Gestiona la publicación en GitHub Pages
- [gulp-git](https://www.npmjs.com/package/gulp-git/): Gestiona Git desde Gulp
- [gulp-htmlmin](https://www.npmjs.com/package/gulp-htmlmin/): Minificador de HTML
- [gulp-iconfont](https://www.npmjs.com/package/gulp-iconfont/): Creando fuentes de Iconos desde archivos vectoriales
- [gulp-jsonlint](https://www.npmjs.com/package/gulp-jsonlint): Linter para json
- [gulp-markdown](https://www.npmjs.com/package/gulp-markdown/): Markdown a HTML
- [gulp-sourcemaps](https://www.npmjs.com/package/gulp-sourcemaps/): Crea SourceMaps
- [gulp-uncss](https://www.npmjs.com/package/gulp-uncss/): Elimina CSS que no se use
- [gulp-jsdoc-to-markdown](https://www.npmjs.com/package/gulp-jsdoc-to-markdown/): Conversor de jsdocs a markdown
- [gulp-unzip](https://www.npmjs.com/package/gulp-unzip/): Descompresor ZIP
- [gulp-webstandards](https://www.npmjs.com/package/gulp-webstandards): Verifica prefijos CSS, Versión de librerías js, dcoType, compatibildiad entre navegadores,  etc...
- [gulp-filesize](https://www.npmjs.com/package/gulp-filesize): Muestra el tamaño de los archivos.
- [gulp-grunt](https://github.com/gratimax/gulp-grunt): Tareas de Grutn funcionan en Gulp
- [gulp-shell](https://github.com/sun-zheng-an/gulp-shell): Manejando comandos de terminal


### Interesante de integrar en los proyectos:
- [Easy Accessibility Testing with aXe](https://www.axe-core.org/)
- [puppeteer: Headless Chrome Node API](https://github.com/GoogleChrome/puppeteer)
- [pageres: Genera pantallazos de la web en diversos tamaños](https://github.com/sindresorhus/pageres)
- [PSI: PageSpeed Insights desde la terminal](https://github.com/addyosmani/psi)
- [Lighthouse: Auditing, performance metrics, and best practices for Progressive Web Apps](https://github.com/GoogleChrome/lighthouse)


### Gulp: [gulpfile.js](https://gist.github.com/UlisesGascon/5f32b686cc43037adbf5c0ddf33f55d5#file-gulpfile-js)

```javascript
// generated on 2018-03-31 using generator-webapp 3.0.1
const gulp = require('gulp');
const gulpLoadPlugins = require('gulp-load-plugins');
const browserSync = require('browser-sync').create();
const del = require('del');
const wiredep = require('wiredep').stream;
const runSequence = require('run-sequence');

const $ = gulpLoadPlugins();
const reload = browserSync.reload;

let dev = true;

gulp.task('styles', () => {
  return gulp.src('app/styles/*.scss')
    .pipe($.plumber())
    .pipe($.if(dev, $.sourcemaps.init()))
    .pipe($.sass.sync({
      outputStyle: 'expanded',
      precision: 10,
      includePaths: ['.']
    }).on('error', $.sass.logError))
    .pipe($.autoprefixer({browsers: ['> 1%', 'last 2 versions', 'Firefox ESR']}))
    .pipe($.if(dev, $.sourcemaps.write()))
    .pipe(gulp.dest('.tmp/styles'))
    .pipe(reload({stream: true}));
});

gulp.task('scripts', () => {
  return gulp.src('app/scripts/**/*.js')
    .pipe($.plumber())
    .pipe($.if(dev, $.sourcemaps.init()))
    .pipe($.babel())
    .pipe($.if(dev, $.sourcemaps.write('.')))
    .pipe(gulp.dest('.tmp/scripts'))
    .pipe(reload({stream: true}));
});

function lint(files) {
  return gulp.src(files)
    .pipe($.eslint({ fix: true }))
    .pipe(reload({stream: true, once: true}))
    .pipe($.eslint.format())
    .pipe($.if(!browserSync.active, $.eslint.failAfterError()));
}

gulp.task('lint', () => {
  return lint('app/scripts/**/*.js')
    .pipe(gulp.dest('app/scripts'));
});
gulp.task('lint:test', () => {
  return lint('test/spec/**/*.js')
    .pipe(gulp.dest('test/spec'));
});

gulp.task('html', ['styles', 'scripts'], () => {
  return gulp.src('app/*.html')
    .pipe($.useref({searchPath: ['.tmp', 'app', '.']}))
    .pipe($.if(/\.js$/, $.uglify({compress: {drop_console: true}})))
    .pipe($.if(/\.css$/, $.cssnano({safe: true, autoprefixer: false})))
    .pipe($.if(/\.html$/, $.htmlmin({
      collapseWhitespace: true,
      minifyCSS: true,
      minifyJS: {compress: {drop_console: true}},
      processConditionalComments: true,
      removeComments: true,
      removeEmptyAttributes: true,
      removeScriptTypeAttributes: true,
      removeStyleLinkTypeAttributes: true
    })))
    .pipe(gulp.dest('dist'));
});

gulp.task('images', () => {
  return gulp.src('app/images/**/*')
    .pipe($.cache($.imagemin()))
    .pipe(gulp.dest('dist/images'));
});

gulp.task('fonts', () => {
  return gulp.src(require('main-bower-files')('**/*.{eot,svg,ttf,woff,woff2}', function (err) {})
    .concat('app/fonts/**/*'))
    .pipe($.if(dev, gulp.dest('.tmp/fonts'), gulp.dest('dist/fonts')));
});

gulp.task('extras', () => {
  return gulp.src([
    'app/*',
    '!app/*.html'
  ], {
    dot: true
  }).pipe(gulp.dest('dist'));
});

gulp.task('clean', del.bind(null, ['.tmp', 'dist']));

gulp.task('serve', () => {
  runSequence(['clean', 'wiredep'], ['styles', 'scripts', 'fonts'], () => {
    browserSync.init({
      notify: false,
      port: 9000,
      server: {
        baseDir: ['.tmp', 'app'],
        routes: {
          '/bower_components': 'bower_components'
        }
      }
    });

    gulp.watch([
      'app/*.html',
      'app/images/**/*',
      '.tmp/fonts/**/*'
    ]).on('change', reload);

    gulp.watch('app/styles/**/*.scss', ['styles']);
    gulp.watch('app/scripts/**/*.js', ['scripts']);
    gulp.watch('app/fonts/**/*', ['fonts']);
    gulp.watch('bower.json', ['wiredep', 'fonts']);
  });
});

gulp.task('serve:dist', ['default'], () => {
  browserSync.init({
    notify: false,
    port: 9000,
    server: {
      baseDir: ['dist']
    }
  });
});

gulp.task('serve:test', ['scripts'], () => {
  browserSync.init({
    notify: false,
    port: 9000,
    ui: false,
    server: {
      baseDir: 'test',
      routes: {
        '/scripts': '.tmp/scripts',
        '/bower_components': 'bower_components'
      }
    }
  });

  gulp.watch('app/scripts/**/*.js', ['scripts']);
  gulp.watch(['test/spec/**/*.js', 'test/index.html']).on('change', reload);
  gulp.watch('test/spec/**/*.js', ['lint:test']);
});

// inject bower components
gulp.task('wiredep', () => {
  gulp.src('app/styles/*.scss')
    .pipe($.filter(file => file.stat && file.stat.size))
    .pipe(wiredep({
      ignorePath: /^(\.\.\/)+/
    }))
    .pipe(gulp.dest('app/styles'));

  gulp.src('app/*.html')
    .pipe(wiredep({
      exclude: ['bootstrap-sass'],
      ignorePath: /^(\.\.\/)*\.\./
    }))
    .pipe(gulp.dest('app'));
});

gulp.task('build', ['lint', 'html', 'images', 'fonts', 'extras'], () => {
  return gulp.src('dist/**/*').pipe($.size({title: 'build', gzip: true}));
});

gulp.task('default', () => {
  return new Promise(resolve => {
    dev = false;
    runSequence(['clean', 'wiredep'], 'build', resolve);
  });
});
```

### [Gulp 4](https://github.com/gulpjs/gulp/tree/4.0)

### Gulp 4: Cambios

- Nuevo sistema de dependencias `gulp.task()` solo admite 2 argumentos
- `gulp.series()` y 'gulp.parallel()' son ahora nativas. ¡Adios [runSequence](https://www.npmjs.com/package/run-sequence)!.
- El orden de las tareas es clave y ya no podemos organizarlas como queramos, deben ir por orden de carga
- Es necesario terminar cada tarea con un callback o resolver la promesa. En Gulp3 no era necesario.
- Por el momento tiene poca adopción

> Si tienes un `gulpile.js` funcionando con Gulp 3.x, no merece la pena migrarse.

#### Nuevo sistema de dependencias en detalles

**Antes - Gulp 3.9.x**
```javascript
gulp.task('a', function () {
  // Do something.
});
gulp.task('b', ['a'], function () {
  // Do some stuff.
});

gulp.task('c', ['b'], function () {
    // Do some more stuff.
});
```


**Ahora - Gulp 4.x**

![conceptos](https://fettblog.eu/wp-content/uploads/2015/folie4.jpg)

- Las tareas solo tienen 2 argumentos.
- La concatenación de tareas puede ser serializada con `gulp.series()` o paralelizada con 'gulp.parallel()'

```javascript
gulp.task('my-tasks', gulp.series('a', 'b', 'c', function() {
  // Do something after a, b, and c are finished.
}));
```

```javascript
gulp.task('build', gulp.parallel('styles', 'scripts', 'images', function () {
  // Build the website.
}));
```

### Gulp 4: Guías
- [The Complete-Ish Guide to Upgrading to Gulp 4](https://www.joezimjs.com/javascript/complete-guide-upgrading-gulp-4/)
- [Web Tooling and Automatisation using gulp 4](http://nealbuerger.com/2017/04/web-tooling-and-automatisation-using-gulp-4/)
- [How to install Gulp 4 before it's officially released](https://demisx.github.io/gulp4/2015/01/15/install-gulp4.html)
- [Migrating to gulp 4 by example](https://blog.wearewizards.io/migrating-to-gulp-4-by-example)
- [How to Upgrade to Gulp 4](https://www.fastless.com/gulp-4/)
- [Getting started with Gulp 4 for Angular](https://hackernoon.com/getting-started-with-gulp-4-for-angular-1280a78fa91a)
- [A quick guide for switching to gulp 4](https://codeburst.io/switching-to-gulp-4-0-271ae63530c0)


### Gulp 4: Ejemplo

```javascript
var gulp = require('gulp');
var less = require('gulp-less');
var babel = require('gulp-babel');
var concat = require('gulp-concat');
var uglify = require('gulp-uglify');
var rename = require('gulp-rename');
var cleanCSS = require('gulp-clean-css');
var del = require('del');

var paths = {
  styles: {
    src: 'src/styles/**/*.less',
    dest: 'assets/styles/'
  },
  scripts: {
    src: 'src/scripts/**/*.js',
    dest: 'assets/scripts/'
  }
};

/* Not all tasks need to use streams, a gulpfile is just another node program
 * and you can use all packages available on npm, but it must return either a
 * Promise, a Stream or take a callback and call it
 */
function clean() {
  // You can use multiple globbing patterns as you would with `gulp.src`,
  // for example if you are using del 2.0 or above, return its promise
  return del([ 'assets' ]);
}

/*
 * Define our tasks using plain functions
 */
function styles() {
  return gulp.src(paths.styles.src)
    .pipe(less())
    .pipe(cleanCSS())
    // pass in options to the stream
    .pipe(rename({
      basename: 'main',
      suffix: '.min'
    }))
    .pipe(gulp.dest(paths.styles.dest));
}

function scripts() {
  return gulp.src(paths.scripts.src, { sourcemaps: true })
    .pipe(babel())
    .pipe(uglify())
    .pipe(concat('main.min.js'))
    .pipe(gulp.dest(paths.scripts.dest));
}

function watch() {
  gulp.watch(paths.scripts.src, scripts);
  gulp.watch(paths.styles.src, styles);
}

/*
 * You can use CommonJS `exports` module notation to declare tasks
 */
exports.clean = clean;
exports.styles = styles;
exports.scripts = scripts;
exports.watch = watch;

/*
 * Specify if tasks run in series or parallel using `gulp.series` and `gulp.parallel`
 */
var build = gulp.series(clean, gulp.parallel(styles, scripts));

/*
 * You can still use `gulp.task` to expose tasks
 */
gulp.task('build', build);

/*
 * Define default task that can be called by just running `gulp` from cli
 */
gulp.task('default', build);
```

### Grunt vs. Gulp

  ![gulp_vs_grunt](http://theodorelee.com/wp-content/uploads/2015/04/grunt-vs-gulp.jpg)

Grunt:

![Grunt_WF](http://frontendlabs.io/wp-content/uploads/2014/08/grunt-file-manipulation.png)

Gulp:

![Gulp_WF](http://frontendlabs.io/wp-content/uploads/2014/08/gulp-file-manipulation.png)



### Yeoman
![Yeoman Logo](https://raw.githubusercontent.com/yeoman/media/master/optimized/yeoman-masthead.png)
> The Yeoman workflow comprises three types of tools for improving your productivity and satisfaction when building a web app: the scaffolding tool (yo), the build tool (Grunt, Gulp, etc) and the package manager (like Bower and npm).

- [Yeoman Instalation Working Flow](https://www.youtube.com/watch?v=zBt2g9ekiug)
- [Yeoman - Generator-webapp](https://github.com/yeoman/generator-webapp)
- [Yeoman - Santa Barbara JavaScript Meetup](http://www.slideshare.net/tim_doherty/yeoman-santa-barbara-bjava-scriptmeetup)
- [Automating Your Front-end Workflow with Yeoman 1.0 (Addy Osmani)](https://www.youtube.com/watch?v=1OAfGm_cI6Y)


### Yeoman: Instalación
Instalamos Yeoman global (incluye Grunt, Bower...)
```
  npm install yo -g
```

Instalamos globalmente el generador de proyectos web
```
  npm install --global generator-gulp-webapp
```

En la carpeta deseada lanzamos el generador para que se cree un pryecto completo
```
  yo gulp-webapp
```

Acabada la instalación con exito
```
  gulp serve
```

Preparando todo para producción
```
  gulp
```

### Yeoman: Gestión de errores

Verificamos que es lo que no funciona.
```
  yo doctor
```

*Resultado esperado:*
```
Yeoman Doctor
Running sanity checks on your system

✔ Global configuration file is valid
✔ Node.js version
✔ No .bowerrc file in home directory
✔ No .yo-rc.json file in home directory
✔ npm version
✔ NODE_PATH matches the npm root
```


### Yeoman: [Generadores populares](http://yeoman.io/generators/)

*Nota: Los :small_blue_diamond: son generadores creados por el equipo de Yeoman y se consideran `generadores oficiales`* 

**:top: downloads**
- [ hyperledger-composer](https://github.com/hyperledger/composer#readme): *Generates projects from Hyperledger Composer business network definitions*
- [ jhipster](http://www.jhipster.tech/): *Spring Boot + Angular in one handy generator*
- [ kittn](https://github.com/kittn/generator-kittn#readme): *Kittn Scaffolding and Frontend Toolchain*
- [ garlic-webapp](https://github.com/molnarzs/generator-garlic-webapp#readme): *Generator for GarlicTech webapps*
- [ loopback](https://github.com/strongloop/generator-loopback#readme): *LoopBack*
- [ baukasten](https://github.com/davidhellmann/generator-baukasten#readme): *A little 'Baukasten' for your next project to gettings shit done. It's focused on Craft CMS but there is also a bit WordPress stuff on board*
- [ talend](https://github.com/Talend/ui/tree/master/packages/generator#readme): *Talend's JavaScript generator*
- [ swiftserver](https://github.com/IBM-Swift/generator-swiftserver#readme): *Generator for Kitura REST webservice servers*
- [ ibm-service-enablement](https://github.com/ibm-developer/generator-ibm-service-enablement#readme): *This generator adds Service enablement toapps*
- [ code](http://code.visualstudio.com/): *Visual Studio Code Extensions*
- [ dhboilerplate](https://davidhellmann.com/): *Boilerplate made by David Hellmann #gulp #npm #craftcms #wordpress #vue #twig*
- [ phaser-h5](https://github.com/Sanchez3/generator-phaser-h5): *Generate h5 games with phaser.js or not, based on Gulp!*
- [:small_blue_diamond: angular](https://github.com/yeoman/generator-angular#readme): *AngularJS*
- [ primer-module](https://github.com/primer/primer#readme): *Use this to create a new Primer modules!*
- [ feathers](https://github.com/feathersjs/generator-feathers): *A Feathersapp*
- [ angular-fullstack](https://github.com/angular-fullstack/generator-angular-fullstack): *Creating MEAN stackapps, using MongoDB, Express, AngularJS, and Node*
- [ hubot](https://github.com/github/generator-hubot#readme): *Hubot*
- [ dmninteractives](https://github.com/DallasMorningNews/generator-dmninteractives#readme): *Interactive pages at The Dallas Morning News*
- [ fabric-composer](https://github.com/hyperledger/composer#readme): *Generates skeleton projects from Hyperledger Composer business network definitions*
- [ weex-plugin](https://github.com/weexteam/weex-plugin-template#readme): *>*
- [ donejs](http://donejs.com/): *Aur DoneJSapp*
- [ feathers-plugin](https://github.com/feathersjs/generator-feathers-plugin): *A generator for Feathersjs Plugins*
- [:small_blue_diamond: mocha](https://github.com/yeoman/generator-mocha#readme): *Mocha*
- [:small_blue_diamond: karma](https://github.com/yeoman/generator-karma#readme): *Karma*
- [ nitro](https://github.com/namics/generator-nitro#readme): *The nitro frontend framework*
- [ toolbox](http://frontend.github.io/toolbox/): *Generator*
- [ jhipster-primeng](https://github.com/sudheerj/generator-jhipster-primeng): *Generate PrimeNG Components*
- [ daggerok-fatjar](https://github.com/daggerok/generator-daggerok-fatjar): *Generate fat-jar java / java-ee / scala projects*
- [ license](https://github.com/jozefizso/generator-license): *Licensebased projects*
- [ ibm-usecase-enablement](https://github.com/ibm-developer/generator-ibm-usecase-enablement#readme): *Generator to add usecase enablement*
- [:small_blue_diamond: webapp](https://github.com/yeoman/generator-webapp#readme): *Scaffold out a front-end web app*
- [:small_blue_diamond: jasmine](https://github.com/yeoman/generator-jasmine#readme): *Jasmine*
- [ office](https://github.com/officedev/generator-office): *Creating Microsoft Office projects using any text editor*
- [ npm-wp-s-theme](https://github.com/mnyorba/generator-npm-wp-s-theme): *A WordPress starter theme (using Underscores) with npm and other good stuff*
- [ terminus-ui](https://github.com/GetTerminus/generator-terminus-ui): *A generator for adding new components to the Terminus UI library*
- [ git](https://documentup.com/kikobeats/generator-git): *Create the configurable scaffolding to start with a git-like project*
- [ ibm-core-node-express](https://github.com/ibm-developer/generator-ibm-core-node-express#readme): *Core node expressapp*
- [ travis](https://github.com/iamstarkov/generator-travis#readme): *Get and keep `.travis.yml` up-to-date effortlessly*
- [ keystone](https://github.com/keystonejs/generator-keystone): *A KeystoneJS Project*
- [ codenut](https://github.com/uznam8x/generator-codenut#readme): *Yoman generator codenut for website*
- [ stereobase](https://github.com/stereosuper/generator-stereobase#readme): *Generate a simple template based on 7-1 architecture, with the opportunity to use Twig and GSAP*
- [:small_blue_diamond: generator](https://github.com/yeoman/generator-generator#readme): *Generate generator*
- [ hughes](http://yeoman.io/generators/coloradohughes.com): *Web development generator for Kevin Hughes*
- [ express](https://github.com/petecoop/generator-express): *A nodejs express*
- [ ng-fullstack](https://github.com/ericmdantas/generator-ng-fullstack#readme): *Client, server or fullstack - it's up to you. ng-fullstack gives you the best of the latest: Node, Go, HTTP/2, Angular 1, Angular 2, Vue, Aurelia, Express, Koa, Echo, Gin, MongoDB, Gulp, Babel, Typescript and much more*
- [ openapi-repo](https://github.com/Rebilly/generator-openapi-repo#readme): *OpenAPI(fka Swagger) repo to help you share spec for your API*
- [ cicero-template](https://github.com/accordproject/cicero#readme): *Code generator for a Cicero Template*
- [ cozen-angular](https://github.com/C0ZEN/generator-cozen-angular): *Use this help you create AngularJSapps based to works properly with the Altran Angular Library*
- [ spring-microservice](https://github.com/NationalLibraryOfNorway/generator-spring-microservice): *Microservice with Maven + Spring + Netflix + Docker*
- [ tcg](https://github.com/jeffreysbrother/generator-tcg#readme): *Rename stuff!*
- [:small_blue_diamond: node](https://github.com/yeoman/generator-node): *Create a Node.js module*
- [ rn-toolbox](https://github.com/bamlab/generator-rn-toolbox#readme): *React-Native generators to kickstart your project*
- [ sublime](https://github.com/mcfly-io/generator-sublime#readme): *Scaffolfding the standard configuration root files like .gitignore, .jshintrc, .jscsrc etc..*
- [ aspnet](https://github.com/omnisharp/generator-aspnet#readme): *ASP.NET Core apps*
- [ typescript-microservice](https://github.com/lifegadget/generator-typescript-microservice#readme): *A NodeJS generator for Node/TypeScript which leverages 'serverless' to be deployable to all the major cloud platforms*
- [ liferay-theme](https://github.com/liferay/generator-liferay-theme#readme): *Creating Liferay themes*
- [ angular2-library](https://github.com/jvandemo/generator-angular2-library): *Generator to create an Angular 2 library*
- [ webappstarter](https://github.com/unbug/generator-webappstarter#readme): *Quick start a web app for mobile.Automatically adjusts according to a device’s screen size without any extra work*
- [ liveblog-theme](https://github.com/liveblog/generator-liveblog-theme#readme): *Generator*
- [ bannertime](https://github.com/bannertime/generator-bannertime): *Creating HTML5 advertising campaigns*
- [ jest](https://github.com/SBoudrias/generator-jest#readme): *Add jest support to any projects*
- [ aem-component](https://github.com/Blainegunn/generator-aem-component#readme): *A basic conponent generator for Adobe Expirecne Manager (AEM)*
- [ fountain-react](http://fountainjs.io/): *Fountain generator to scaffold a webapp with React written in ES6 (Babel), TypeScript through Webpack or SystemJS including tools Gulp 4, ESLint, Browsersync and Karma*
- [ sppp](https://github.com/koltyakov/generator-sppp): *SharePoint Pull-n-Push - client-side development*
- [ dizmo](https://github.com/dizmo/yeoman-generator-dizmo): *DizmoGen: a generator for dizmo projects*
- [ ng-poly](https://github.com/dustinspecker/generator-ng-poly#readme): *Modular AngularJS apps with Gulp and optional Polymer support*
- [ giraffe](https://github.com/tsukasa-web/generator-giraffe): *A generator for html5 website*
- [ nodeserver](https://github.com/ibm-developer/generator-nodeserver#readme): *Generates a nodeserver project*
- [ phaser-plus](https://github.com/rblopes/generator-phaser-plus/tree/master/packages/generator-phaser-plus#readme): *Create Phaser Web games with ease*
- [ aspnetcore-spa](https://github.com/aspnet/JavaScriptServices#readme): *DEPRECATED. Do not use. Use 'dotnet new' to create ASP.NET Core Single-Pageappprojects instead*
- [ canner-react](https://github.com/canner/generator-canner-react#readme): *A generator for react projects*
- [ react-webpack](https://github.com/react-webpack-generators/generator-react-webpack#readme): *Using React with Webpack via Babel*
- [ react-skeleton](https://github.com/fiWhy/Yo-React-Skeleton#readme): *React 16 skeleton*
- [ skinny](https://github.com/skinny-framework/skinny-framework): *A generator for Skinny framework which is a 'Scala on Rails'*
- [ screwdriver](https://github.com/screwdriver-cd/generator-screwdriver): *Make a new npm module for use in the Screwdriver project*
- [ fountain-angular1](http://fountainjs.io/): *Fountain generator to scaffold a webapp with Angular 1 written in ES6 (Babel), TypeScript through Webpack or SystemJS including tools Gulp 4, ESLint, Browsersync and Karma*
- [ yeogurt](https://github.com/larsonjj/generator-yeogurt): *A generator for creating static sites. Helps you harness the power of your favorite tools: Jade or Nunjucks, Gulp, ES6/2015, and much more!*
- [ bpnr](http://bpnr.co.kr/): *BPNR Dev standard generator*
- [ electrode](http://www.electrode.io/): *Generate Electrode React App*
- [ openhab](https://github.com/kubawolanin/generator-openhab): *Generates simple openHAB items and sitemaps for your home*
- [ ng-component](https://github.com/daftmonk/generator-ng-component#readme): *Generator*
- [ jhipster-nav-element](https://github.com/vivekmore/generator-jhipster-nav-element): *A generator to scaffold a new page (and the corresponding navigation menu) in a JHipster project*
- [ python-lib](https://gitlab.com/hyper-expanse/generator-python-lib#readme): *Generator for bootstrapping a Python library*
- [ jhipster-docker](https://github.com/pascalgrimaud/generator-jhipster-docker): *Additional Docker support: Docker Hub, Local SMTP Server, NGinx*
- [ fountain-webapp](http://fountainjs.io/): *Fountain generator to scaffold a webapp with React or Angular written in ES6 (Babel), TypeScript through Webpack or SystemJS including tools Gulp 4, ESLint, Browsersync and Karma*
- [ folklore](https://github.com/Folkloreatelier/folklore-js/tree/master/packages/generator-folklore#readme): *Projects at Folklore*
- [ fountain-angular2](http://fountainjs.io/): *Fountain generator to scaffold a webapp with Angular 2 written in ES6 (Babel), TypeScript through Webpack or SystemJS including tools Gulp 4, ESLint, Browsersync and Karma*
- [ jhipster-entity-audit](https://github.com/hipster-labs/generator-jhipster-entity-audit): *JHipster module to enable entity audit and audit log page*
- [ electric](http://electricjs.com/): *Creating documentation sites using electric.js*
- [ fountain-vue](https://github.com/fountainjs/generator-fountain-vue#readme): *Fountain generator to scaffold a webapp with Vue.js written in ES6 (Babel) through Webpack including tools Gulp 4, ESLint, Browsersync and Karma*
- [ tsoa-bootstrap](https://github.com/jeremyoverman/generator-tsoa-bootstrap#readme): *TSOA, Sequelize, and Jasmine scaffolding including model, test, controller, and migration creation*
- [ jhipster-elasticsearch-reindexer](https://github.com/geraldhumphries/generator-jhipster-elasticsearch-reindexer): *Generates a service that reindexes all database rows for each of your entities*
- [ craftplugin](https://github.com/nystudio107/generator-craftplugin#readme): *Generator-craftplugin is Craft CMS plugins*
- [ jhipster-ci](https://github.com/pascalgrimaud/generator-jhipster-ci): *JHipster module, Continuous Integration support in your JHipsterapp*
- [ totem](https://github.com/toolbarthomas/generator-totem#readme): *Creating Totem projects & modules*
- [ ehi-compgen](https://www.eventhi.io/): *Used internally by the EventHi team to generate new components boilerplate*
- [ meanjs](https://github.com/meanjs/generator-meanjs#readme): *MEAN.JS Official Generator*
- [ ngx-rocket](https://github.com/ngx-rocket/generator-ngx-rocket): *Extensible Angular 5+ enterprise-grade project generator based on angular-cli with best practices from the community. Includes PWA and Cordova support, coding guides and more!*
- [ clam](https://github.com/jayli): *A Clam*
- [ bitch](https://github.com/darlanmendonca/generator-bitch): *A simple generator (for Yeoman) to scaffolding webapps, just frontend stack*
- [ sanji-ui](https://github.com/Sanji-IO/generator-sanji-ui#readme): *Sanji UI generator*
- [ yx](https://github.com/huyaxiong/generator-yx#readme): *Full stack javascript project scaffold*
- [ node-oss](https://github.com/luftywiranda13/generator-node-oss#readme): *Create a Node.js project with ease*
- [ jhipster-swagger2markup](https://github.com/atomfrede/generator-jhipster-swagger2markup): *JHipster module to create nice looking static api docs with swagger2markup*
- [ static-website](https://github.com/claudetech/generator-static-website#readme): *Generator to create static websites*
- [ gulp-angular](https://github.com/swiip/generator-gulp-angular#readme): *AngularJS with Gulp*
- [ angular-page](https://github.com/thepipecat/yo-angular-page#readme): *Yeoman.io generator fo Angular.io page with routing*
- [ jhipster-bootstrap-material-design](https://github.com/moifort/generator-jhipster-bootstrap-material-design): *Add Material design to your JHipsterapp*
- [ angular-famous-ionic](https://github.com/thaiat/generator-angular-famous-ionic#readme): *Scaffolding an app using angularjs browserify and famous*
- [ yi-frames](https://github.com/mapkab/generator-yiframes#readme): *The Frames of Yi-Front-End-Development-Team*
- [ qmui](http://qmuiteam.com/web/): *QMUI Web*
- [ adaptivejs](https://github.com/mobify): *A*
- [ angular-material](https://github.com/iansawyerva/generator-angular-material): *Google's Angular Material*
- [ cat](https://github.com/HsuTing/generator-cat): *Generator cat*
- [ tymlez-plugin](https://www.tymlez.com/): *Tymlez NextGen RTappscaffolding*
- [ prototype](https://github.com/Prototype-Group/generator-prototype#readme): *Scaffold modern frontend web apps with Assemble, Grunt, Sass and Bower. Use modern frameworks like Bourbon, Bootstrap, Foundation and structure the web app with Backbone and RequireJS*
- [ vintage-frontend](https://github.com/Vintage-web-production/generator-vintage-frontend): *Modern front-end workflow generator*
- [ abas-dashboard-widget](https://abas-erp.com/): *This creates basic file structures to develop and test abas dashboard widgets*
- [ rc](https://github.com/react-component/generator-rc#readme): *React component*
- [ hoop-django](http://www.hoopcommunication.it/): *A generator to start a django project*
- [ bunny](https://github.com/luftywiranda13/generator-bunny#readme): *Jumpstart node module, like a bunny*
- [ rest](https://github.com/diegohaz/generator-rest): *RESTful API generator using NodeJS, Express and MongoDB. Watch https://youtu.be/6x-ijyG-ack*
- [ teka](http://www.mmda.com.br/): *Create a brand new teka theme*
- [ ng2-webpack](https://github.com/cmelion/generator-ng2-webpack): *An opinionated tool for scaffolding an app using angular2 and webpack*
- [ cg-angular](https://github.com/cgross/generator-cg-angular): *Enterprise Angular projects*
- [ git-init](https://github.com/iamstarkov/generator-git-init#readme): *Simply `git init` and optional `init` commit*
- [ jhipster-pages](https://github.com/Magillem/generator-jhipster-pages): *Create pages : client only (static), or client and server side. Load data from server, Save data to server, form, table..*
- [ xf](https://github.com/larchanka/generator-xf): *XFramework*
- [ iojs](https://github.com/joeybaker/generator-iojs): *A basic node module template, that includes handy git hooks, a release script, and auto-changelog generation*
- [ simple-static-blog](https://github.com/matthewbdaly/generator-simple-static-blog#readme): *Generating a static blog*
- [ express-no-stress-typescript](https://github.com/cdimascio/generator-express-no-stress-typescript#readme): *Create awesome APIs with Typescript, ExpressJS and Swagger*
- [ jhipster-ionic](https://github.com/oktadeveloper/generator-jhipster-ionic): *A JHipster Module that generates an Ionic Client*
- [ jhipster-postgresuuid-converter](https://github.com/amitjindal/generator-jhipster-postgresuuid-converter): *Postgresql Long to UUID converter*
- [ moda](https://github.com/johannesjo/generator-modular-angular#readme): *A truly modular AngularJS all device apps*
- [ bfee-blankrepo](https://github.com/brennanfee/generator-bfee-blankrepo): *Yoeman generator to create a blank starter repo*
- [ speedseed](https://github.com/ifedu/generator-speedseed): *Oriented to components, allow create/choice template, multiple configuration with easy maintenance*
- [ typings](https://github.com/typings/generator-typings): *Create typings repository for `typings` (https://github.com/typings/typings)*
- [ jhipster-spring-social-connectors](https://github.com/moifort/generator-jhipster-spring-social-connectors): *Add Spring social connector to your JHipsterapp*
- [ mytime-ng2component](https://github.com/gion/generator-ng2component#readme): *An angular 2 component/service generator for all platforms based on new namespace '@angular/core' powered by yeoman. Forked from https://github.com/SteveZheng-BSFT/generator-ng2component*
- [ nuxeo](https://www.nuxeo.com/): *Nuxeo Generator based on Yeoman*
- [ confit](https://github.com/odecee/generator-confit#readme): *Creating the development process, tools and a sample project for current-generation webapps*
- [ future-static](https://github.com/future-team/generator-future-static#readme): *脚手架生成工具*
- [ mean-seed](https://github.com/notorii/generator-mean-seed): *MEAN-seed - AngularJS and node.js responsive/cross-platform/mobile ready app/website*
- [ material-app](https://github.com/michaelkrone/generator-material-app#readme): *Generates a material webappwith AngularJS, Express and Mongoose*
- [ ideil-atom](https://github.com/ideil/generator-ideil-atom#readme): *Ideil Atom*
- [ swaggerize](https://github.com/krakenjs/generator-swaggerize#readme): *OpenAPI(swagger)app*
- [ tabris-js](http://tabrisjs.com/): *Tabris.js*
- [ co-microservice](https://github.com/comparaonline/generator-co-microservice): *This bootstrap a microservice to run on the ComparaOnline infrastructure*
- [ panneau](https://github.com/Folkloreatelier/panneau-js): *Panneau*
- [ cappen-site](https://github.com/cappen): *Generator*
- [ jhipster-swagger-cli](https://github.com/cbornet/generator-jhipster-swagger-cli): *JHipster module to generate swagger client code from a swagger definition*
- [ kickoff](https://github.com/trykickoff/generator-kickoff): *The Kickoff front-end framework. Find out more at http://trykickoff.com*
- [ veams](http://veams.org/): *Scaffold modern frontend web apps or web pages with a static site generator, Grunt and/or Gulp, Sass and Bower. Use modern frameworks like Bourbon, Bootstrap or Foundation and structure your JavaScript with ES Harmony support*
- [ wejs](https://github.com/wejs/generator-wejs#readme): *We.js generate plugins, themes and projects*
- [ ng-panes](https://github.com/joelchu/generator-ng-panes#readme): *AngularJS 1.X, and support 8 UI frameworks. Part of the panes.js framework tool set. 前端开发神器!*
- [ famous](https://github.com/TheAlphaNerd): *Create new Famo.us projects*
- [ hfe](https://github.com/PaulGuo): *HFE*
- [ bcflow-library](https://github.com/the-bcflow/bcflow-template-library#readme): *A generator for build library*
- [ sp](https://github.com/snphq/generator-sp): *A*
- [ packing](https://github.com/packingjs/generator-packing#readme): *[packing](https://github.com/zhongzhi107/packing)*
- [ coffee-react](https://github.com/jhessin/generator-coffee-react#readme): *A simple project using create-react-app, coffeescript, and a custom version of react-hyperscript-helpers*
- [:small_blue_diamond: chrome-extension](https://github.com/yeoman/generator-chrome-extension#readme): *Scaffold out a Chrome extension*
- [ wordpress](https://github.com/wesleytodd/YeoPress): *WordPress*
- [ jhipster-entity-audit-and-delete](https://github.com/hipster-labs/generator-jhipster-entity-audit): *JHipster module to enable entity audit, add audit log page and allow to change default delete behavior*
- [ meshblu-connector](https://github.com/octoblu/generator-meshblu-connector): *A*
- [ angular2-application-scaffolder](https://github.com/ruffiem/generator-angular2-application-scaffolder): *Angular2appScaffolder is designed to be an applicationproviding a full stack working environment for Angular2 (beta 17+) developments*
- [ yohoho](https://github.com/jamrizzi/generator-yohoho): *Agenerators*
- [ jhipster-db-helper](https://github.com/bastienmichaux/generator-jhipster-db-helper): *A JHipster module for already existing databases*
- [ kevoree](https://github.com/kevoree/generator-kevoree): *A Kevoree project*
- [ scaffold](https://github.com/marcosmoura/generator-scaffold#readme): *Generator to automate the most common tasks in day-to-day of a Front End project*
- [ angular-eggs](https://github.com/albatrosary/generator-angular-eggs#readme): *Angular 1.5, Angular Component Router, Bootstrap v4(alpha) and TingoDB(like MongoDB) with an Express server*
- [ react-firebase](http://github.com/prescottprue/generator-react-firebase): *React and Firebase (with option for Redux) starter project generator*
- [ xiaoping-vue](https://github.com/excaliburhan/generator-xiaoping-vue#readme): *A generator for vue project*
- [ thundr-gae-react](https://github.com/3wks/generator-thundr-gae-react): *A React app that runs atop Thundr on Google App Engine*
- [ nightbird](https://github.com/AcklenAvenue/nightbird#readme): *Angular Web App*
- [ frontend](https://github.com/nDmitry/generator-frontend): *Scaffolds out a boilerplate for front-end development*
- [ ssm](https://github.com/ssmWebExpert/generator-ssm#readme): *Pug sass less generator with all we need modules*
- [ huddle](https://github.com/techmuch/generator-huddle#readme): *Generator*
- [ bespoke](https://github.com/bespokejs/generator-bespoke): *Create Bespoke.js presentations using Yeoman*
- [ devine-project](https://github.com/devinehowest/generator-devine-project#readme): *The one and only devine.be project generator*
- [ redux-stack](https://github.com/zakangelle/generator-redux-stack#readme): *A react/redux generator with all the build tooling goodies*
- [ polymer-element](https://github.com/seaneking/generator-polymer-element#readme): *Quickly scaffold lightweight Polymer 2 elements with Yeoman*
- [ tipicss](https://github.com/toolbarthomas/generator-tipicss): *Tipicss*
- [ bone](https://github.com/jiyutech/generator-bone.git): *The generator for koa by jiyu*
- [ dgp-api-aspnetcore](https://github.com/digipolisantwerp/generator-dgp-api-aspnetcore_yeoman): *Generator for an ASP.NET Core API project*
- [ symfonangular](https://github.com/zguillez): *PHP Symfony 3 framework with Javascript AngularJS framework integration for full stack development*
- [ politico-interactives](https://github.com/The-Politico/generator-politico-interactives#readme): *Interactive projects at POLITICO*
- [ mis](https://github.com/tbfe/generator-mis#readme): *百度贴吧MIS生成器*
- [ graphql](https://github.com/lucasbento/create-graphql#readme): *Create production-ready GraphQL servers*


**:top: stars**
- [ react-fullstack](https://github.com/kriasoft/react-starter-kit#readme): *React.js projects based on React Starter Kit (ES6+, Babel, React.js, Express, Webpack, BrowserSync)*
- [ jhipster](http://www.jhipster.tech/): *Spring Boot + Angular in one handy generator*
- [ react-native-ignite](https://github.com/infinitered/ignite#readme): *Create new react native files that fit the IR workflow*
- [ primer-module](https://github.com/primer/primer#readme): *Use this to create a new Primer modules!*
- [ angular-fullstack](https://github.com/angular-fullstack/generator-angular-fullstack): *Creating MEAN stackapps, using MongoDB, Express, AngularJS, and Node*
- [:small_blue_diamond: angular](https://github.com/yeoman/generator-angular#readme): *AngularJS*
- [ gulp-angular](https://github.com/swiip/generator-gulp-angular#readme): *AngularJS with Gulp*
- [ react-server](http://github.com/redfin/react-server): *A react-server generator*
- [:small_blue_diamond: webapp](https://github.com/yeoman/generator-webapp#readme): *Scaffold out a front-end web app*
- [ react-static](https://github.com/kriasoft/react-static-boilerplate#readme): *Project template for authoring stand-alone webapps (aka SPA) optmized for CDN hosting (in Fireabase). It's built upon best of breed technologies including React (ReactJS), Redux, Babel, Webpack, CSS Modules, PostCSS, Browsersync, HMR, React Hot L*
- [ react-webpack](https://github.com/react-webpack-generators/generator-react-webpack#readme): *Using React with Webpack via Babel*
- [:small_blue_diamond: chrome-extension](https://github.com/yeoman/generator-chrome-extension#readme): *Scaffold out a Chrome extension*
- [ ionic](https://github.com/diegonetto/generator-ionic): *A generator for the Ionic Framework*
- [ fluxible](https://github.com/yahoo/fluxible#readme): *Fluxible*
- [ arc](https://github.com/diegohaz/arc): *React app generator with Webpack, React Router, Jest, Redux, Server Side Rendering and more*
- [ nodejs-api](https://github.com/kriasoft/nodejs-api-starter#readme): *Node.js API Starter Kit built with Docker, Node.js, JavaScript (ES6, ES2015+ via Babel), PostgreSQL and GraphQL*
- [ graphql-server](https://github.com/kriasoft/graphql-starter-kit#readme): *GraphQL Starter Kit built with Node.js, JavaScript (ES2015+ via Babel) and PostgreSQL*
- [ electrode](http://www.electrode.io/): *Generate Electrode React App*
- [ wordpress](https://github.com/wesleytodd/YeoPress): *WordPress*
- [ starhackit](https://github.com/FredericHeem/starhackit): *Starhackit - Fullstack starterkit based on react and node*
- [ fountain-webapp](http://fountainjs.io/): *Fountain generator to scaffold a webapp with React or Angular written in ES6 (Babel), TypeScript through Webpack or SystemJS including tools Gulp 4, ESLint, Browsersync and Karma*
- [:small_blue_diamond: polymer](https://github.com/yeoman/generator-polymer#readme): *Scaffold out a Polymer project*
- [:small_blue_diamond: mobile](https://github.com/yeoman/generator-mobile): *Mobile based on Web Starter Kit*
- [ hyperledger-composer](https://github.com/hyperledger/composer#readme): *Generates projects from Hyperledger Composer business network definitions*
- [ relay-fullstack](http://lvarayut.github.io/relay-fullstack): *Relay Starter Kit integrated with Relay, GraphQL, Express, ES6/ES7, JSX, Webpack, Babel, Material Design Lite, and PostCSS*
- [ aspnetcore](https://github.com/kriasoft/aspnet-starter-kit#readme): *Stand-alone webapp(SPA) boilerplate built with ASP.NET Core, EF Core, Identity, C#, JavaScript, ES6/ES2015, Babel, Webpack, HMR, Browsersync, PostCSS, CSS Modules and more*
- [ aspnet](https://github.com/omnisharp/generator-aspnet#readme): *ASP.NET Core apps*
- [:small_blue_diamond: generator](https://github.com/yeoman/generator-generator#readme): *Generate generator*
- [ hottowel](https://github.com/johnpapa/generator-hottowel#readme): *HotTowel Angular*
- [ express](https://github.com/petecoop/generator-express): *A nodejs express*
- [ angular2-library](https://github.com/jvandemo/generator-angular2-library): *Generator to create an Angular 2 library*
- [ m-ionic](https://github.com/mwaylabs/generator-m-ionic#readme): *Advanced workflows for building rock-solid Ionic apps: develop, prototype, test, build and deliver high quality apps with Yeoman, Gulp, Bower, Angular, Cordova and of course Ionic. All in one sexy generator*
- [ ng-cli-lib](https://github.com/jvandemo/generator-angular2-library): *Generator to create an Angular 2 library*
- [ m](https://github.com/mwaylabs/generator-m#readme): *Generator-m*
- [ ng-fullstack](https://github.com/ericmdantas/generator-ng-fullstack#readme): *Client, server or fullstack - it's up to you. ng-fullstack gives you the best of the latest: Node, Go, HTTP/2, Angular 1, Angular 2, Vue, Aurelia, Express, Koa, Echo, Gin, MongoDB, Gulp, Babel, Typescript and much more*
- [:small_blue_diamond: backbone](https://github.com/yeoman/generator-backbone#readme): *Scaffold out a Backbone.js project*
- [ jekyllrb](https://github.com/robwierzbowski/generator-jekyllrb): *Supercharge Jekyll development with Yeoman. Yo, Jekyllrb!*
- [ cg-angular](https://github.com/cgross/generator-cg-angular): *Enterprise Angular projects*
- [ rest](https://github.com/diegohaz/generator-rest): *RESTful API generator using NodeJS, Express and MongoDB. Watch https://youtu.be/6x-ijyG-ack*
- [ react-cdk](https://github.com/kadirahq/react-cdk#readme): *React Component Development Kit*
- [ electron](https://github.com/sindresorhus/generator-electron#readme): *Scaffold out an Electron app boilerplate*
- [ rn-toolbox](https://github.com/bamlab/generator-rn-toolbox#readme): *React-Native generators to kickstart your project*
- [ react-webpack-redux](https://github.com/stylesuxx/generator-react-webpack-redux): *ReactJS and Flux (Redux) via Webpack*
- [ nm](https://github.com/sindresorhus/generator-nm#readme): *Scaffold out a node module*
- [ yeogurt](https://github.com/larsonjj/generator-yeogurt): *A generator for creating static sites. Helps you harness the power of your favorite tools: Jade or Nunjucks, Gulp, ES6/2015, and much more!*
- [ javascript](https://www.kriasoft.com/babel-starter-kit): *Generates a JavaScript library boilerplate for Node.js and the browser with ES6 / ES2015, ESLint, Babel, Mocha, Chai, Sinon, Istanbul, Coveralls..*
- [ meanjs](https://github.com/meanjs/generator-meanjs#readme): *MEAN.JS Official Generator*
- [:small_blue_diamond: node](https://github.com/yeoman/generator-node): *Create a Node.js module*
- [:small_blue_diamond: canner-node](https://github.com/yeoman/generator-node): *Create a Node.js module*
- [:small_blue_diamond: my-node](https://github.com/yeoman/generator-node): *Create a Node.js module*
- [:small_blue_diamond: ember](https://github.com/yeoman/generator-ember): *Ember*
- [ react-redux-universal](http://github.com/bertho-zero/react-redux-universal-hot-example): *A full-stack starter kit with react, redux and feathers*
- [ react-gulp-browserify](https://github.com/randylien/generator-react-gulp-browserify): *Facebook's React framework. It includes gulp, browserify, livereload and famous official Twitter bootstrap Sass version*
- [ reveal](https://github.com/slara/generator-reveal): *A Reveal.js*
- [ ngx-rocket](https://github.com/ngx-rocket/generator-ngx-rocket): *Extensible Angular 5+ enterprise-grade project generator based on angular-cli with best practices from the community. Includes PWA and Cordova support, coding guides and more!*
- [ ngx-app](https://github.com/angular-starter-kit/generator-ngx-app#readme): *Angular 4+ enterprise-grade project generator based on angular-cli with best practices from the community, a scalable starter template and a good learning base*
- [ ngx-core](https://github.com/angular-starter-kit/generator-ngx-app#readme): *Angular 2+ industrial project generator based on angular-cli with best practices from the community, a scalable starter template and a good learning base*
- [ rise](https://github.com/bucaran/generator-rise#readme): *Node module template for authoring with ES6+, Babel, Tape and npm scripts*
- [ style-prototype](https://github.com/north/generator-style-prototype): *Style prototypes*
- [ babel-boilerplate](https://github.com/babel/generator-babel-boilerplate): *Generate a boilerplate for a library written in ES2015 for Node and the browser*
- [ graphql](https://github.com/lucasbento/create-graphql#readme): *Create production-ready GraphQL servers*
- [ angular-famous-ionic](https://github.com/thaiat/generator-angular-famous-ionic#readme): *Scaffolding an app using angularjs browserify and famous*
- [ mcfly](https://github.com/mcfly-io/generator-mcfly#readme): *Scaffolding an app using angularjs browserify*
- [ marionette](https://github.com/mrichard/generator-marionette): *Express, Marionette and Backbone with AMD*
- [ jekyllized](https://github.com/sondr3/generator-jekyllized#readme): *Jekyll to rapidly build sites using Gulp*
- [ flux](https://github.com/banderson/generator-flux-react): *App based on Facebook's Flux/React architecture*
- [ sails-rest-api](https://github.com/ghaiklor/generator-sails-rest-api): *Provides already configured and optimized Sails REST API with bundle of predefined features*
- [:small_blue_diamond: chromeapp](https://github.com/yeoman/generator-chromeapp): *Scaffold out a Chrome app*
- [ keystone](https://github.com/keystonejs/generator-keystone): *A KeystoneJS Project*
- [ racket](https://github.com/mohebifar/racket#readme): *Scaffold a universal reactapp*
- [ node-webkit](https://github.com/Dica-Developer/generator-node-webkit): *A generator for node-webkit*
- [ webappstarter](https://github.com/unbug/generator-webappstarter#readme): *Quick start a web app for mobile.Automatically adjusts according to a device’s screen size without any extra work*
- [ docker](https://github.com/Microsoft/generator-docker#readme): *Docker generator*
- [ aws-lambda-dotnet](https://github.com/aws/aws-lambda-dotnet/tree/master/Blueprints): *A collection of generators for writing .NET Core AWS Lambda functions and AWS Serverlessapps*
- [ angular2](https://github.com/swirlycheetah/generator-angular2): *Angular2 Generator*
- [ react-aspnet-boilerplate](https://github.com/pauldotknopf/react-aspnet-boilerplate): *A boiler plate for getting started with ASP.NET projects using react/redux/universal-rendering*
- [ yo-wordpress](https://github.com/romainberger/yeoman-wordpress): *Wordpress projects and plugins*
- [ phaser](https://github.com/julien/generator-phaser): *Generate HTML5 games with phaser.js*
- [ redux](https://github.com/banderson/generator-redux#readme): *CLI for Redux: next-gen functional Flux/React with devtools*
- [ ng-poly](https://github.com/dustinspecker/generator-ng-poly#readme): *Modular AngularJS apps with Gulp and optional Polymer support*
- [ h5bp](https://github.com/h5bp/generator-h5bp#readme): *HTML5 Boilerplate generator*
- [ express-no-stress](https://github.com/cdimascio/generator-express-no-stress#readme): *Create awesome APIs with ExpressJS and Swagger*
- [ zf5](https://github.com/juliancwirko/generator-zf5): *Zurb Foundation 5*
- [ react-component](https://github.com/JedWatson/generator-react-component): *ReactJS Component projects*
- [ angular-flask](https://github.com/rayokota/generator-angular-flask): *AngularJS + Flask*
- [ angularfire](https://github.com/firebase/generator-angularfire): *Angular+Firebase*
- [ plugin-wp](https://github.com/WebDevStudios/generator-plugin-wp#readme): *WordPress plugins*
- [:small_blue_diamond: bootstrap](https://github.com/yeoman/generator-bootstrap#readme): *Bootstrap*
- [ chrome-extension-kickstart](https://github.com/HaNdTriX/generator-chrome-extension-kickstart#readme): *Generator*
- [ angular-go-martini](https://github.com/rayokota/generator-angular-go-martini): *AngularJS + Go + Martini*
- [ material-app](https://github.com/michaelkrone/generator-material-app#readme): *Generates a material webappwith AngularJS, Express and Mongoose*
- [ api](https://github.com/ndelvalle/generator-api#readme): *Creating RESTful NodeJS APIs, using ES6, Mongoose and Express*
- [ bespoke](https://github.com/bespokejs/generator-bespoke): *Create Bespoke.js presentations using Yeoman*
- [ wp-make](https://github.com/10up/generator-wp-make#readme): *Generator*
- [ mean-seed](https://github.com/notorii/generator-mean-seed): *MEAN-seed - AngularJS and node.js responsive/cross-platform/mobile ready app/website*
- [ angular-require](https://github.com/aaronallport/generator-angular-require#readme): *AngularJS using RequireJS*
- [:small_blue_diamond: karma](https://github.com/yeoman/generator-karma#readme): *Karma*
- [ office](https://github.com/officedev/generator-office): *Creating Microsoft Office projects using any text editor*
- [ node-typescript](https://github.com/ospatil/generator-node-typescript#readme): *A minimal creating NodeJS modules using TypeScript*
- [ canner-node-typescript](https://github.com/ospatil/generator-node-typescript#readme): *A minimal creating NodeJS modules using TypeScript*
- [ flux-on-rails](https://github.com/alexfedoseev/generator-flux-on-rails#readme): *Scaffolder of isomorphic/universal Flux app, backed by Rails API*
- [ jhipster-react](https://github.com/deepu105/generator-jhipster-react): *A Jhipster based generator to create react + spring bootapp*
- [ react-on-rails](https://github.com/alexfedoseev/generator-react-on-rails): *Scaffolder of isomorphic NodeJS & ReactJS app, backed by Rails API*
- [ test](https://github.com/phillipalexander/generator-test): *Based generator that creates a simple mocha/chai TDD scaffold for solving algorithms*
- [ angular-webpack-es6](https://github.com/STUkh/generator-angular-webpack-es6#readme): *Angular Webpack ES6 generator. Uses SASS as CSS preprocessor, UI router as default angular router, LazyLoading example included. Inspired by generator-gulp-angular*
- [ meteor](https://github.com/Pent/generator-meteor): *A Meteor app*
- [ jquery-boilerplate](https://github.com/jquery-boilerplate/generator-jquery-boilerplate#readme): *JQuery Boilerplate*
- [ firefox-os](https://github.com/zenorocha/generator-firefox-os): *Firefox OS*
- [ meanstack](https://github.com/wlepinski/generator-meanstack): *The MEAN stack*
- [ angulpify](https://github.com/jgoux/generator-angulpify): *Involving AngularJS, Gulp and Browserify*
- [ openapi-repo](https://github.com/Rebilly/generator-openapi-repo#readme): *OpenAPI(fka Swagger) repo to help you share spec for your API*
- [ gulp-ng](https://github.com/henyojess/generator-gulp-ng): *Gulp+angular*
- [ ionic-gulp](https://github.com/tmaximini/generator-ionic-gulp#readme): *Ionic projects with gulp*
- [ micro-service](https://github.com/vadimdemedes/generator-micro-service#readme): *Kickstart your microservice with `micro` and `ava`!*
- [ hubot](https://github.com/github/generator-hubot#readme): *Hubot*
- [ bootstrap-less](https://github.com/Thomas-Lebeau/generator-bootstrap-less): *Bootstrap less*
- [ bangular](https://github.com/42Zavattas/generator-bangular): *Generate and serve your project in a blink of an eye*
- [ patternlab](http://degdigital.github.io/generator-patternlab/): *Pattern Lab Generator*
- [ chisel](https://github.com/xfiveco/generator-chisel#readme): *Scaffolding front-end and WordPress projects*
- [ server-configs](https://github.com/h5bp/generator-server-configs): *Scaffolds out webserver configuration for various platforms. Goes well with HTML5 Boilerplate*
- [ element](https://github.com/webcomponents/generator-element): *Create Custom Elements using Polymer, X-Tag or VanillaJS*
- [ react-firebase](http://github.com/prescottprue/generator-react-firebase): *React and Firebase (with option for Redux) starter project generator*
- [ loopback](https://github.com/strongloop/generator-loopback#readme): *LoopBack*
- [ mean](https://github.com/jrcryer/generator-mean): *MEAN stack, inspired by mean.io*
- [ htmlemail](https://github.com/jahvi/generator-htmlemail): *HTML Email boilerplate*
- [ assemble](https://github.com/assemble/generator-assemble): *Create new Assemble projects*
- [ rf](https://github.com/taiansu/generator-rf#readme): *RF: a React/Flux webapp generator with webpack, dialects and some good stuffs*
- [ ng2-webpack](https://github.com/cmelion/generator-ng2-webpack): *An opinionated tool for scaffolding an app using angular2 and webpack*
- [ code](http://code.visualstudio.com/): *Visual Studio Code Extensions*
- [ angularjs-library](https://github.com/jvandemo/generator-angularjs-library#readme): *Create an AngularJS component library*
- [ flight](https://github.com/flightjs/generator-flight): *Generator for scaffolding out a Flight web app*
- [ ngtailor](https://github.com/lauterry/generator-ngtailor): *Generator*
- [ jekyll-starter-kit](https://github.com/nirgn975/generator-jekyll-starter-kit): *Combine Jekyll and Google web-starter-kit to enjoy the best of both worlds*
- [ kraken](https://github.com/krakenjs/generator-kraken): *A kraken*
- [ ngbp](https://github.com/thardy/generator-ngbp): *Based on the ngBoilerplate kickstarter, a best-practice boilerplate for scalable Angular projects built on a highly modular, folder-by-feature structure. Now with easily switchable mocking via $httpBackend and RESTful resource scaffolding*
- [ angular-meteor](https://github.com/ndxbxrme/generator-angular-meteor): *Creating AngularJS + Meteorapps*
- [ threejs](https://github.com/timmywil/generator-threejs): *Three.js projects*
- [ angular-crud](https://github.com/jlmonteagudo/generator-angular-crud#readme): *Angular CRUD generator*
- [ hedley](https://github.com/gizra/generator-hedley#readme): *Headless Drupal, Angular app, and Behat framework*
- [ android-mvp-starter](https://github.com/ravidsrk/android-mvp-starter): *An MVP Boilerplate to save me having to create the same project over from scratch every time! :)*
- [ wbp](https://github.com/silvenon/generator-wbp#readme): *Scaffolds a modern workflow for starting a React app*
- [ nodex](https://github.com/NewbranLTD/generator-nodex#readme): *使用语言选项创建 node.js 模块 / Create a Node.js module with language option. Pass `nodex --lang=cn | en`*
- [ joli-symfony](https://github.com/jolicode/generator-joli-symfony#readme): *Scaffolds a standard Symfony2appwith Yeoman*
- [ angularjs-cordova](http://keshavos.github.io/generator-angularjs-cordova): *Combines the best features and practices to initialise and scaffold an AngularJS based cordova mobile app using a module based approach. Includes Angular UI, Bootstrap 3*
- [ electric](http://electricjs.com/): *Creating documentation sites using electric.js*
- [ esri-appbuilder-js](https://github.com/Esri/generator-esri-appbuilder-js#readme): *Help customize the ArcGIS Web AppBuilder*
- [ fountain-vue](https://github.com/fountainjs/generator-fountain-vue#readme): *Fountain generator to scaffold a webapp with Vue.js written in ES6 (Babel) through Webpack including tools Gulp 4, ESLint, Browsersync and Karma*
- [ angular-xl](https://github.com/kennethlynne/generator-angular-xl): *Custom AngularJS*
- [ hapi-style](https://github.com/jedireza/generator-hapi-style): *Scaffolding hapi apps and plugins*
- [ wp-theme](https://github.com/danielauener/generator-wp-grunted-theme): *A WordPress theme generator, to kickstart WordPress theme development with yo, sass and grunt*
- [ bones](https://github.com/matt-bailey/generator-bones): *Scaffolding out a basic web project*
- [ dyno](https://github.com/jhendley25/generator-dyno): *ES6-ready Javascript, with Browserify, Gulp, and Jade*
- [ thorax](https://github.com/walmartlabs/generator-thorax): *A Thorax*
- [ fountain-angular1](http://fountainjs.io/): *Fountain generator to scaffold a webapp with Angular 1 written in ES6 (Babel), TypeScript through Webpack or SystemJS including tools Gulp 4, ESLint, Browsersync and Karma*
- [ react-reflux](https://github.com/tfaga/generator-react-reflux): *Facebook's React framework and flux architecture using reflux*
- [ keystone-react](http://keystonejs.com/): *KeystoneJS + ReactappGenerator*
- [ fountain-angular2](http://fountainjs.io/): *Fountain generator to scaffold a webapp with Angular 2 written in ES6 (Babel), TypeScript through Webpack or SystemJS including tools Gulp 4, ESLint, Browsersync and Karma*
- [ vuejs](https://github.com/birdeggegg/generator-vuejs#readme): *A simple Vue + Webpack generator*
- [ create-redux-app](https://github.com/jonidelv/generator-create-redux-app): *Add Redux, styled-components and other useful libraries like Generators in top of create-react-app*
- [:small_blue_diamond: jquery](https://github.com/yeoman/generator-jquery#readme): *Generate a jQuery plugin*
- [ angular-express-sequelize](https://github.com/rayokota/generator-angular-express-sequelize): *AngularJS + Express + Sequelize*
- [ appx](https://github.com/MicrosoftEdge/generator-appx#readme): *Windows 10 App Build System*
- [ aio-angular](https://github.com/pinkyjie/generator-aio-angular#readme): *All In One AngularJS generator*
- [ modern-frontend](https://github.com/endel/generator-modern-frontend#readme): *Scaffold out a modern front-end web app*
- [ hexo-theme](https://github.com/tcrowe/generator-hexo-theme#readme): *Create hexo themes like crazy!*
- [ django](https://github.com/diegotoral/generator-django): *A*
- [ react-webpack-alt](https://github.com/weblogixx/generator-react-webpack-alt): *ReactJS and Flux (alt.js) via Webpack*
- [ mobile-boilerplate](https://github.com/h5bp/generator-mobile-boilerplate#readme): *H5BP Mobile Boilerplate generator*
- [ flask](https://github.com/romainberger/yeoman-flask): *Flask project*
- [ kibana-plugin](https://github.com/elastic/generator-kibana-plugin#readme): *A Kibana plugin*
- [ aurelia](https://github.com/zewa666/generator-aurelia#readme): *The JavaScript Framework Aurelia*
- [ laravel](https://github.com/Freyskeyd/generator-laravel): *A generator for Laravel (with Yeoman)*
- [:small_blue_diamond: gruntfile](https://github.com/yeoman/generator-gruntfile): *A gruntfile*
- [ modern-web-dev](https://npmjs.com/package/generator-modern-web-dev): *Modern Web Development Generator: Gulp, ES2015, TypeScript, Angular 2, SASS, Minification, Bundling, Sourcemaps, ..*
- [ phaser-plus](https://github.com/rblopes/generator-phaser-plus/tree/master/packages/generator-phaser-plus#readme): *Create Phaser Web games with ease*
- [ angm](https://github.com/newaeonweb/generator-angm#readme): *AngularJS help you getting started with a new project based on AngularJS and Angular Material to build large scaleapps*
- [ awesome-list](https://github.com/dar5hak/generator-awesome-list#readme): *GitHub awesome lists 😎*
- [ gulp-bootstrap](https://github.com/niallobrien/generator-gulp-bootstrap): *Scaffold out a front-end web app using Sass (node-sass) by default*
- [ angular-ui-router](https://github.com/yeoman/generator-angular): *AngularJS( include UI-router )*
- [ alfred](https://github.com/samverschueren/generator-alfred#readme): *Scaffold out an Alfred workflow*
- [ ghost](https://github.com/sethvincent/generator-ghost): *Generate Ghost blogs and themes using Yeoman*
- [ gulp-angular2](https://github.com/x6doooo/generator-gulp-angular2#readme): *Angular2 + Gulp, base on angular2-seed and generator-gulp-angular*
- [ polymer-init-custom-build](https://github.com/PolymerElements/generator-polymer-init-custom-build#readme): *A starting point for building apps using Polymer Starter Kit with a custom gulp process leveraging polymer-build*
- [ ng-plugin](https://github.com/tinesoft/generator-ng-plugin#readme): *Bootstrap AngularJS plugin creation, with integrated demo app, continuous integration system, dependencies and code coverage status*
- [ koa](https://github.com/peter-vilja/generator-koa): *A Koa*
- [ ngx-library](https://github.com/tinesoft/generator-ngx-library#readme): *Bootstrap Angular library creation and publication, with integrated demo app, continuous integration/deployment system, code coverage status and much more!*
- [ angular-dropwizard](https://github.com/rayokota/generator-angular-dropwizard): *AngularJS + Dropwizard*
- [ angular-material-fullstack](https://github.com/sincraianul/generator-angular-material-fullstack): *Creating MEAN stackapps, using MongoDB, Express, AngularJS, and Node*
- [ nod](https://github.com/diegohaz/nod): *NodeJS modules generator with ES6 (Babel), Jest, Flow, Travis, Codecov, Documentation and more*
- [ standard-readme](https://github.com/RichardLitt/generator-standard-readme): *Scaffold out a Standard Readme*
- [ openui5](https://github.com/saschakiefer/generator-openui5): *OpenUI5*
- [ serverless-policy](https://github.com/dancrumb/generator-serverless-policy#readme): *Generator for the basic IAM policy to allow a user to deploy a Serverless service*
- [ angular-slim](https://github.com/rayokota/generator-angular-slim): *AngularJS + Slim*
- [ k](https://github.com/minghe/generator-k): *A best Koa generator*
- [ firefox-extension](https://github.com/dgil/generator-firefox-extension#readme): *Firefox Extensions*
- [ jsmodule](https://github.com/necolas/generator-jsmodule): *Generator for scaffolding out a JavaScript module for Node.js or the browser*
- [ mobx-react](https://github.com/cafreeman/generator-mobx-react): *A lightweight for generator for scaffolding new mobx-react projects*
- [ wp-bones](https://github.com/0dp/generator-wp-bones): *Installs Bones Wordpress starter theme into the current directory - goto the themes folder and run wp-bones*
- [ koa-rest](https://github.com/patrickwolleb/generator-koa-rest): *Generator*
- [ es6-angular](https://github.com/leftstick/generator-es6-angular): *Generator-es6-angular*





**Scrip mágico**
```javascript
// Ejecutar en http://yeoman.io/generators/
var md = ""
function generateMd(dataItem){
	
	md += `**:top: ${dataItem}**\n`
	var datos = document.querySelectorAll(".list > tr")
	
	datos.forEach(function(dato){
		var linkSelector = dato.querySelector("a")
		var nameSelector = dato.querySelector(".name")
		var descripcionSelector = dato.querySelector(".description")
		var usefulldata;
		if(linkSelector && nameSelector){
			var usefulldata = {
				official: dato.classList.contains('official'),
				titulo: nameSelector.innerText,
				descripcion: descripcionSelector.innerText,
				link: linkSelector.href
			}		
		}
	
		if(usefulldata){
			md += `- [${usefulldata.official ? ":small_blue_diamond:": ""} ${usefulldata.titulo}](${usefulldata.link}): *${usefulldata.descripcion}*\n`;
		}
	})
	
	md += "\n\n"

}

function orderListBy (dataItem){
	document.querySelector(`[data-sort='${dataItem}']`).click()
}

function startSecuence(dataItem){
	orderListBy(dataItem)
	orderListBy(dataItem)
	generateMd(dataItem)
}

startSecuence("downloads")
startSecuence("stars")
console.log(md)
```


### Yeoman: ¡Hagamos nuestro generador! :muscle::muscle:

**Documentación**
- [Getting started](http://yeoman.io/authoring/index.html)
- [Running Context](http://yeoman.io/authoring/running-context.html)
- [User Interactions](http://yeoman.io/authoring/user-interactions.html)
- [Composability](http://yeoman.io/authoring/composability.html)
- [Managing Depedencies](http://yeoman.io/authoring/dependencies.html)
- [Interacting with the file system](http://yeoman.io/authoring/file-system.html)
- [storing user configs](http://yeoman.io/authoring/storage.html)
- [Unit Testing](http://yeoman.io/authoring/testing.html)
- [Debugging Generators](http://yeoman.io/authoring/debugging.html)
- [Integrating Yeoman in other tools](http://yeoman.io/authoring/integrating-yeoman.html)
- [Full API documentation](http://yeoman.io/generator/)

**Recursos**
- [Create A Custom Yeoman Generator in 4 Easy Steps](https://scotch.io/tutorials/create-a-custom-yeoman-generator-in-4-easy-steps)
- [A quick and dirty introduction to Yeoman generator development](https://benclinkinbeard.com/posts/a-quick-and-dirty-introduction-to-yeoman-generator-development/)
- [Building a Yeoman Generator](https://webcake.co/building-a-yeoman-generator/)
- [One Yeoman generator for all your frontend projects](http://fountainjs.io/doc)
- [Creating your own Custom Yeoman Generator](https://devdactic.com/creating-custom-yeoman-generator/)
- [Guide to create and publish a Yeoman generator](https://medium.com/@vallejos/yeoman-guide-adea4d6ea1e3)
- [Build Your Own Yeoman Generator](https://code.tutsplus.com/tutorials/build-your-own-yeoman-generator--cms-20040)




### Ejercicios

**1 -** Partiendo del repositorio [gulp-example-spa#template](https://github.com/josex2r/gulp-example-spa/tree/template) completar el fichero `gulpfile.js` para construir la **Single Page Application**:

```javascript
  // Tu solución
```