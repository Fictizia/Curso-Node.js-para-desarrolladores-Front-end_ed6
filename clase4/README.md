# Clase 4

### HTTP

- **Hello World con HTTP:**

  ```javascript
  const http = require('http');

  const msg = 'Hola a todos, ahora usando HTTP\n';
  
  http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end(msg);
  }).listen(8080, 'localhost');
  ```

- **Rediccionamiento:**

  ```javascript
  const http = require('http');
  
  http.createServer((req, res) => {
    res.writeHead(301, {
      'Location': 'http://www.google.es/'
    });
    res.end();
  }).listen(8080, 'localhost');
  ```

- **Ping (petición http):**

  ```javascript
  const http = require('http');
  
  const url = 'https://google.es';
  
  http.get({ host: url }, (resOrigen) => {
    http.createServer((req, res) => {
      res.writeHead(200, {'Content-Type': 'text/plain'});
      res.end(`La respuesta de ${url} es ${resOrigen.statusCode}`);
    }).listen(8080, 'localhost');
  }).on('error', (e) => {
    http.createServer((req, res) => {
      res.writeHead(200, {'Content-Type': 'text/plain'});
      res.end(`La respuesta de ${url} es ${e.message}`);
    }).listen(8080, 'localhost');
    console.log('Tenemos un error!! -', e.message);
  });
  ```

