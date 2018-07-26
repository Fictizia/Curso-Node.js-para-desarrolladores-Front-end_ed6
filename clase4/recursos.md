# Clase 4

### HTTP
- [Objeto Request](https://nodejs.org/api/http.html#http_http_request_options_callback)
- [Objeto Response](https://nodejs.org/api/http.html#http_class_http_serverresponse)
- [Guide - Anatomy of an HTTP Transaction](https://nodejs.org/en/docs/guides/anatomy-of-an-http-transaction/)


### Events
- [The JavaScript Event Loop: Explained](http://blog.carbonfive.com/2013/10/27/the-javascript-event-loop-explained/)


### Process
- Captura de [señales en entronos UNIX](https://www.wikiwand.com/en/Unix_signal)
- **Librerías**
	- [node-upstarter](https://github.com/carlos8f/node-upstarter) 


### Cluster
- [Taking Advantage of Multi-Processor Environments in Node.js](http://blog.carbonfive.com/2014/02/28/taking-advantage-of-multi-processor-environments-in-node-js/#tldr)
- **Librerias:**
	- [luster](https://github.com/nodules/luster)
	- [cluster-map](https://www.npmjs.com/package/cluster-map)
	- [PM2](https://www.npmjs.com/package/pm2)


### Variables del Entorno
- **Alternativas**
	- [dotenv - librería para Nodejs](https://github.com/motdotla/dotenv)


### Modularización
- [CommonJS](https://www.wikiwand.com/en/CommonJS)


### NPM
- [Documentación](https://docs.npmjs.com/cli/docs)
- [Librerías útiles](https://github.com/sindresorhus/awesome-nodejs#command-line-utilities)


### Yarn

- [Web](https://yarnpkg.com/en/)
- [Empezar](https://yarnpkg.com/en/docs/getting-started)
- [Documentación](https://yarnpkg.com/en/docs)
- [Paquetes](https://yarnpkg.com/en/packages/)
- [Blog](https://yarnpkg.com/blog/)


### Dependency Hell:

- [nipster](http://nipstr.com/)
- [Nodei.co](https://nodei.co/)
- [Dependency Hell](http://www.wikiwand.com/en/Dependency_hell)
- **[David Dm](https://david-dm.org/)**
   - [Ejemplo Twitter-sentiments](https://david-dm.org/UlisesGascon/twitter-sentiments#info=dependencies&view=list)
   - [Ejemplo Grunt](https://david-dm.org/gruntjs/grunt#info=dependencies&view=table)
   - [Ejemplo Express](https://david-dm.org/strongloop/express)
   - [Ejemplo Bower](https://david-dm.org/bower/bower#info=dependencies&view=table)
- [ShieldsIO](http://shields.io/)
   - [Your Badge Service](http://badges.github.io/gh-badges/) 


### Seguridad:
- [Seguridad](https://nodesecurity.io/resources)
- [Seguridad Avisos](https://nodesecurity.io/advisories)
- [Recursos](https://nodesecurity.io/resources)


### package.json
- [Documentación](https://docs.npmjs.com/files/package.json)
- [Semantic Versioning](http://semver.org/lang/es/)


### NVM  (manejando varias versiones de Node)
- [paquete nvm](https://www.npmjs.com/package/nvm)


### Actualizando Node (método alternativo)
- [paquete n](https://www.npmjs.com/package/n)


### Express

**Migraciones**
- [De Express 3.x a Express 4.x](http://expressjs.com/es/guide/migrating-4.html)
  - [Documentación de la 3.x (desuso)](http://expressjs.com/es/3x/api.html)
  - [Cambios](http://expressjs.com/es/guide/migrating-4.html)
  - [Nuevas funcionaldiades](https://github.com/expressjs/express/wiki/New-features-in-4.x?_ga=1.226364894.554285759.1461232316)
- [De Express 4.x a Express 5.x (hoy es Alpha)](http://expressjs.com/es/guide/migrating-5.html)
  - [Cambios Previstos](https://github.com/expressjs/express/pull/2237?_ga=1.29731835.554285759.1461232316)

**Partes Claves**
- [express()](http://expressjs.com/es/4x/api.html#express)
- [Application](http://expressjs.com/es/4x/api.html#application)
- [Request](http://expressjs.com/es/4x/api.html#request)
- [Response](http://expressjs.com/es/4x/api.html#response)
- [Router](http://expressjs.com/es/4x/api.html#router)

- Manejadores: Métodos de respuesta
  - [res.download()](http://expressjs.com/es/4x/api.html#res.download)
  - [res.end()](http://expressjs.com/es/4x/api.html#res.end)
  - [res.json()](http://expressjs.com/es/4x/api.html#res.json)
  - [res.jsonp()](http://expressjs.com/es/4x/api.html#res.jsonp)
  - [res.redirect()](http://expressjs.com/es/4x/api.html#res.redirect)
  - [res.render()](http://expressjs.com/es/4x/api.html#res.render)
  - [res.send()](http://expressjs.com/es/4x/api.html#res.send)
  - [res.sendFile()](http://expressjs.com/es/4x/api.html#res.sendFile)
  - [res.sendStatus()](http://expressjs.com/es/4x/api.html#res.sendStatus)

- **Middleware incorporado**
  - [express.static](https://github.com/expressjs/serve-static)

- **Middleware oficial (No incorporado)**
  - [serve-favicon](https://github.com/expressjs/serve-favicon)
  - [Morgan](https://github.com/expressjs/morgan)
  - [body-parser](https://github.com/expressjs/body-parser)
  - [basic-auth-connect](https://github.com/expressjs/basic-auth-connect)
  - [csurf](https://github.com/expressjs/csurf)
  - [cors](https://github.com/expressjs/cors)
  - [compression](https://github.com/expressjs/compression)
  - [express-session](https://github.com/expressjs/session)
  - [multer](https://github.com/expressjs/multer)
  - [cookie-session](https://github.com/expressjs/cookie-session)
  - [cookie-parser](https://github.com/expressjs/cookie-parser)
  - [cookie-session](https://github.com/expressjs/cookie-session)
  - [serve-static](https://github.com/expressjs/serve-static)
  - [vhost](https://github.com/expressjs/vhost)
  - [restful-router](https://github.com/expressjs/restful-router)
  - [connect-markdown](https://github.com/expressjs/connect-markdown)

**Middleware: Más Middleware, más funcionalidad**
- [La lista de Raynos](https://github.com/Raynos/http-framework/wiki/Modules)

**[Ejemplos con Express](https://github.com/expressjs/express/tree/master/examples)**

- **Utilidades**
  - [PostMan](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)
  - [Expresiones regulares](https://regex101.com/)

### PUG (antes Jade)

- **Cambios**
  - [Jade... ya no se llama jade. Ahora se llama PUG](https://github.com/pugjs/pug/issues/2184)

- **[Comparativa de Motores de plantillas](https://strongloop.com/strongblog/compare-javascript-templates-jade-mustache-dust/)**

- **Implementaciones en otros lenguajes**
  - [php](https://github.com/kylekatarnls/jade-php)
  - [scala](https://scalate.github.io/scalate/documentation/scaml-reference.html)
  - [ruby](https://github.com/slim-template/slim)
  - [python](https://github.com/SyrusAkbary/pyjade)
  - [java](https://github.com/neuland/jade4j)

- **Documentacion**
  - [Jade en Github](https://github.com/jadejs/jade)
  - [Jade en CLI](http://jade-lang.com/command-line/)
  - [Jade API](http://jade-lang.com/api/)
  - [Jade Language Ref](http://jade-lang.com/reference/)

- **Utilidades**
 - [PostMan](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)
 - [Html2Jade](http://html2jade.org/)