- **[Objeto Request](https://nodejs.org/api/http.html#http_http_request_options_callback)**
- **[Objeto Response](https://nodejs.org/api/http.html#http_class_http_serverresponse)**
- **[Guide - Anatomy of an HTTP Transaction](https://nodejs.org/en/docs/guides/anatomy-of-an-http-transaction/)**
 

### URL

![url_parts](https://doepud.co.uk/images/blogs/complex_url.png)

- **Leyendo urls:**

  ```javascript
  const url = require('url');
  const demoURL = 'http://localhost:3000/ruta?parametro=dato#detalle';
  
  console.log('El host: ' + url.parse(demoURL).hostname);
  console.log('El puerto: ' + url.parse(demoURL).port);
  console.log('La ruta: ' + url.parse(demoURL).pathname);
  console.log('La parametro: ' + url.parse(demoURL).query);
  console.log('El hash(#): ' + url.parse(demoURL).hash);
  ```
  
  ```javascript
  const { URL } = require('url');
  
  const demoURL = new URL("http://localhost:3000/ruta?parametro=dato#detalle");
  
  console.log('Host: ' + demoURLhostname);
  console.log('Puerto: ' + demoURL.port);
  console.log('Ruta: ' + demoURL.pathname);
  console.log('Parámetros: ' + demoURL.query);
  console.log('Hash: ' + demoURL.hash);
  ```

- **Trabajando con rutas:**

  ```javascript
  const http = require('http');
  const url = require('url');
  
  http.createServer(function (req, res) {
    const pathname = url.parse(req.url).pathname;
  
    if (pathname === '/') {
      res.writeHead(200, {
        'Content-Type': 'text/plain'
      });
      res.end('Index!');
    } else if (pathname === '/otro') {
      res.writeHead(200, {
        'Content-Type': 'text/plain; charset=utf-8'
      });
      res.end('sencillamente otra página');
    } else if (pathname === '/alindex') {
      res.writeHead(301, {
        'Location': '/'
      });
      res.end();    
      
    } else {
      res.writeHead(404, {
        'Content-Type': 'text/plain'
      });
      res.end('Querido... 404!');
    }
  }).listen(8080, 'localhost');
  ```

- **Ping recurrente (consola):**

  ```javascript
  const http = require('http');
  const url = "google.es";
  const tiempo = 3500;
  
  setInterval(function() {
    http.get({ host: url }, function(res) {
      if (res.statusCode === 200 ) {  
        console.log(`Sin errores en ${url}`);
      } else {
        console.log(`Respuesta Http ${res.statusCode} en ${url}`);
      }    
    }).on('error', function(e) {
      console.log(`Con errores -> La respuesta de ${url} es ${e.message}`);
    });
  }, tiempo);
  ```



### Asincronía:

> El modelo de programación de Node.js es monohilo, asíncrono y dirigido por eventos. 
1. No puede haber código bloqueante o todo el servidor quedará bloqueado y esto incluye no responder a nuevas peticiones entrantes.
2. La asincronicidad implica que no sabemos cuándo ni en que orden se va a ejecutar el código, generalmente esto no es importante pero en ocasiones sí lo es y habrá que tenerlo en cuenta.
3. En caso de error inesperado debemos capturarlo y controlar el posible estado en que haya podido quedar la ejecución del código.
> Nicolas Nombela en [nnombela](http://nnombela.com/blog/2012/03/21/asincronicidad-en-node-dot-js/)

- **Síncrono - código bloqueante:**

  ```javascript
  const http = require('http');
  let numeroPeticion = 1
    
  function writeResponse(response) {
    response.writeHead(200, {'Content-Type': 'text/plain'});
    response.write('Hola Mundo!, numero de peticion ', numeroPeticion);
    response.end();
    console.log('Se termino... ', numeroPeticion);
  }
    
  function sleepSynch(seconds, response) {
    const startTime = new Date().getTime();
    while (new Date().getTime() < startTime + Math.floor((Math.random() * 1000) + 500) * seconds) {
      // Nada pasa....
    }
    writeResponse(response);
  }
    
  http.createServer(function(request, response) {
    console.log('Empezo...', numeroPeticion);
    sleepSynch(10, response);
    numeroPeticion++;
  }).listen(8080);
  ```

- **Asíncrono - timeOut()**

  ```javascript
  const http = require('http');

  function writeResponse(response) {
    response.writeHead(200, {'Content-Type': 'text/plain'});
    response.write('Hola Mundo!');
    response.end();
    console.log('Se termino... ');
  }
  
  function sleepAsynch(seconds, response) {
    setTimeout(function() {
      writeResponse(response);
    }, 3000);
  }
  
  http.createServer((request, response) => {
    console.log('Empezo... ');
    sleepAsynch(10, response);
  }).listen(8080);
  ```


### Mantener Node funcionando

- Se cierra:

  ```javascript
  setTimeout(function (){
    process.stdout.write("Cerrando Node...")
  }, 1000)
  ```

- Se mantiene:

  ```javascript
  setInterval(function (){
    // Nada pasa... pero sigo funcionando
  }, 1000)
  ```
  
- Programando una salida:

  ```javascript
  let contador = 0
  setInterval(() => {
    contador++
    if(contador > 10){
      process.exit()
    } else {
      console.log('Sigo. Valor contador -> ', contador);
    }
  }, 1000);
  ``` 


### File System

- **Leer un archivo**

  ```javascript
  const fs = require('fs');
  
  fs.readFile('archivo.txt', 'utf8', (err, data) => {
    if (!err) {
      console.log(data);
    } else {
      throw err;
    }
  });
  ```

- **Escribir un archivo**

  ```javascript
  const fs = require('fs');

  const data = "y esto... se guardará en 'test.txt'";

  fs.writeFile('test.txt', data, (err) => {
    if (!err) {
      console.log('Datos guardados en el \'test.txt\'');
    } else {
      throw err;
    }
  });
  ```

- **Usando Promesas y Callbacks**

  ```javascript
  const fs = require('fs');
  
  // Con CallBacks!
  fs.readFile('./README.md', (error, content) => {
  	console.log('Leyendo el archivo...');
  	fs.writeFile('./length.txt', content.length, (error) => {
	    if (error) {
	      console.log('error! ', error);
	    } else {
	      console.log('Terminado... hemos almacenado una cadena que vale ', content.length);
	    }
  	});
  });

  // Con Promesas!
  function leerArchivo (file) {
  	return new Promise((resolve, reject) => {
  		fs.readFile(file, (error, contenido) => {
  			console.log('Empezando la lectura de ', file);
  			if(error){
  				console.log('Error en la lectura');
  				return reject(error);
  			}
  			console.log('Lectura finalizada en ', file);
  			resolve(contenido);
  		});
  	});
  }

  function escribirArchivo(file, content){
  	return new Promise((resolve, reject) => {
  		fs.writeFile(file, content, (error) => {
  			if(error){
  				console.log('Error en la escritura de ', file);
  				return reject(error);
  			}
  			console.log('Escritura Termianda en ', file);
  			resolve();
  		});
  	});
  }

  //Opción1
  leerArchivo('./miArchivo.txt')
    .then((content) => {
        escribirArchivo('./longitud.txt', content);
    }, (error) => {
    	console.log('Promesas con errores: ');
    	console.log(error);
    });

  //Opción2
  Promise.all([
  	leerArchivo('./otros.txt'),
  	leerArchivo('./usuarios.txt'),
  	leerArchivo('./mas_cosas.txt')
	]).then((respuestas) => {
		console.log('Tenemos un total de '+respuestas.length+' respuesta/s.');
		console.log('El primero tiene '+respuestas[0].length+' caracteres');
		console.log('El segundo tiene '+respuestas[1].length+' caracteres');
		console.log('El tercero tiene '+respuestas[2].length+' caracteres');
	});

  //Opcion3
  Promise.race([
  	leerArchivo('./otros.txt'),
  	leerArchivo('./usuarios.txt'),
  	leerArchivo('./mas_cosas.txt')
	]).then((respuesta) => {
		console.log('El más rápido tiene solo '+respuesta.length+' caracteres.');
	});
  ```
  
- **Ejemplo utilizando la librería [Q](https://github.com/kriskowal/q)**

  ```javascript
  const fs = require('fs');
  const Q = require('q');
  const readFile = Q.denodeify(fs.readFile);
  
  // Con CallBacks!
  readFile('./README.md').then(content) => {
  	console.log('El contenido es:', content);
  }, (error) => {
    console.log('error! ', error);
  });
  ```


- **[Más métodos para:](https://nodejs.org/api/fs.html)**
	- Síncronos
	- Escucha de cambios
	- Manipulación de carpetas
	- Comprobación de ficheros/directorios
	- etc...

### Events

![events](https://www.safaribooksonline.com/library/view/nodejs-the-right/9781941222355/images/eventloop.png)
- Patrón Observador
- Similar al navegador

- **Suscribiendonos a eventos**
	- Sin eventos

	```javascript
	const http = require('http');
	
	const server = http.createServer((request, response) => {
		response.writeHead(200, {'Content-Type': 'text/plain'});
		response.end('¡Hola people!');
	}).listen(8080);
	```

	- Con eventos

	```javascript
	const http = require('http');
	
	const server = http.createServer().listen(8080);
	
	server.on('request', (request, response) => {
		response.writeHead(200, {'Content-Type': 'text/plain'});
		response.end('¡Hola people!');
	});
	```

- **Ejemplo sencillo: Creando nuestros eventos**

  ```javascript
  const events = require('events');
  const EventEmitter = events.EventEmitter;
  
  const ee = new EventEmitter(); 
  ee.on('current-date', (date) => { 
     console.log(date); 
  }); 
  setInterval(() => { 
     ee.emit('current-date', Date.now()); 
  }, 500);
  ```

- **Ejemplo: Juguemos al Ping-Pong**

  ```javascript
  const { EventEmitter } = require('events');
  const pingPong = new EventEmitter();
  
  let pingNumero = 1;
  
  console.log('Bienvenido al juego de Ping/Pong!');
  console.log('Empezamos en 5 segundos....');
  
  setTimeout(() => {
    console.log('Primer Ping... que desencadenará el juego');
    pingPong.emit('ping', pingNumero);
    pingNumero++;
  }, 5000);
  
  pingPong.on('ping', (numero) => {
    console.log('Llegó el Ping('+numero+'). Emitimos Pong');
    setTimeout(() => pingPong.emit('pong'), 1000);
  });
  
  pingPong.on('pong', () => {
    console.log('Llegó el Pong. Emitimos Ping');
    setTimeout(() => {
      pingPong.emit('ping', pingNumero);
      pingNumero++;
    }, 1000);
  });
  ```

### Repasar los conceptos clave

**Loop**

- [The JavaScript Event Loop: Explained](http://blog.carbonfive.com/2013/10/27/the-javascript-event-loop-explained/)

![](https://media.licdn.com/mpr/mpr/AAEAAQAAAAAAAAhTAAAAJGEzYjdjNTFlLTI1MjQtNGFjMS04YTZkLWM2ZmU0ODgzOTNjZA.png)

![loop](https://cdn-images-1.medium.com/max/1600/1*ROxiavz7LeRpIfcgRDE7CA.png)

**Arquitecura diferente**

![](https://cdn-images-1.medium.com/max/800/1*4LsfQ0ZbZkapHDR8eTYp4g.png)


**Single Thread**
![](https://strongloop.com/wp-content/uploads/2014/01/threading_java.png)


**Multi Thread**
![](https://strongloop.com/wp-content/uploads/2014/05/threading_node.png)


### Process

- **[Códigos de salida en Node.js](https://nodejs.org/dist/latest-v4.x/docs/api/process.html#process_exit_codes)**
  - 1 - *Uncaught Fatal Exception - No ha podido ser capturada*
  - 2 - **Unused (reserved by Bash for builtin misuse)**
  - 3 - *Internal JavaScript Parse Error *
  - 4 - *Internal JavaScript Evaluation Failure *
  - 5 - *Fatal Error - There was a fatal unrecoverable error in V8.*
  - 6 - *Non-function Internal Exception Handler*
  - 7 - *Internal Exception Handler Run-Time Failure*
  - 8 - **Unused**
  - 9 - *Invalid Argument*
  - 10 - *Internal JavaScript Run-Time Failure *
  - 12 - *Invalid Debug Argument*
  - 128 - *Signal Exits - El sistema operativo acaba con Node.*


- **process.argv:**

  ```javascript
  console.log(process.argv)
  /*
  1. ubicacion de node (bin)
  2. ubicación del script (location)
  3. [Otros parametros]
  */
  ```

- **Detalles del sistema**

  ```javascript
  process.argv[2] = process.argv[2] || "Node.js funcionando desde C9.io";

  console.log("===================================");
  console.log("Id: " + process.pid);
  console.log("Título: " + process.title);
  console.log("Ruta: " + process.execPath);
  console.log("Directorio Actual: " + process.cwd());
  console.log("Node Versión: " + process.version);
  console.log("Plataforma: " + process.platform);
  console.log("Arquitectura: " + process.arch);
  console.log("Tiempo activo: " + process.uptime());
  console.log("Versiones Dependencias: ");
  process.argv.forEach((val, index, array) => {
        console.log(`${index}: ${val}`);
  });
  console.log("===================================");
  ```

- Librerías para controlar los parámetros de un script:
  - [commander](https://www.npmjs.com/package/commander)
  - [meow](https://github.com/sindresorhus/meow)
  - [minimist](https://github.com/substack/minimist)
  - [Inquirer (input vía cli)](https://github.com/SBoudrias/Inquirer.js)

- **console.log("Hola"):**

  ```javascript
  const mensaje = "Hola"
  process.stdout.write(mensaje + '\n')
  ```

- **Captura de errores inesperados**

  ```javascript
  process.on('uncaughtException', (err) => {
    console.error(error.stack);
  });
  ```

- **Ejecucción de tareas antes de la finalización del proceso**

  ```javascript
  process.on('exit', function (err) {
    // Limpiar cache.. y cosas similares...
  });
  ```

- **Captura de [señales en entronos UNIX](https://www.wikiwand.com/en/Unix_signal)**

  ```javascript
  // SIGINT -> Control-C
  process.stdin.resume(); // Evitamos que se cierre Node.js
  
  process.on('SIGINT', function() {
    console.log('Llegó SIGINT. Control-C... Saliendo...');
    process.exit(0);
  });
  ```

### Creando ejecutables

- Solo para entornos UNIX

- Necesitamos *shebang*
  
  > Shebang es, en la jerga de Unix, el nombre que recibe el par de caracteres #! que se encuentran al inicio de los programas ejecutables interpretados.

  ```javascript
  #!/usr/bin/env node
  console.log('Soy un script!');
  ```

- Necesitamos hacer el script ejecutable

  ```
  chmod +x mi_escript_archivo.js
  ```

- Ejecutando el script

  ```
  ./mi_escript_archivo.js <parámetro>
  ```

- **Ejemplo: Hello world!**

  ```javascript
  #!/usr/bin/env node
  console.log('Hello World!');
  process.exit(1); // Por defecto la salida es '1'
  ```

**Arrancar Scripts al incio del sistema**
- Librerías:
  - [node-upstarter](https://github.com/carlos8f/node-upstarter) 


###  Child Process
- Ideal para tareas pesadas, inestables o muy lentas
- Nos permite usar comandos del sistema.
- Podemos lanzar aplicaciones basadas en otros lenguajes o sistemas.

- **Creando hijos y usando spawn**
-  *spawn* devuelve un *stream*

  ```javascript
  const spawn = require('child_process').spawn;
  const ping = spawn('ping', ['fictizia.com']);
  
  ping.stdout.setEncoding('utf8');
  ping.stdout.on('data', console.log);
  ```

- **Creando hijos y usando exec**
-  *exec* retorna un *buffer*

  ```javascript
  const { exec } = require('child_process');

  // cat solo funciona en UNIX
  exec('cat README.md', (err, stdout, stderr) => {
    if(!err){  
      console.log('El contenido de nuestro archivo', stdout)
    } else {
      console.log('Error: '+err)
    }
  });
  ```

- **Manejando hijos:**

  ```javascript
  const { spawn } = require('child_process');

  if(process.argv[2] === 'hijo'){
    console.log('Estoy dentro del proceso hijo');
  } else {
    const hijo = spawn(process.execPath, [__filename, 'hijo'])
    hijo.stdout.pipe(process.stdout)
  }
  ```

- **Manejando hijos (con herencia):**

  ```javascript
  const spawn = require('child_process').spawn

  if(process.argv[2] === 'hijo'){
    console.log('Estoy dentro del proceso hijo');
  } else {
    const hijo = spawn(process.execPath, [__filename, 'hijo'], {
      stdio: 'inherit'
    })
  }
  ```

- **Manejando hijos (contexto común):**

  ```javascript
  const spawn = require('child_process').spawn;

  let contador = 1;
  contador += 1;

  if(process.argv[2] === 'hijo'){
    console.log('hijo', contador);
    contador++;
    console.log('pero.. además el hijo.. suma otra! y son', contador);
  } else {
    const hijo = spawn(process.execPath, [__filename, 'hijo'], {
      stdio: 'inherit'
    });
    console.log('padre', contador);
  }
  ```

### Cluster

> A single instance of Node.js runs in a single thread. To take advantage of multi-core systems, the user will sometimes want to launch a cluster of Node.js processes to handle the load.

- **Sin usar Cluster**

  ```javascript
  const http = require('http');
  const url = require('url');

  const server = http.createServer().listen(8080);

  server.on('request', (req, res) => {
      const pathname = url.parse(req.url).pathname;
      if (pathname === '/kill') {
          res.writeHead(200, {
              'Content-Type': 'text/plain'
          });
          res.end('Has matado el monohilo. PID: ' + process.pid);
          process.exit(0);
      } else {
          res.writeHead(200, {
              'Content-Type': 'text/plain'
          });
          res.end('Hola desde el monohilo. PID: ' + process.pid);
      }
  });
  ```

- **Usando Cluster.**
  - El proceso hijo que cae se vuelve a levantar.
  - El proceso padre se mantiene "separado"

  ```javascript
  const cluster = require('cluster');
  const http = require('http');
  const url = require('url');
  const cpus = require('os').cpus().length; // nproc
  
  if (cluster.isMaster) {
    console.log('Proceso maestro con PID:', process.pid);

    for (let i = 0; i < cpus; i++) {
      cluster.fork();
    }

    cluster.on('exit', (worker) => {
      console.log('hijo con PID ' + worker.process.pid + ' muerto');
      cluster.fork();
    });
  
  } else {
    console.log('Arrancado hijo con PID:', process.pid);

    const server = http.createServer().listen(process.env.PORT);

    server.on('request', (req, res) => {
      const pathname = url.parse(req.url).pathname;
      if (pathname === '/kill') {
        res.writeHead(200, {
            'Content-Type': 'text/plain'
        });
        res.end('Has matado al proceso hijo ' + process.pid);
        process.exit(0);
      } else {
        res.writeHead(200, {
            'Content-Type': 'text/plain'
        });
        res.end('Hola desde ' + process.pid);
      }
    });
  }
  ```

- [Taking Advantage of Multi-Processor Environments in Node.js](http://blog.carbonfive.com/2014/02/28/taking-advantage-of-multi-processor-environments-in-node-js/#tldr)

- **Librerias:**
  - [luster](https://github.com/nodules/luster)
  - [cluster-map](https://www.npmjs.com/package/cluster-map)
  - [PM2](https://www.npmjs.com/package/pm2)

### Buffer

- Nos ofrece la posibilidad de alamacenar datos sin procesar
- Una vez iniciados no puede modificarse el tamaño
- Tamaño máximo 1GB

```javascript
const buf1 = new Buffer(10); // buf1.length = 10
const buf2 = new Buffer([1,2,3]); // [01, 02, 03]
const buf3 = new Buffer('prueba'); // ASCII [74, 65, 73, 74]
const buf4 = new Buffer('ñam ñam', 'utf8'); // UTF8 [74, c3, a9, 73, 74]
  
console.log("===================================");
console.log("buf1: " + buf1.length);
console.log("buf2: " + buf2[0]);
console.log("buf3: " + buf3);
console.log("buf3 (hex): " + buf3.toString('hex'));
console.log("buf3 (base64): " + buf3.toString('base64'));
console.log("buf4: " + buf4);
console.log("buf4 (hex): " + buf4.toString('hex'));
console.log("buf4 (base64): " + buf4.toString('base64'));
console.log("===================================");
```


### Stream

- Gestionamos el *flujo de datos*
- Muy usados por librerías y modulos (ej. `gulp`)
- Capa de abstracción para operaciones con datos
- Lógica de tuberias (cadena de procesos)
- Gestiona el *buffer* por si mismo
- Tipos:
  - Readable *Lectura*
    - Eventos (data, error, end)
  - Writable *Escritura*
    - Eventos (drain, error, finish)
  - Duplex *Ambos*
  - Transform *Transformación de datos*
- **Función .pipe()**
  - Simple: 
  `origen.pipe(destino);`
  - Concatenando:
  `origen.pipe(destino).pipe(otroDestino);`

- **Ejemplo: Stream multimedia**

  ```javascript
  const http = require('http');
  const fs = require('fs');
  
  http.createServer((req, res) => {
    const song = 'song.mp3';
    const stat = fs.statSync(song);
  
    res.writeHead(200, {
      'Content-Type': 'audio/mpeg',
      'Content-Length': stat.size
    });
  
    const readableStream = fs.createReadStream(song);
    readableStream.pipe(res);
  }).listen(8080);
  ```

- **Stream y ficheros**

  ```javascript
  const fs = require('fs');
  
  const lectura = fs.createReadStream('README.md');
  const escritura = fs.createWriteStream('COPY.md');
  
  lectura.pipe(escritura);
  ```


### Variables del Entorno

- Conocer todas las variables disponibles en el entorno
  - Windows: 

  ```
  SET
  ```

  - UNIX: 

  ```
  env
  ```

- Guardar nuevas variables en el entorno
  - Windows: 

  ```
  SET ALGO='mi secreto'
  ```

  - UNIX: 

  ```
  export ALGO='mi secreto'
  ```
  
- Recuperar las variables con Node.js

  ```javascript
  const datoRecuperado = process.env.ALGO;
  console.log(process.env.ALGO);
  ```

- Creando variables del entorno limitadas a Node.js y temporales (SOLO UNIX)
  - Arrancando...   

  ```
  NODE_ENV=production node app.js
  ```

  - Usando datos...

  ```javascript
  if(process.env.NODE_ENV === "production"){
    console.log("Entramos en modo producción");
  } else if (process.env.NODE_ENV === "development"){
    console.log("Entramos en modo desarrollo");
  } else {
    console.log("Entramos en modo desconocido. ¡Revisa las variables del entorno!");
  }
  ```  
  
- **Alternativas**
  - [dotenv - librería para Nodejs](https://github.com/motdotla/dotenv)

### Modularización

- Especificación de [CommonJS](https://www.wikiwand.com/en/CommonJS)
- Exports es un objeto que vamos "rellenando"
- La asignacion al exports es inmediata. No se pueden usar callbacks o similares
- No es necesario usar *module.exports* ya es que es global.
  - `const exports = module.exports = {};`
- Es importante controlar la reasignación de *module.exports*

### Modularización: Usando exports

- **Exportar los datos:**

  ```javascript
  // archivo -> config.js
  
  const datoPrivado = "Lo que pasa en Node... se queda en Node";
  const datoCompartido = "Hola! desde Config.js"
  
  function privada (){
    return datoPrivado;
  }
  
  exports.metodo = function () {
    console.log(datoCompartido);
    console.log(privada());
  }
  exports.mensaje = datoCompartido;
  ```

- **Importar los datos:**

  ```javascript
  const config = require('./config');
  
  config.metodo();
  console.log(config.mensaje);
  ```

### Modularización: Usando module.exports

- **Exportar los datos:**

  ```javascript
  // archivo -> config.js
  const config = {
    token: "<--- MiSecreto--->",
  };
  
  module.exports = config;
  ```

- **Importar los datos:**

  ```javascript
  const config = require('./config');
  
  console.log(config.token);
  ```

### NPM

![npm_logo](https://docs.npmjs.com/images/npm.svg)

**[Librerías interesantes de node](https://github.com/sindresorhus/awesome-nodejs#command-line-utilities)**

- ** Comprobar versión**

  ```
  npm -v
  ```

- **Instalar paquetes:**
  - global:

    ```
    npm install -g <paquete>
    ```  

  - local:

    ```
    npm install <paquete>
    ```    

- **Buscar paquetes**

  ```
  npm search <paquete>
  ```

- **Información de los paquetes**

  ```
  npm view <paquete>
  ```

- **Lista de paquetes instalados**

  ```
  npm ls
  ```

- **Lista de paquetes instalados globalmente**

  ```
  npm ls -g
  ```

- **Instalando versiones especificas:**

  - la más reciente:

    ```  
    npm install <paquete>@latest
    ```  
  
  - versión especifica:

    ```  
    npm install <paquete>@1.x (1.xx.xx)
    ```
  
  - Otra versión especifica

    ```
    npm install <paquete>@2.10.x (2.10.x)
    ```

- **Paquetes desactualziados:**

  ```
  npm outdated
  ```
  
- **Actualizando paquetes:**

  ```
  npm update <paquete>
  ```

- **Desinstalando paquete:**

  ```
  npm uninstall <paquete>
  ```

- **Información sobre Bugs**

  ```
  npm bugs <paquete>
  ```

- **[Más comandos - CLI](https://docs.npmjs.com/cli/install)**

### Dependency Hell:

**Abyssus abyssum invocat. El abismo llama al abismo.**

- [nipster](http://nipstr.com/)
- [Nodei.co](https://nodei.co/)
- [Dependency Hell](http://www.wikiwand.com/en/Dependency_hell)
- [David Dm](https://david-dm.org/)
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
- [snyk](https://snyk.io/test)

### package.json

- Datos proyecto
- Tareas
- Dependencias (dependencies y devDependencies)
- **[Documentación](https://docs.npmjs.com/files/package.json)**

- **Creación:**

  ```
  npm init
  ```
  
- **Guardar nuevas dependencias:**

  ```
  npm install <paquete> --save
  ```

- **Guardar nuevas dependencias (solo para entorno desarrollo):**

  ```
  npm install <paquete> --save -dev
  ```

- **Guardando versiones especificas:**
  - (1.xx.xx):

    ```
    npm install --save <paquete>@1.x
    ```
  
  - (2.10.x)

    ```
    npm install --save <paquete>@2.10.x
    ```
  
  - Latest

    ```
    npm install --save <paquete>@lastest
    ```
  
- **Quitando dependencias:**

  ```
  npm uninstall <paquete> --save
  ```
  
- **Instalamos las dependencias en el proyecto:**
  - todo:

    ```
    npm install (todo)
    ```
  
  - Solo production:

    ```
    npm install --production (solo producción)
    ```
  
  - Solo development:

    ```
    npm install --dev
    ```

- **[Semantic Versioning](http://semver.org/lang/es/)**
  - Estructura -> X.Y.Z-Extra 
  - Cambio Mayor - *No retrocompatible*
  - Cambio Menor - *Retrocompatible - Nuevas funcionaldiades o cambios*
  - Parche - *Retrocompatible - Solución de errores*
  - Extras - Indicativos o versiones especiales (Beta, Alfa, x86, etc...)

### npm scripts (comandos de CLI)

- **Añadiendo comandos:**

  ```javascript
  // ...
  "scripts": {
      "test": "npm -v",
      "start": "node -v",
      "hola": "echo 'Hola mundo!'"
  }
  // ...
  ```

- **Mostrando todos los comandos:**
  
  ```
  npm run
  ```

- **Ejecutando comandos:**
  - test

    ```
    npm test
    ```

  - start

    ```
    npm start
    ```

  - hola

    ```
    npm run hola
    ```  

### YARN

![yarn_logo](https://yarnpkg.com/assets/og_image.png)

- [Web](https://yarnpkg.com/en/)
- [Empezar](https://yarnpkg.com/en/docs/getting-started)
- [Documentación](https://yarnpkg.com/en/docs)
- [Paquetes](https://yarnpkg.com/en/packages/)
- [Blog](https://yarnpkg.com/blog/)


### NVM  (manejando varias versiones de Node)

- **Comrpobando la version de NVM:**

  ```
  nvm --version
  ```

- **Instalando una version:**

  ```
  nvm install 0.12
  ```

- **Desinstalando una version:**

  ```
  nvm uninstall 0.12
  ```

- **Usar una version (globalmente):**

  ```
  nvm use 0.12
  ```
  
- **Usando versiones (por proyecto):**

  ```
  echo 0.12 > .nvmrc
  ```
  
  ```
  nvm use
  ```


### Actualizando Node (método alternativo)
- Sin soporte a Windows
- Instalando el [paquete n](https://www.npmjs.com/package/n)

  ```
  npm install -g n
  ```

- **Opciones**

  ```
  n                              Output versions installed
  n latest                       Install or activate the latest node release
  n -a x86 latest                As above but force 32 bit architecture
  n stable                       Install or activate the latest stable node release
  n lts                          Install or activate the latest LTS node release
  n <version>                    Install node <version>
  n use <version> [args ...]     Execute node <version> with [args ...]
  n bin <version>                Output bin path for <version>
  n rm <version ...>             Remove the given version(s)
  n --latest                     Output the latest node version available
  n --stable                     Output the latest stable node version available
  n --lts                        Output the latest LTS node version available
  n ls                           Output the versions of node available
  ```


### Ejercicios

**1 -** Crea las rutas básicas para tener una página web clásica:
  - Debe responder con contenido HTML
  - `/`: Mostrará un título (`h1`) con el texto `Bienvenido`
  - `/contact`: Aparecerá un listado (`ul`) con algunos datos personales (nombre, apellidos, email, ...)
  - `/about`: Se mostrará un pequeño texto introductorio
  - `/bug`: Modificará todos los mensajes anteriores por la [siguiente imagen](https://www.iconexperience.com/_img/v_collection_png/256x256/shadow/bug_yellow_error.png)
  - En el caso de que la ruta no exista se redigirá al index (`/`)

**Solución:**

```javascript
// Tu solución
```

**2 -** Crear un servidor web que al acceder te muestre el contenido del fichero que aparece en la url:
  - Dada la siguiente url: `http://localhost/README.md`
  - Hay que extraer el nombre del fichero con la librería `URL` (`README.md`)
  - Leer el fichero con el `FileSystem` (`fs`):
    - Si el fichero no existe, devolver un error 404
    - Si el fichero existe, devolver el contenido del mismo

**Solución:**

```javascript
// Tu solución
```

**3 -** Crear un servidor web con las siguientes características:
  - Al recibir una petición **GET** mostrará el texto `Hola Mundo!`
  - Si en la petición anterior llega el parámetro `search` buscará una película con ese valor utilizando [omdbAPI](http://www.omdbapi.com)
    - Puedes utilizar la api key `e9b5e65a`
    - Ejemplo: `localhost?search=Avengers`
  - Si hay resultados se mostrará el listado de películas
  - Si no hay resultados se devolverá un 404

**Solución:**

```javascript
// Tu solución
```

**4 -** Realiza un script ejecutable que nos muestre la información de los terremotos acontecidos en la última hora.
- [Fuente de datos](http://earthquake.usgs.gov/earthquakes/feed/v1.0/geojson.php)
- Requisitos:
  - Debemos utilizar párametros cuando se ejecute para definir la magnitud de los terremotos que queremos
  - Si no se detecta el parámetro... la aplicación debe cerrarse.
  - Si el parametro es incorrecto también.
  - Ajustaremos la petición http en función del parámetro. 
- Apariencia(Orientativa):

  ```
  *****************************
  USGS All Earthquakes, Past Hour
     ---------------------     
  total: 8
  status: 200
     ---------------------     
  5/10/2016, 3:46:30 PM
  ==============================
  M 1.3 - 6km WNW of Anza, California
  5/10/2016, 3:43:01 PM
  Magnitud: 1.32
  Estatus: automatic
  Tipo: earthquake
  Lugar: 6km WNW of Anza, California
  Coordenadas: -116.7246704 , 33.5830002
  Info: http://earthquake.usgs.gov/earthquakes/eventpage/ci37563240
  Detalles: http://earthquake.usgs.gov/earthquakes/feed/v1.0/detail/ci37563240.geojson
  ==============================
  ... (por cada terremoto de los iguales a los iguales)
  ```

**Solución:**

```javascript
// Tu solución
```

**5 -** Crearemos varios scripts para automatizar tareas utilizando `npm`:
- `npm run versions`: Tiene que mostrar las versiones de `nodejs` y `npm`
- `npm run status`: Verificador del status de Git
- `npm run curso`: Clona nuestro curso de Github
- `npm run emoji`: Muestra un emoji al azar utilizando [emoji-random](https://www.npmjs.com/package/emoji-random)
- `npm run emoji`: Muestra **la url** de un **gif** por consola [make-me-lol](https://www.npmjs.com/package/make-me-lol)

```javascript
// Tu solución
```



### Express

![Express_logo](https://i.cloudup.com/zfY6lL7eFa-3000x3000.png)

**Influencias / usos**
- Otros frameworks similares:
  - Zend (PHP)
  - Django (Python)
  - Sinatra (Ruby)

- Uso:
  - API JSON
  - Single Page Applications
  - App tiempo real

**Pros**
- Rutas
- Parámetros
- Formularios y subida de ficheros
- Cookies
- Sesiones
- Templates
- Middlewares

**Contras**
- Base de datos / ORM
- Autenticación de usuarios
- Seguridad
- Migraciones
- Deployment
- Organización del código

**Migraciones**
- [De Express 3.x a Express 4.x](http://expressjs.com/es/guide/migrating-4.html)
  - [Documentación de la 3.x (desuso)](http://expressjs.com/es/3x/api.html)
  - [Cambios](http://expressjs.com/es/guide/migrating-4.html)
  - [Nuevas funcionaldiades](https://github.com/expressjs/express/wiki/New-features-in-4.x?_ga=1.226364894.554285759.1461232316)
- [De Express 4.x a Express 5.x (hoy es Alpha)](http://expressjs.com/es/guide/migrating-5.html)
  - [Cambios Previstos](https://github.com/expressjs/express/pull/2237?_ga=1.29731835.554285759.1461232316)


**Instalación**

- Instalación local:

  ```
  npm install express
  ```

- Instalación global:

  ```
  npm install -g express
  ```

- Instalación versiones anteriores:

  ```
  npm install -g express@3.x
  ```

**Hello World!**

  ```javascript
  const express= require('express');
  const app = express();
  
  app.get('/', (req, res) => res.send('Hello World!'));
  
  app.listen(8080, () => console.log('Example app listening on port 8080'));
```

**Generador de Express**

- Instalación global del generador

  ```
  npm install express-generator -g
  ```

- Opciones de instalación

  ```
  express -h
  ```

- Generar un proyecto (genera un directorio)

  ```
  express <nombre_proyecto>
  ```

- Entramos en la carpeta e instalamos las dependencias

  ```
  cd <nombre_proyecto> && npm install
  ```

- Estructura de un Proyecto (MVC)

  ```
  ├── app.js (Nuestra aplicación - módulo)
  ├── bin (Gestión de la aplicación)
  │   └── www
  ├── package.json (Información y dependencias)
  ├── public (Nuestros estáticos)
  │   ├── images
  │   ├── javascripts
  │   └── stylesheets
  │       └── style.css
  ├── routes (Nuestros controladores)
  │   ├── index.js
  │   └── users.js
  └── views (Nuestras vistas/plantillas)
      ├── error.jade
      ├── index.jade
      └── layout.jade
  ```

- Ejecutando la aplicación:
  - Windows

    ```
      set DEBUG=<nombre_proyecto>:* & npm start
    ```

  - MacOS/Linux

    ```
      DEBUG=<nombre_proyecto>:* npm start
    ```

- Opcional: [Volviendo el arranque al estilo Express 3.x](http://expressjs.com/es/guide/migrating-4.html#app-gen)

**Partes Claves**
- [express()](http://expressjs.com/es/4x/api.html#express)
- [Application](http://expressjs.com/es/4x/api.html#application)
- [Request](http://expressjs.com/es/4x/api.html#request)
- [Response](http://expressjs.com/es/4x/api.html#response)
- [Router](http://expressjs.com/es/4x/api.html#router)


**Mecánica: app.set()**
- Nos permite establecer la configuración de Express
- Podemos almacenar datos personalizados de manera global
- Ejemplos
  - Guardando la versión

  ```javascript
  app.set('version', '1.5.0');
  app.get('version'); // 1.5.0
  ```

  - Maneras de Habilitar contenido

  ```javascript
  app.enable('dia_soleado'); // igual a -> app.set('dia_soleado', true);
  app.enabled('dia_soleado'); // igual a -> app.get('dia_soleado') === true;
  app.disabled('dia_soleado'); // igual a -> app.get('dia_soleado') === false;
  ```  

  - Definiendo el puerto

  ```javascript
    app.set('port', process.env.PORT || 3000);
  ```

  - Configuraciones según el entorno
    - Para todos los entornos 

      ```
      NODE_ENV=production node app.js
      ```
  
      ```javascript
      app.set('estado_aplicacion', '*');
      ```

    - Solo desarrollo

      ```
      NODE_ENV=development node app.js
      ```

      ```javascript
      if (NODE_ENV === 'develop')
        app.set('estado_aplicacion', 'development');
      }
      ```

    - Solo producción

      ```
      NODE_ENV=production node app.js
      ```
  
      ```javascript
      if (NODE_ENV === 'production')
        app.set('estado_aplicacion', '*');
      }
      ```

    - Solo personalizado

      ```
      NODE_ENV=personalizado1 node app.js
      ```

      ```javascript
      if (NODE_ENV === 'personalizado1')
        app.set('estado_aplicacion', '*');
      }
      ```

  - Motores de Plantillas
    - Variables locales (solo disponibles para las plantillas)

      ```javascript
      // Guardando
      app.locals.title = 'My App';
      app.locals.email = 'me@myapp.com';
      
      // Usando
      app.locals.title // My App
      app.locals.email // me@myapp.com
      ```

    - Definiendo el sistema de plantillas que usaremos

      ```javascript
      // npm install pug --save
      const express = require('express');
      const app = express();
      
      app.set('view engine', 'pug');
      
      app.get('/', (req, res) => {
          res.render('index', { title: 'Hey', message: 'Hello there!'});
      });
      
      app.listen(8080);
      ```

- [Comparativa de Motores de plantillas](https://developer.ibm.com/node/2014/11/11/compare-javascript-templates-jade-mustache-dust/)


**Mecánica: app.all(), app.get(), app.post(), app.put(), app.delete(), app.route()**

```javascript
app.METODO(Ruta, Manejador)
```

- Estructura
  - app *Instanciado de express*
  - METODO *[Metodo HTTP](https://www.wikiwand.com/es/Hypertext_Transfer_Protocol) de la Ruta*
    - Soportados: get, post, put, head, delete, options, trace, copy, lock, mkcol, move, purge, propfind, proppatch, unlock, report, mkactivity, checkout, merge, m-search, notify, subscribe, unsubscribe, patch, search y connect.
    - Para todas las rutas usamos *app.all()*
  - Ruta *Ruta (url) donde se aplica*
    - Podemos usar
      - Series
      - Patrones de Series (Subtipo de Regex)
        - Reducido a los subconjuntos ?, +, *, y ()
      - [Expresiones regulares](https://regex101.com/)
  - Manejador *La función que será llamada cuando se alcance la ruta con el método/s correctos/s*
    - Se puede usar funciones individuales
    - Se pueden hacer matrices de funciones
    - Se pueden mezclar matrices y funciones individuales
    - Argumentos:
      - Obj Request de Node.js
      - Obj Response de Node.js
      - next() *Función que dispara el siguiente middleware*

- Métodos HTTP: delimitando a un único método

  ```javascript
  app.get('/', (req, res, next) => {
    res.send('Solo get como método me vale...');
  });
  ```

- Métodos HTTP: Otra forma de delimitar a un método 

  ```javascript
  app['m-search']('/', (req, res, next) => {
    res.send('Solo m-search como método me vale...');
  });
  ```

- Métodos HTTP: permitiendo todos los métodos

  ```javascript
  app.all('/', (req, res, next) => {
    res.send('Cualquier método me vale...');
  });
  ```

- Rutas: Raiz `http://localhost:8080/`

  ```javascript
  app.get('/', (req, res, next) => {
    res.send('Esto es la Raiz');
  });
  ```
- Rutas: Básicas http://localhost:8080/hola

  ```javascript
  app.get('/hola', (req, res, next) => {
    res.send('Esto es /hola');
  });
  ```

- Rutas: Capturando Parámetros `http://localhost:8080/hola/Eduardo`, `http://localhost:8080/hola/Oscar`, ...

  ```javascript
  app.get('/hello/:nombre', (req, res) => {
      res.send('Hola ' + req.nombre + '!');
  });
  ```
- Rutas: Capturando varios parámetros `http://localhost:8080/desde/Madrid/a/Malga`, `http://localhost:8080/desde/Madrid/a/NYC`

  ```javascript
    app.get('/desde/:origen/a/:destino', (req, res, next) => {
      res.send('Quieres ir de ' + req.params.origen + ' a ' + req.params.destino);
    });
  ```
- Rutas: Capturando varios parámetros y alguno determiando `http://localhost:8080/mensaje/1/editar`, `http://localhost:8080/mensaje/500/borrar`, ...

  ```javascript
    app.get('/mensaje/:id/:accion(editar|borrar)', (req,res,next) => {
      res.send('Quieres ' + req.params.accion + ' el mensaje numero ' + req.params.id);
    });
  ```

- Rutas: Parámetros opcionales `http://localhost:8080/user/1/editar`, `http://localhost:8080/user/500/borrar`, ...

  ```javascript
  app.get('/user/:id/:comando?', (req, res, next) => {
    if(req.params.comando){
      res.send("Tenemos algo! Quieres " + req.params.comando);
    } else {
      res.send("Nada de nada...");
    }
  });
  ```
  
- Rutas: Más parámetros opcionales http://localhost:8080/user/1.pdf, http://localhost:8080/user/500.zip, etc...

  ```javascript
  app.get('/user/:id.:formato?', (req, res, next) => {
    if(req.params.formato){
      res.send("["+req.params.formato+"] Extensión requerida... ");
    } else {
      res.send("Sin Extensión requerida");
    }
  });
  ```

- Rutas: Tipo fichero `http://localhost:8080/hola.text`

  ```javascript
  app.get('/hola.text', (req, res) => {
    res.send('Hola');
  });
  ```

- Rutas: Patrones de serie (?) *http://localhost:8080/acd o http://localhost:8080/abcd*

  ```javascript
  app.get('/ab?cd', (req, res) => {
    res.send('ab?cd');
  });
  ```

- Rutas: Patrones de serie (+) *http://localhost:8080/abcd, http://localhost:8080/abbbbbcd, etc...*

  ```javascript
  app.get('/ab+cd', (req, res) => {
    res.send('ab+cd');
  });
  ```

- Rutas: Patrones de serie (*) *http://localhost:8080/abcd, http://localhost:8080/abAALGOOOcd, etc...*

  ```javascript
  app.get('/ab*cd', (req, res) => {
    res.send('ab*cd');
  });
  ```

- Rutas: Patrones de serie (()) *http://localhost:8080/abe o http://localhost:8080/abcd*
  
  ```javascript
  app.get('/a(bc)d', (req, res) => {
    res.send('a(bc)d');
  });
  ```

- Rutas: Expresiones regulares *http://localhost:8080/mcfly, http://localhost:8080/dragonfly, etc...*

  ```javascript
  app.get(/.*fly$/, (req, res) => {
    res.send('/.*fly$/');
  });
  ```

- Rutas: Molularidad con app.route()

  ```javascript
  app.route('/pelicula')
    .get((req, res) => {
      res.send('todas las peliculas...');
    })
    .post((req, res) => {
      res.send('Añadir una pelicula...');
    })
  ```

- Manejadores: Función individual

  ```javascript
  app.get('/example/a', (req, res) => {
    res.send('Hola desde A!');
  });
  ```

- Manejadores: Dos funciones individuales

  ```javascript
  app.get('/example/b', (req, res) => {
    console.log('La respuesta se enviará a la siguiente función...');
    next();
  }, (req, res) => {
    res.send('Hola desde B!');
  });
  ```

- Manejadores: Matrices

  ```javascript
  const cb0 = (req, res, next) => {
    console.log('CB0');
    next();
  };
  
  const cb1 = (req, res, next) => {
    console.log('CB1');
    next();
  };
  
  const cb2 = (req, res) => {
    res.send('Hola desde C!');
  };
  
  app.get('/example/c', [cb0, cb1, cb2]);
  ```

- Manejadores: Matrices y funciones individuales

  ```javascript
  const cb0 = (req, res, next) => {
    console.log('CB0');
    next();
  };
  
  const cb1 = (req, res, next) => {
    console.log('CB1');
    next();
  };
  
  app.get('/example/d', [cb0, cb1], (req, res, next) => {
    console.log('La respuesta se enviará a la siguiente función...');
    next();
  }, (req, res) => {
    res.send('Hola desde D!');
  });
  ```

- Manejadores: Objeto petición
  - `req.ip` *Almacena la IP desde donde se realizó la peticioón*
  - `req.is` *Que tipo de datos nos llegan desde la petición. Booleano*

    ```javascript
    req.is('json');
    req.is('application/*');
    req.is('application/json');
    ```
  - `req.params` *Contenido de la ruta (http://localhost:8080/usuarios/:id)*
  - `req.query` *Contenido de la consulta de la URL (http://localhost:8080/peliculas?categoria=Ficcion&director=George+Lucas)*
    - simples (http://localhost:8080/peliculas?categoria=Ficcion&director=George+Lucas):
    ```javascript
    app.get('/peliculas', function(req,res,next){
      console.log(req.query.director) // George Lucas
      console.log(req.query.categoria) // Ficcion
    });
    ```
    - Agrupados (http://localhost:8080/peliculas?categoria[tipo]=Corto&director=Yo+Mismo):
    ```javascript
    app.get('/peliculas', function(req,res,next){
      console.log(req.query.director) // Yo Mismo
      console.log(req.query.categoria.tipo) // Corto
    });
    ```
  - `req.body` *Contenido dentro de la propia petición*

- Manejadores: Métodos de respuesta
  - [res.download()](http://expressjs.com/es/4x/api.html#res.download) *Solicita un archivo para descargarlo.*
  - [res.end()](http://expressjs.com/es/4x/api.html#res.end) *Finaliza el proceso de respuesta.*
  - [res.json()](http://expressjs.com/es/4x/api.html#res.json) *Envía una respuesta JSON.*
  - [res.jsonp()](http://expressjs.com/es/4x/api.html#res.jsonp) *Envía una respuesta JSON con soporte JSONP.*
    - Valores por defecto ajustables en app.set()
      - *?callback=* valor por defecto en la petición
      - `res.jsonp({date: newDate()});`
  - [res.redirect()](http://expressjs.com/es/4x/api.html#res.redirect) *Redirecciona una solicitud.*
  - [res.render()](http://expressjs.com/es/4x/api.html#res.render) *Renderiza una plantilla a la que le pasa además datos (opcional)*
  - [res.send()](http://expressjs.com/es/4x/api.html#res.send) *Envía una respuesta de varios tipos.*
    - Muy flexible
      - Código y contenido `res.send(404,'Oops...');`
      - Enviar un JSON `res.send({mensaje: "secreto"});`
      - Solo código (autocompleta el mensaje) `res.send(200);` 


  - [res.sendFile()](http://expressjs.com/es/4x/api.html#res.sendFile) *Envía un archivo para ser visualizado.*
  - [res.sendStatus()](http://expressjs.com/es/4x/api.html#res.sendStatus) *Envía un archivo para ser descargado.*


**Mecánica: app.use()**
- Usando Middleware: app.use(middleware)
  - Declaración directa 

    ```javascript
    app.use((req, res, next) => {
        console.log("Petición en "+req.url+" con el método" + req.method);
        next(); 
    });
    ```

  - Enlazando

    ```javascript
    const express = require('express');
    const app = express();
    
    function chivato (req, res, next) {
        console.log(`Nueva petición en ${req.url} con el método ${req.method}`);
        next(); 
    };
    
    app.use(chivato);

    app.get('/', (req, res) => {
      res.send('Hola a todos!');
    });
    
    app.listen(3000);    
    ```

**Middleware: La clave**

![Mw_schema](http://image.slidesharecdn.com/introtonode-140914093424-phpapp01/95/intro-to-nodejs-14-638.jpg?cb=1410687757)

Una función que recibe 3 o 4 parámetros: req, res, next

- Tipos:
  - Middleware de nivel de aplicación
  - Middleware de nivel de direccionador
  - Middleware de manejo de errores
  - Middleware incorporado
  - Middleware de terceros

- Concatenación:
  - Al terminar su tarea, tiene que invocar a next()


**Middleware de nivel de aplicación**
- Global *Afecta a cualquier Ruta*

  ```javascript
  const app = express();
  
  app.use((req, res, next) => {
    console.log('Time:', Date.now());
    next();
  });
  ```

- Punto de Montaje *Afecta solo a una vía de acceso, en este caso /user/:id*

  ```javascript
  const app = express();
  
  app.get('/user/:id', (req, res, next) => {
    console.log('ID:', req.params.id);
    next();
  }, (req, res, next) => {
    res.send('User Info');
  });
  ```

**Middleware de nivel de direccionador**
- Global *Afecta a cualquier Ruta*

  ```javascript
  const app = express();
  const router = express.Router();
  
  router.use((req, res, next) => {
    console.log('Time:', Date.now());
    next();
  });
  ```

- Punto de Montaje *Afecta solo a una vía de acceso, en este caso /user/:id*

  ```javascript
  const app = express();
  const router = express.Router();
  
  router.get('/user/:id', (req, res, next) => {
    console.log('ID:', req.params.id);
    next();
  }, (req, res, next) => {
    res.send('User Info');
  });
  ```

**Middleware de manejo de errores**
- Argumento adiccional

  ```javascript
  const bodyParser = require('body-parser');
  const methodOverride = require('method-override');
  
  app.use(gestionErrorServer);
  
  function gestionErrorServer(err, req, res, next) {
    if (req.xhr) {
      res.status(500).send({ error: 'Something failed!' });
    } else {
      res.status(500);
      res.render('error', { error: err });
    }
  }
  
  //...
  ```

**Middleware incorporado**
- Desde la versión 4.x Express no depende de [Connect](https://github.com/senchalabs/connect)
- Solamente queda incorporado [express.static](https://github.com/expressjs/serve-static)
  - Incluyendo archivos estáticos

    ```javascript
    app.use(express.static('public'));
    ```

  - Configurando la carpeta pública

    ```javascript
    const options = {
      dotfiles: 'ignore',
      etag: false,
      extensions: ['htm', 'html'],
      index: false,
      maxAge: '1d',
      redirect: false,
      setHeaders(res, path, stat) {
        res.set('x-timestamp', Date.now());
      }
    }
    
    app.use(express.static('public', options));
    ```

  - Usando múltiples directorios estáticos

    ```javascript
    app.use(express.static('public'));
    app.use(express.static('uploads'));
    app.use(express.static('files'));
    ```


- Middleware oficial (No incorporado):
  - [serve-favicon](https://github.com/expressjs/serve-favicon)
    - Sirve el favicon
  - [Morgan](https://github.com/expressjs/morgan)
    - Logger para peticiones HTTP
  - [body-parser](https://github.com/expressjs/body-parser)
    - Decodifica:
      - application/json
      - application/x-www-form-urlencoded
      - multipart/form-data
    - Crea el objeto req.body con los parámetros
    - Crea el objeto req.files con los ficheros que se han subido desde un formulario
  - [basic-auth-connect](https://github.com/expressjs/basic-auth-connect)
    - Protección básica de las rutas usando usuario y contraseña
  - [csurf](https://github.com/expressjs/csurf)
    - Crea *req.session._csrf* 
    - Protección contra Cross-site request forgery
    - Usando tokens
  - [cors](https://github.com/expressjs/cors)
    - Gestión de Cross Origin Resource Sharing (CORS)
  - [compression](https://github.com/expressjs/compression)
    - [gzip](https://www.wikiwand.com/es/Gzip)
  - [express-session](https://github.com/expressjs/session)
    - Simple gestor de sesiones 
  - [multer](https://github.com/expressjs/multer)
    - *Node.js middleware for handling `multipart/form-data`.*
  - [cookie-session](https://github.com/expressjs/cookie-session)
    - *Simple cookie-based session middleware*
  - [cookie-parser](https://github.com/expressjs/cookie-parser)
    - *cookie parsing middleware*
    - Crea req.cookies
  - [cookie-session](https://github.com/expressjs/cookie-session)
    - Inicializa y parsea los datos de sesión del usuario
    - Utilizando cookies como almacenamiento
    - Algunas opciones avanzadas
  - [serve-static](https://github.com/expressjs/serve-static)
    - *Serve static files*
    - ¡Muy útil! Se pone cerca del final
    - Cachea los ficheros
    - La variable global __dirname contiene el directorio donde reside el script en ejecución
  - [vhost](https://github.com/expressjs/vhost)
    - Virtual Domain Hosting
  - [restful-router](https://github.com/expressjs/restful-router)
    - *Simple RESTful url router.*
  - [connect-markdown](https://github.com/expressjs/connect-markdown)
    - *Auto convert markdown to html for connect.*

**Middleware: Más Middleware, más funcionalidad**
- [La lista de Raynos](https://github.com/Raynos/http-framework)

- Habilitando CORS

  ```javascript
  app.use(function(req, res, next) {
    res.header("Access-Control-Allow-Origin", "*");
    res.header('Access-Control-Allow-Methods', 'GET,PUT,POST,DELETE');
    res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
    next();
  });
  ```

- Baneando Navegadores (IE8 y anteriores)

  ```javascript
  // ban.js
  const banned = [ 'MSIE', 'Trident/6.0'];
  
  module.exports = () => (req, res, next) =>{
    if (req.headers['user-agent'] !== undefined && req.headers['user-agent'].indexOf(banned) > -1) {
      res.end('Navegador no compatible');
    } else { 
      next(); 
    }
  };
  ```

- Mapeado de parámetros en rutas.
  - Cuidado con app.param()
    - Funcionamiento (orden de busqueda):
      - req.params
      - req.body
      - req.query

    ```javascript
    app.param('id_usuario', (req, res, next, id) =>{
      // Llamamos a una función que valida....
      validadorUsuario(id, (err, usuario) => {
        if (err) { 
          next(err);
        } else if (user) { 
          // Actualizamos con los nuevos datos
          req.params.usuario = usuario; 
          // damos paso a la siguiente función
          next();
        } else {
          next(new Error('Error al cargar el usuario'));
        } 
      });
    });
    ```

-  Redireccionando al usuario en caso de no estar logados

  ```javascript
  module.exports = (req, res, next) => {
    if (req.params.usuario.logged){
      next();
    } else {
      res.redirect('/login');
    }
  };
  ```

- Gestion de errores tipo 4xx y tipo 5xx

  ```javascript
  // Error 404
  app.use((req, res) => {
    res.status(400);
    res.render('404', { title: '404 - No encontrado' });
  });
  
  // Error 500 (solo en caso de desarrollo)
  app.use('development', (error, req, res, next) => {
    res.status(500);
    res.render('500', {
      title: 'Jefe, ¡Tenemos un 500!',
      error: error
    });
  });
  
  
  // Error 500 (solo en caso producción)
  app.use('production', (error, req, res, next) => {
    res.status(500);
    res.render('500', {
      title: 'Oops… ¡Algo salió mal!'
    });
    // Mandamos un email con los datos al equipo.
  });
  ```

**[Ejemplos con Express](https://github.com/expressjs/express/tree/master/examples)**


**Express en resumen**

- GET Básico

  ```javascript
  app.get('/hola', (req, res) => {
      res.send('hemos abierto una nueva ruta!');
  });
  ```

- POST Básico
  - app.js 

    ```javascript
    app.post('/', (req, res) => {
      res.send(req.body);
    });
    ```

  - index.jade 

    ```jade
    section.container
    h1 Manda tu mensaje!
  
    form(method='post', action='/')
      fieldset
        legend Mandame tu mensaje:
        p.contenido
          label Tu mensaje
          input(name='mensaje')
        p.acciones
          input(type='submit', value='Enviar')
    ```

  - respuesta 

    ```javascript
    {
      "mensaje": "Hola Cracks!"
    }
    ```


- Parámetros en las rutas
  - app.js 

    ```javascript
    app.get('/hola/:usuario', (req, res) => {
        res.send(`Hola ${req.params.usuario}. Hemos abierto una nueva ruta personalizada!`);
    });
    ```

- Simulando una respuesta de una base de datos en las rutas:

  - app.js 

    ```javascript
    app.get('/consulta/:usuario', (req, res) => {
      const datos = {
        marca: "Seat",
        modelo: "Ibiza",
        edad: 20,
        ITVPasada: true,
        seguroPasado: true
      };
      
      res.render('consulta.jade', {usuario: req.params.usuario, datos: datos});
    });
    ```

  - consulta.jade 

  ```jade
  .datos
    h3 Datos: 
    p= "El Coche de "+usuario+" es un "+datos.marca+" "+datos.modelo
      
    h3 Detalles técnicos:
    ul
        li= "ITV en regla: " +datos.ITVPasada 
        li= "seguro en regla: " +datos.seguroPasado
  ```

**Utilidades**

- Recuperar cabeceras:

  ```
  curl -I 127.0.0.1:3000
  ```

- [PostMan](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)
- [Html2Jade](http://html2jade.org/)



### PUG (antes Jade)

![Jade_logo](https://css-tricks.com/wp-content/uploads/2016/01/jade-logo-1.png)

**[Jade... ya no se llama jade. Ahora se llama PUG](https://github.com/pugjs/pug/issues/2184)**

![PUG_logo](https://camo.githubusercontent.com/be9ed9b1e0a28a074109fc994da6d00c1d8cd6e6/68747470733a2f2f63646e2e7261776769742e636f6d2f7075676a732f7075672d6c6f676f2f336561326433613836633632323730323064643562323037343361356161343538383038636134652f5356472f5f5f7075672d6c6f676f2d636f6c6f75722d776964652e737667)

**Implementaciones en otros lenguajes**
- [php](https://github.com/kylekatarnls/jade-php)
- [scala](https://scalate.github.io/scalate/documentation/scaml-reference.html)
- [ruby](https://github.com/slim-template/slim)
- [python](https://github.com/SyrusAkbary/pyjade)
- [java](https://github.com/neuland/jade4j)


- **Entendiendo la mécanica**
  - index.jade:

    ```jade
    doctype html
    html(lang="en")
      head
        title= pageTitle
        script(type='text/javascript').
          if (foo) {
             bar(1 + 5)
          }
      body
        h1 Jade - node template engine
        #container.col
          if youAreUsingJade
            p You are amazing
          else
            p Get on it!
          p.
            Jade is a terse and simple
            templating language with a
            strong focus on performance
            and powerful features.
    ```
  
  - index.html:

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <title>Jade</title>
        <script type="text/javascript">
          if (foo) {
             bar(1 + 5)
          }
        </script>
      </head>
      <body>
        <h1>Jade - node template engine</h1>
        <div id="container" class="col">
          <p>You are amazing</p>
          <p>
            Jade is a terse and simple
            templating language with a
            strong focus on performance
            and powerful features.
          </p>
        </div>
      </body>
    </html>
    ```
  
- Bootstrap:
  - index.jade:

    ```jade
    doctype html
    html
      head
        title title
        include ./includes/styles.jade
      body
        .row
          .container
            .jumbotron
              h1 Hola, desde Bootstrap!
              p ¿Qué te parece?
              p
                a.btn.btn-primary.btn-lg(href='http://getbootstrap.com/', role='button') Aprende más!
        include ./includes/scripts.jade
    ```

  - includes/styles.jade

    ```jade
    //- includes/styles.jade
    // Bootstrap
    link(rel='stylesheet', href='//maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css')
    ```

  - includes/scripts.jade

    ```jade
    //- includes/scripts.jade
    // Jquery
    script(src='//ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js')
    // Bootstrap
    script(src='//maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js')
    ```

  - index.html

    ```html
    <!DOCTYPE html>
    <html>
      <head>
        <title>title</title>
        <!-- Bootstrap-->
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css">
        </head>
      <body>
        <div class="row">
          <div class="container">
            <div class="jumbotron">
              <h1>Hello, desde Bootstrap!</h1>
              <p>¿Qué te parece?</p>
              <p>
                  <a href="http://getbootstrap.com/" role="button" class="btn btn-primary btn-lg">Aprende más!</a>
              </p>
            </div>
          </div>
        </div>
        <!-- Jquery-->
        <script src="//ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
        <!-- Bootstrap-->
        <script src="//maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js"></script>
      </body>
    </html>
    ```

- [Pug - Github](https://github.com/pugjs/pug)
- [Pug - Getting Started](https://pugjs.org/api/getting-started.html)
- [Jade Syntax Documentation by example](http://naltatis.github.io/jade-syntax-docs/)


### Ejercicios

**1 -** Crearemos una aplicación utilizando Express para gestionar las peliculas que nos gustan.

```javascript
  // Tu solución
```