# Clase 6

### Firebase

![FirebaseLogo](https://firebase.google.com/images/brand-guidelines/logo-standard.png)

- [Pricing](https://firebase.google.com/pricing/)
- [Features](https://firebase.google.com/features/)
- [Clientes](https://firebase.google.com/customers/)
- [Documentación](https://firebase.google.com/docs/)
  - [Primeros Pasos](https://firebase.google.com/docs/web/setup)
  - [Referencia de la API](https://firebase.google.com/docs/reference/js/)
  - [Ejemplos](https://firebase.google.com/docs/samples/#web)
- [Librerías y ayudas](https://firebase.google.com/docs/libraries/)

### Aprendiendo con Firebase 2.x

- [Firebase Docs](https://www.firebase.com/docs/)
- [Firebase Open Data Sets (deprecated)](https://www.firebase.com/docs/open-data/)
- [Firebase - GeoFire](https://github.com/firebase/geofire-js)
- [Firebase - Backbone](https://www.firebase.com/docs/web/libraries/backbone/quickstart.html)
- [Firebase - Angular](https://www.firebase.com/docs/web/libraries/angular/quickstart.html)
- [Firebase - Nodejs/js](https://www.firebase.com/docs/web/quickstart.html)
- [Firebase - Ionic](https://www.firebase.com/docs/web/libraries/ionic/guide.html)
- [Firebase - React](https://www.firebase.com/docs/web/libraries/react/)
- [Firebase - Ember](https://www.firebase.com/docs/web/libraries/ember/)


**Primeros pasos**

- Crear una cuenta:
  - [SignUp](https://www.firebase.com/signup/)
  
- Gestionar dependéncias en cliente:
```javascript
  <script src="https://cdn.firebase.com/js/client/2.2.9/firebase.js"></script>
```

- Gestionar dependéncias en Nodejs:
```
  npm install firebase -save
```


**Limitaciones**

- [Limitaciones técnicas](https://www.firebase.com/docs/web/guide/understanding-data.html#section-limitations)
- [Conversión de Arrays](https://www.firebase.com/docs/web/guide/understanding-data.html#section-arrays-in-firebase)


**Guardando Datos**

- [Guardando datos en Firebase](https://www.firebase.com/docs/web/guide/saving-data.html#section-ways-to-save)
- set() Almacena / remplaza los datos
- update() Actualiza los datos
- push() Alamacena los datos con un ID único.
- transaction() Para datos complejos y cocurridos.




- set():

```javascript
  var ref = new Firebase("https://<<---URL--->>.firebaseio.com/fb-ejemplos/escritura");
  var usersRef = ref.child("users");
  usersRef.set({
    alanisawesome: {
      date_of_birth: "June 23, 1912",
      full_name: "Alan Turing"
    },
    gracehop: {
      date_of_birth: "December 9, 1906",
      full_name: "Grace Hopper"
    }
  });
```

```javascript
  var ref = new Firebase("https://<<---URL--->>.firebaseio.com/fb-ejemplos/escritura");
  usersRef.child("alanisawesome").set({
    date_of_birth: "June 23, 1912",
    full_name: "Alan Turing"
  });
  usersRef.child("gracehop").set({
    date_of_birth: "December 9, 1906",
    full_name: "Grace Hopper"
  });
```


- update():

```javascript
  var hopperRef = usersRef.child("gracehop");
  hopperRef.update({
    "nickname": "Amazing Grace"
  });
```

- push():

```javascript
// update y Callback
  var dataRef = ref.child("IDs");
  dataRef.push("Guardando datos...", function(error) {
    if (error) {
      console.warn("No se han podido guardar los datos." + error);
    } else {
      console.info("Datos guardados con exito.");
    }
  });
```

- **[Demo](https://codepen.io/ulisesgascon/pen/pyYYoR)**


**Eventos**

- Evento (value):

```javascript
  var ref = new Firebase("https://docs-examples.firebaseio.com/web/saving-data/fireblog/posts");
  
  ref.on("value", function(snapshot) {
    console.log(snapshot.val());
  }, function (errorObject) {
    console.log("Fallo en lectura de datos: " + errorObject.code);
  });
```


- Evento (child_changed):

```javascript
  var ref = new Firebase("https://<<--URL-->>.firebaseio.com/fb-ejemplos/escritura/users");
  
  ref.on("child_changed", function(snapshot) {
    var usersData = snapshot.val();
    console.log("Nuevos cambios(child_changed): ", usersData);
  });
```


- Evento (child_removed):

```javascript
  var ref = new Firebase("https://<<--URL-->>.firebaseio.com/fb-ejemplos/escritura/users");
  
  ref.on("child_removed", function(snapshot) {
    var usersData = snapshot.val();
    console.log("Usuario eliminado(child_removed): ", usersData);
  });
```


- once() *una vez*:

```javascript
var ref = new Firebase("https://<<--URL-->>.firebaseio.com/fb-ejemplos/escritura/users");

ref.once("child_changed", function(snapshot) {
  var usersData = snapshot.val();
  console.log("Nuevo cambio(once - child_changed): " + usersData);
});
```


- Quitar evento (value):

```javascript
  ref.off("value");
```

- Quitar todos los eventos:

```javascript
  ref.off();
```

- **[Demo](https://codepen.io/ulisesgascon/pen/grEEeP)**


**Queries**

- orderByChild() Ordenar por hijo
- orderByKey() Ordenar por Llave
- orderByValue() Ordenar por valor
- orderByPriority() Ordenar por prioridad
- Documentación
  - [Firebase - Queries Part I](https://www.firebase.com/blog/2013-10-01-queries-part-one.html)
  - [Firebase - Queries Part II](https://www.firebase.com/blog/2014-01-02-queries-part-two.html)
  - [Firebase - Denormalizing is normal](https://www.firebase.com/blog/2013-04-12-denormalizing-is-normal.html)
  - [Firebase Docs - Ordenando Datos](https://www.firebase.com/docs/web/guide/retrieving-data.html#section-ordered-data)



- orderByChild():

```javascript
  var ref = new Firebase("https://dinosaur-facts.firebaseio.com/dinosaurs");
  ref.orderByChild("height").on("child_added", function(snapshot) {
    console.log(snapshot.key() + " was " + snapshot.val().height + " meters tall");
  });
```

- orderByKey():

```javascript
  var ref = new Firebase("https://dinosaur-facts.firebaseio.com/dinosaurs");
  ref.orderByKey().on("child_added", function(snapshot) {
    console.log(snapshot.key());
  });
```

- orderByValue():

```javascript
  var scoresRef = new Firebase("https://dinosaur-facts.firebaseio.com/scores");
  scoresRef.orderByValue().on("value", function(snapshot) {
    snapshot.forEach(function(data) {
      console.log("The " + data.key() + " dinosaur's score is " + data.val());
    });
  });
```

- **[Demo](https://codepen.io/ulisesgascon/pen/dMrrgb)**

**Queries Avanzadas**

- limitToFirst() desde el primero...
- limitToLast() desde el final...
- startAt() empiezan por...
- endAt() terminan por...
- equalTo() igual a...


**Queries Avanzadas (básicos)**

- limitToFirst():

```javascript
  var ref = new Firebase("https://dinosaur-facts.firebaseio.com/dinosaurs");
  ref.orderByChild("height").limitToFirst(2).on("child_added", function(snapshot) {
    console.log(snapshot.key());
  });
```


- limitToLast():

```javascript
  var ref = new Firebase("https://dinosaur-facts.firebaseio.com/dinosaurs");
  ref.orderByChild("weight").limitToLast(2).on("child_added", function(snapshot) {
    console.log(snapshot.key());
  });
```


**Queries Avanzadas (concatenando)**

- .orderByValue() y .limitToLast():

```javascript
  var scoresRef = new Firebase("https://dinosaur-facts.firebaseio.com/scores");
  scoresRef.orderByValue().limitToLast(3).on("value", function(snapshot) {
    snapshot.forEach(function(data) {
      console.log("The " + data.key() + " dinosaur's score is " + data.val());
    });
  });
```


- .orderByChild() y .startAt():

```javascript
  var ref = new Firebase("https://dinosaur-facts.firebaseio.com/dinosaurs");
  ref.orderByChild("height").startAt(3).on("child_added", function(snapshot) {
    console.log(snapshot.key());
  });
```


- .orderByKey() y .endAt():

```javascript
  var ref = new Firebase("https://dinosaur-facts.firebaseio.com/dinosaurs");
  ref.orderByKey().endAt("pterodactyl").on("child_added", function(snapshot) {
    console.log(snapshot.key());
  });
```


- .startAt() y .endAt() *usando tilde*:

```javascript
var ref = new Firebase("https://dinosaur-facts.firebaseio.com/dinosaurs");
ref.orderByKey().startAt("b").endAt("b~").on("child_added", function(snapshot) {
  console.log(snapshot.key());
});
```

- .equalTo():

```javascript
  var ref = new Firebase("https://dinosaur-facts.firebaseio.com/dinosaurs");
  ref.orderByChild("height").equalTo(25).on("child_added", function(snapshot) {
    console.log(snapshot.key());
  });
```


- Ejemplo: *Busquemos un dinosaurio que sea mas pequeño que un Stegosaurus*

```javascript
  var ref = new Firebase("https://dinosaur-facts.firebaseio.com/dinosaurs");
  ref.child("stegosaurus").child("height").on("value", function(stegosaurusHeightSnapshot) {
    var favoriteDinoHeight = stegosaurusHeightSnapshot.val();
  
    var queryRef = ref.orderByChild("height").endAt(favoriteDinoHeight).limitToLast(2)
    queryRef.on("value", function(querySnapshot) {
        if (querySnapshot.numChildren() == 2) {
          // Data is ordered by increasing height, so we want the first entry
          querySnapshot.forEach(function(dinoSnapshot) {
            console.log("el dinosaurio más pequeño que el Stegosaurus es " + dinoSnapshot.key());
  
            // Returning true means that we will only loop through the forEach() one time
            return true;
          });
        } else {
          console.log("El Stegosaurus es el dinosaurio más pequeño");
        }
    });
  });
```

- **[Demo](https://codepen.io/ulisesgascon/pen/qZvvve)**

**Trabajar Offline**

- [Documentación](https://www.firebase.com/docs/web/guide/saving-data.html#section-writes-offline)


- Realizando acciones al desconectarse:

```javascript
  var presenceRef = new Firebase('https://<<--URL-->>.firebaseio.com/info/connectednow');
  presenceRef.onDisconnect().set("I disconnected!");
  
```



**Social Login**

- [User-auth con Firebase](https://www.firebase.com/docs/web/guide/user-auth.html)
- [Ejemplo en jsfiddle](http://jsfiddle.net/firebase/a221m6pb/embedded/result,js,css/)


**Seguridad y Autorización**

- [Ajustes de seguridad](https://www.firebase.com/docs/security/guide/securing-data.html)


**Deploy**

- [Deploy en Cloud](https://www.firebase.com/docs/web/guide/deploying.html)
- [Deploy usando Node](https://www.firebase.com/docs/hosting/quickstart.html)




### Analicemos Código

- [Código Fuente demo de Velocidad](https://github.com/UlisesGascon/raspberrypi-system-info-data-to-firebase)
- [Curratelo](https://github.com/UlisesGascon/curratelo)
- [Raspberrypi system info data to Firebase](https://github.com/UlisesGascon/raspberrypi-system-info-data-to-firebase)
- [Calidad del Aire con Firebase](https://github.com/UlisesGascon/Calidad-del-Aire-con-Firebase)
- [Agroduino](https://github.com/UlisesGascon/Agroduino)
- [Aire Madrid](https://github.com/UlisesGascon/Aire-Madrid)
- [EMT Bus Live](https://github.com/Borjagodoy/emtBusLive)
- [Bitcoin price ticker with Arduino](https://github.com/UlisesGascon/Bitcoin-price-ticker-with-Arduino)
- [MovieFire con Nodejs](https://github.com/UlisesGascon/Simple-API-REST-with-Firebase-and-IMBD)


### [Nuevo Firebase 3.x/4.x](https://firebase.google.com/)

![new_logo](http://cdn772.swedroid.se/wp-content/uploads/2016/05/google-firebase-logo-600x308.png)
![funcionalidades](https://cdn.scotch.io/1/Bg4r7dI1Q2W3bX9Sf4oD_unnamed.png)


**Lo nuevo**
- [Firebase Docs](https://firebase.google.com/docs/web/setup)
- [Firebase - Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/js/client)
- [Firebase - Authentication](https://firebase.google.com/docs/auth/web/firebaseui)
- [Firebase - Real Time DB](https://firebase.google.com/docs/database/web/start)
- [Firebase - Storage](https://firebase.google.com/docs/storage/web/start)
- [Firebase - Hosting](https://firebase.google.com/docs/hosting/)
- [Muchos más](https://firebase.google.com/docs/)


**Más info**
- [Firebase expands to become a unified app platform](https://firebase.googleblog.com/2016/05/firebase-expands-to-become-unified-app-platform.html)
- [MIgration guide](https://firebase.google.com/support/guides/firebase-web)
- [Survival guide: how to migrate from the Firebase Realtime Database to Cloud Firestore](https://medium.freecodecamp.org/rtdb-to-firestore-fd8da8149877)
- [What we’ve learned from four years of using Firebase](https://medium.com/sketchdeck-developer-blog/what-weve-learned-from-four-years-of-using-firebase-d1f81b3395b5)

**Claves del cambio**
- Nueva Interfaz
- Muchas funcionalidades Nuevas
- Un enfoque amplio a desarrollo de apps nativas (Android e iOS)
- Existe un asistente para migrar los proyectos a la nueva consola
- Los nuevos proyectos ya no componen el nombre del dominio

### Migración de FIrebase 2.x a 3.x

**Creación de una cuenta**

1. Darse de alta en la [we de Firebase](https://www.firebase.com/signup/) mediante la cuenta de Google.
2. Crear un proyecto de Firebase en la [consola de administración](https://console.firebase.google.com).
3. Crear o asociar un proyecto de Google.
4. Crear un proyecto de Firebase.

**Configuración cliente**

```html
<script src="https://www.gstatic.com/firebasejs/4.9.1/firebase.js"></script>
<script>
  // Initialize Firebase
  // TODO: Replace with your project's customized code snippet
  var config = {
    apiKey: "<API_KEY>",
    authDomain: "<PROJECT_ID>.firebaseapp.com",
    databaseURL: "https://<DATABASE_NAME>.firebaseio.com",
    storageBucket: "<BUCKET>.appspot.com",
    messagingSenderId: "<SENDER_ID>",
  };
  firebase.initializeApp(config);
</script>
```

En caso de no necesitar todas las funcionalidades podemos importarlas por separado:

```html
<script src="https://www.gstatic.com/firebasejs/4.9.1/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/4.9.1/firebase-auth.js"></script>
<script src="https://www.gstatic.com/firebasejs/4.9.1/firebase-database.js"></script>
<script src="https://www.gstatic.com/firebasejs/4.9.1/firebase-firestore.js"></script>
<script src="https://www.gstatic.com/firebasejs/4.9.1/firebase-messaging.js"></script>
```

**Configuración Nodejs**

1. Instalar la dependencia

  ```bash
  $ npm install firebase --save
  ```

2. Importar el paquete
  
  ```javascript
  var firebase = require("firebase");
  ```

3. Inicializar el SDK

  ```javascript
  var config = {
    apiKey: "<API_KEY>",
    authDomain: "<PROJECT_ID>.firebaseapp.com",
    databaseURL: "https://<DATABASE_NAME>.firebaseio.com",
    storageBucket: "<BUCKET>.appspot.com",
  };
  firebase.initializeApp(config);
  ```

**Servicios disponibles en el SDK**
- `firebase.auth()`: Authentication
- `firebase.storage()`: Cloud Storage
- `firebase.database()`: Realtime Database
- `firebase.firestore()`: Cloud Firestore



**Los métodos de obtención sin argumento son propiedades solo de lectura**
- Antes
```javascript
// Reference
  var key = ref.key();
  var rootRef = ref.root();
  var parentRef = ref.parent();

// Query
  var queryRef = query.ref();

// DataSnapshot
  ref.on("value", function(snapshot) {
    var dataRef = snapshot.ref();
    var dataKey = snapshot.key();
  });
```

- Ahora
```javascript
// Reference
  var key = ref.key;
  var rootRef = ref.root;
  var parentRef = ref.parent;

// Query
  var queryRef = query.ref;

// DataSnapshot
  ref.on("value", function(snapshot) {
    var dataRef = snapshot.ref;
    var dataKey = snapshot.key;
  });
```


**Actualización de tu código de autenticación**
- Antes
```javascript
  ref.authWithOAuthPopup("twitter", function(error, authData) {
    if (error) {
      // An error occurred
      console.error(error);
    } else {
      // User signed in!
      var uid = authData.uid;
    }
  });
```

- Ahora
```javascript
  var auth = firebase.auth();
  
  var provider = new firebase.auth.TwitterAuthProvider();
  auth.signInWithPopup(provider).then(function(result) {
    // User signed in!
    var uid = result.user.uid;
  }).catch(function(error) {
    // An error occurred
  });
```


**Obtener el token de acceso**

- Antes
```javascript
  ref.onAuth(function(authData) {
    if (authData) {
      var accessToken = authData.providerData[authData.provider].accessToken;
    }
  });
```

- Ahora
```javascript
  var auth = firebase.auth();
  
  var provider = new firebase.auth.GoogleAuthProvider();
  auth.signInWithPopup(provider).then(function(result) {
    var accessToken = result.credential.accessToken;
  });
```


**Controlar el estado de autenticación**

- Antes
```javascript
  ref.onAuth(function(authData) {
    if (authData) {
      // User signed in!
      var uid = authData.uid;
    } else {
      // User logged out
    }
  });
```

- Ahora
```javascript
  var auth = firebase.auth();
  
  auth.onAuthStateChanged(function(user) {
    if (user) {
      // User signed in!
      var uid = user.uid;
    } else {
      // User logged out
    }
  });
```




### Authentication

![auth](https://firebase.google.com/docs/auth/images/auth-providers.png?hl=es-419)

[Todas las funcionalidades](https://firebase.google.com/docs/auth/web/start)

**FirebaseUI**

FirebaseUI es una capa que recubre el módulo de autenticación de Firebase que provee de flujos visuales de autenticación con las plataformas más utilizadas de la web.

> Añade fácilmente autenticación visual mediante FirebaseUI

- **Multiple Providers**: Email, teléfono, Google, Facebook, Twitter and GitHub sign-in.
- **Account Linking**: Flujos definidos para almacenar la información del usuario.
- **Customization**: Permite sobreescribir los estilos CSS por defecto.
- **One-tap**: Un único click para autenticarse
- **Localized UI**: Internacionalización para 40 idiomas.

**Login con Google** (sólo cliente)

```javascript
const provider = new firebase.auth.GoogleAuthProvider();

// Open login pop-up
firebase.auth().signInWithPopup(provider).then((result) => {
  // This gives you a Google Access Token. You can use it to access the Google API.
  var token = result.credential.accessToken;
  // The signed-in user info.
  var user = result.user;
  // ...
}).catch((error) => {
  // Handle Errors here.
  var errorCode = error.code;
  var errorMessage = error.message;
  // The email of the user's account used.
  var email = error.email;
  // The firebase.auth.AuthCredential type that was used.
  var credential = error.credential;
  // ...
});
```

**Login con Google** (Nodejs)

1. Recupera el `idToken` de la respuesta de la autenticación y envíalo al back-end:

  ```javascript
  const provider = new firebase.auth.GoogleAuthProvider();

  // Open login pop-up
  firebase.auth().signInWithPopup(provider).then((result) => {
    const token = result.client.idToken;
    // Send the token to the server
  });
  ```

2. Utiliza el token para autenticarte en el servidor

  ```javascript
  // Build Firebase credential with the Google ID token.
  const credential = firebase.auth.GoogleAuthProvider.credential(id_token);

  // Sign in with credential from the Google user.
  firebase.auth().signInWithCredential(credential).then((response) =>{
    // ...
  });
  ```

**Detectar cambios de usuario**

```javascript
firebase.auth().onAuthStateChanged((user) => {
  if (!user) {
    // Do something...
  }
});
```

*### Cloud Storage

![storage](https://cdn-images-1.medium.com/max/1600/1*w1IJOmdzBNji2uAyXX4XgQ.jpeg)

[Todas las funcionalidades](https://firebase.google.com/docs/storage/web/start)

**Subir ficheros**

```javascript
// Create a root reference
const storageRef = firebase.storage().ref();

// use the Blob or File API
const file = ...

// Upload the file
storageRef.put(file).then((snapshot) => {
  console.log('Uploaded a blob or file!');
});
```

**Descargar ficheros**

```javascript
// Create a root reference
const storageRef = firebase.storage().ref();

storageRef.child('images/stars.jpg').getDownloadURL().then((url) => {
  // `url` is the download URL for 'images/stars.jpg'

  // This can be downloaded directly:
  fetch(url)
      .then((response) => response.blob())
      .then((file) => {
          console.log('Here is the file!', file);
      });

  // Or inserted into an <img> element:
  var img = document.getElementById('myimg');
  img.src = url;
}).catch(function(error) {
  // Handle any errors
});
```

**Recursos**
- [Example of native HTML5 file drag and drop with Firebase](https://github.com/fedosejev/html5-file-drag-and-drop-firebase)
- [Getting Started with Firebase Storage on the Web - Firecasts](https://www.youtube.com/watch?v=SpxHVrpfGgU)
- [https://hurlatunde.github.io/multiple-drag-and-drop-file-uploading-to-firebase-storage](https://hurlatunde.github.io/multiple-drag-and-drop-file-uploading-to-firebase-storage)


### Firebase Cloud Functions

![logo](https://cdn-images-1.medium.com/max/1600/1*P96fpzo_Tr0PgJwZjEjHxw.png)

#### ¿Cómo Funciona?

> Después de escribir y de implementar una función, los servidores de Google comienzan a administrarla de inmediato. Para ello, detectan eventos y ejecutan la función cuando se activa. A medida que la carga aumenta o disminuye, la respuesta de Google es escalar con rapidez la cantidad de instancias de servidor virtual necesarias para ejecutar la función.

**Ciclo de vida de una función**

1. El programador escribe código para una nueva función, selecciona un proveedor de eventos (como Realtime Database) y define las condiciones según las cuales debe ejecutarse la función.
2. El programador implementa la función y Firebase la conecta al proveedor de eventos seleccionado.
3. Cuando el proveedor de eventos genera un evento que coincide con las condiciones de la función, se invoca el código.
4. Si la función está ocupada con muchos eventos, Google crea más instancias para controlar el trabajo con más rapidez. Si la función está inactiva, las instancias se borran.
5. Cuando el programador actualiza la función mediante la implementación del código actualizado, todas las instancias de la versión antigua se borran y se reemplazan por instancias nuevas.
6. Cuando un programador borra la función, se borran todas las instancias y se quita la conexión entre la función y el proveedor de eventos.

**TL:DR;**

- Configura Cloud Functions
- Escribe funciones
- Implementa y supervisa

### Ejemplos


**Notifica a los usuarios cuando ocurre algo interesante**

![img](https://firebase.google.com/docs/functions/images/notify.png?hl=es-419)

**Ejecuta limpieza y mantenimiento de Realtime Database**

![img](https://firebase.google.com/docs/functions/images/sanitization.png?hl=es-419)

**Ejecuta tareas intensivas en la nube en lugar de en la app**

![img](https://firebase.google.com/docs/functions/images/intensive.png?hl=es-419)

**Realizar integraciones con API y servicios de terceros**

![img](https://firebase.google.com/docs/functions/images/commit.png?hl=es-419)


### Arrancando el proyecto

**Dependencias**
```bash
npm install firebase-functions@latest firebase-admin@latest --save
npm install -g firebase-tools
```

**Puesta en marcha**
1. Ejecuta `firebase login` para acceder a través del navegador y autenticar la herramienta de Firebase.
_Nota: `firebase login --no-localhost` en C9.io_
2. Ve al directorio de tu proyecto de Firebase.
3. Ejecuta `firebase init functions`.

### Restricciones importantes

> Los proyectos de Firebase en el plan Spark solo pueden realizar solicitudes de salida a las API de Google. Las solicitudes a API de terceros generan un error. Para obtener más información acerca de cómo cambiar tu proyecto a un plan superior. 

_[Consulta Precios](https://firebase.google.com/pricing/?hl=es-419)_.


### Estrcutura del proyecto

```
myproject
 +- .firebaserc    # Hidden file that helps you quickly switch between
 |                 # projects with `firebase use`
 |
 +- firebase.json  # Describes properties for your project
 |
 +- functions/     # Directory containing all your functions code
      |
      +- .eslintrc.json  # Optional file containing rules for JavaScript linting.
      |
      +- package.json  # npm package file describing your Cloud Functions code
      |
      +- index.js      # main source file for your Cloud Functions code
      |
      +- node_modules/ # directory where your dependencies (declared in
                       # package.json) are installed
```

### Composición del `index.js`

```javascript
// The Cloud Functions for Firebase SDK to create Cloud Functions and setup triggers.
const functions = require('firebase-functions');

// The Firebase Admin SDK to access the Firebase Realtime Database.
const admin = require('firebase-admin');
admin.initializeApp(functions.config().firebase);

//...
```

#### Activadores

- [Cloud Firestore](https://firebase.google.com/docs/functions/firestore-events?hl=es-419)
- [Realtime Database](https://firebase.google.com/docs/functions/database-events?hl=es-419)
- [Firebase Authentication](https://firebase.google.com/docs/functions/auth-events?hl=es-419)
- [Google Analytics para Firebase](https://firebase.google.com/docs/functions/analytics-events?hl=es-419)
- [Crashlytics](https://firebase.google.com/docs/functions/crashlytics-events?hl=es-419)
- [Cloud Storage](https://firebase.google.com/docs/functions/gcp-storage-events?hl=es-419)
- [Pub/Sub de Cloud](https://firebase.google.com/docs/functions/pubsub-events?hl=es-419)
- [Activadores HTTP](https://firebase.google.com/docs/functions/http-events?hl=es-419)


### Ejemplos sencillos

**Hello World disparado por eventos en base de datos**
```javascript
const functions = require('firebase-functions');
const admin = require('firebase-admin');
admin.initializeApp(functions.config().firebase);

// Always change the value of "/hello" to "world!"
exports.hello = functions.database.ref('/hello').onWrite(event => {
  // set() returns a promise. We keep the function alive by returning it.
  return event.data.ref.set('world!').then(() => {
    console.log('Write succeeded!');
  });
});
```


**Aquí se muestra la versión completa de functions/index.js, que contiene las funciones addMessage() y makeUppercase().**

*Estas funciones te permiten pasarle un parámetro a un extremo HTTP que escribe un valor en Realtime Database, para luego transformarlo mediante el uso de mayúsculas en todos los caracteres de la string.*

```javascript
// The Cloud Functions for Firebase SDK to create Cloud Functions and setup triggers.
const functions = require('firebase-functions');

// The Firebase Admin SDK to access the Firebase Realtime Database.
const admin = require('firebase-admin');
admin.initializeApp(functions.config().firebase);

// Take the text parameter passed to this HTTP endpoint and insert it into the
// Realtime Database under the path /messages/:pushId/original
exports.addMessage = functions.https.onRequest((req, res) => {
  // Grab the text parameter.
  const original = req.query.text;
  // Push the new message into the Realtime Database using the Firebase Admin SDK.
  admin.database().ref('/messages').push({original: original}).then(snapshot => {
    // Redirect with 303 SEE OTHER to the URL of the pushed object in the Firebase console.
    res.redirect(303, snapshot.ref);
  });
});

// Listens for new messages added to /messages/:pushId/original and creates an
// uppercase version of the message to /messages/:pushId/uppercase
exports.makeUppercase = functions.database.ref('/messages/{pushId}/original')
    .onWrite(event => {
      // Grab the current value of what was written to the Realtime Database.
      const original = event.data.val();
      console.log('Uppercasing', event.params.pushId, original);
      const uppercase = original.toUpperCase();
      // You must return a Promise when performing asynchronous tasks inside a Functions such as
      // writing to the Firebase Realtime Database.
      // Setting an "uppercase" sibling in the Realtime Database returns a Promise.
      return event.data.ref.parent.child('uppercase').set(uppercase);
    });
```

### [Ejemplos para reutilizar](https://github.com/firebase/functions-samples)

 1. [**Quickstarts**](https://github.com/firebase/functions-samples/blob/master/README.md#quickstarts) are minimal examples for each types of triggers.
 2. [**Development Environment Samples and Boilerplates**](https://github.com/firebase/functions-samples/blob/master/README.md#environment) illustrates how to get started with
different, commonly used JavaScript development patterns such as Typescript, React SSR, ES2017 etc...
 3. [**Image Processing**](https://github.com/firebase/functions-samples/blob/master/README.md#image) shows a few ways where you can process and transform images using Cloud Functions such as generating thumbnails, converting images extracting metadata...
 4. [**Firebase Realtime Database Data Consistency**](https://github.com/firebase/functions-samples/blob/master/README.md#rtdb) show how to implement automatic data consistency such as keeping a count of children, having a max amount of node childs, cleaning up old data etc... for your Realtime Database.
 5. [**Other common usecases**](https://github.com/firebase/functions-samples/blob/master/README.md#other) a set of other common usecases for Cloud Functions.

### Despliegue y pruebas

- [Primeros pasos: Cómo escribir y también implementar tus primeras funciones](https://firebase.google.com/docs/functions/get-started?hl=es-419)
- [Ejecuta funciones de manera local](https://firebase.google.com/docs/functions/local-emulator?hl=es-419)

### Recursos

- [Google Codelab: firebase-cloud-functions](https://codelabs.developers.google.com/codelabs/firebase-cloud-functions/#0)
- [Navidades con Firebase](https://www.youtube.com/watch?v=hgEl7g_tMgk&list=PLUdlARNXMVkmmBGGnr1ky-RQJ65XW6BE4)
- [Lecciones sobre Cloud Functions (serie de videos)](https://firebase.google.com/docs/functions/video-series?hl=es-419)
- [Referencia de la API](https://firebase.google.com/docs/reference/functions/?hl=es-419)



### Resumen Rápido: Realtime Database

![realtime](https://cdn-images-1.medium.com/max/1200/1*qmvFg6ILS7Y8WsUxa2vLOw.gif)

[Todas las funcionalidades](https://firebase.google.com/docs/database/web/start)

**[Configurando las reglas de lectura/escritura](https://firebase.google.com/docs/database/security/quickstart#sample-rules)**

**¿Cómo se estructuran los datos?**

La base de datos es un simple JSON

```json
{
  "users": {
    "alovelace": {
      "name": "Ada Lovelace",
      "contacts": { "ghopper": true },
    },
    "ghopper": { ... },
    "eclarke": { ... }
  }
}
```

**Lectura/escritura de datos**

```javascript
var userRef = firebase.database().ref(`users/${userId}`);

// LEscuchar cambios en `users/${userId}`
userRef.on('value', (snapshot) => {
  console.log(snapshot.val());
});

// Escuchar una única vez cambios en `users/${userId}`
userRef.once('value', (snapshot) => {
  console.log(snapshot.val());
});

// Almacenar datos en `users/${userId}`
userRef.set({
  username: name,
  email: email,
  profile_picture : imageUrl
});
```

**Actualizando varios datos simultáneamente**

```javascript
var updates = {
    'timestamp': new Date().getTime()
};

updates[`users/${userId}`] = {
  username: name,
  email: email,
  profile_picture : imageUrl
};

firebase.database().ref().update(updates);
```

**¿Cómo borrar datos?**

Las referencias tienen una función `remove()`.

**¿Cómo saber si se ha actualizado un dato?**

Las funciones `set` y `update` devuelven promesas.

**¿Cómo quitar un listener o una referencia?**

Las referencias tienen una función `off(listener)`.
Si no se le pasa ningún parámetro elimina todos los listeners.

**"Arrays" -> Listas**

```javascript
var userRef = firebase.database().ref(`users`);

// Almacenar datos en `users` (genera una clave aleatoria)
userRef.push({
  username: name,
  email: email,
  profile_picture : imageUrl
});
```

**Escuchar cambios en las listas**

```javascript
var userRef = firebase.database().ref(`users`);

// Cuando se añade un elemento
userRef.on('child_added', (snapshot) => { /* ... */ });

// Cuando cambia un elemento
userRef.on('child_changed', (snapshot) => { /* ... */ });

// Cuando se elimina un elemento
userRef.on('child_removed', (snapshot) => { /* ... */ });
```

**Recuperar todos los elementos de una lista**

```javascript
var userRef = firebase.database().ref(`users`);

// Cuando se añade un elemento
userRef.on('value', (snapshot) => {
    snapshot.forEach((childSnapshot) => {
        const element = childSnapshot.val();
    });
});
```

**Ordenar una lista**

```javascript
const ref = firebase.database().ref(`users`);

// Ordena por el valor de una clave
ref.orderByChild('name');
ref.orderByChild('location/latitude');

// Ordena por el nombre de la clave
ref.orderByKey();

// Ordena por el valor de cada elemento
ref.orderByValue();
```

**Filtrar una lista**

```javascript
const ref = firebase.database().ref(`users`);

// Limita el número de elementos de la lista desde el inicio hasta la cantidad de elementos indicada
ref.limitToFirst(10);

// Limita el número de elementos de la lista desde el final hasta la cantidad de elementos indicada
ref.limitToLast(5);

// Elementos mayores o iguales al valor indicado
ref.startAt(70);

// Elementos menores o iguales al valor indicado
ref.endAt();

// Elementos iguales al valor indicado
ref.equalTo();
```

**Trabajar Offline**

- [Documentación](https://firebase.google.com/docs/database/web/offline-capabilities)

```javascript
var connectedRef = firebase.database().ref('.info/connected');

connectedRef.on('value', (snap) => {
  if (snap.val() === true) {
    alert('connected');
  } else {
    alert('not connected');
  }
});
```

**Hosting**

1. Instalar cli

  ```bash
  $ npm install -g firebase-tools
  ```

2. Inicializar aplicación:

  ```bash
  $ firebase init
  ```

3. Desplegar

  ```bash
  $ firebase deploy
  ```

### Ejemplos

- [Social Login](http://jsfiddle.net/firebase/a221m6pb/embedded/result,js,css/)
- [Código Fuente demo de Velocidad](https://github.com/UlisesGascon/raspberrypi-system-info-data-to-firebase)
- [Curratelo](https://github.com/UlisesGascon/curratelo)
- [Raspberrypi system info data to Firebase](https://github.com/UlisesGascon/raspberrypi-system-info-data-to-firebase)
- [Calidad del Aire con Firebase](https://github.com/UlisesGascon/Calidad-del-Aire-con-Firebase)
- [Agroduino](https://github.com/UlisesGascon/Agroduino)
- [Aire Madrid](https://github.com/UlisesGascon/Aire-Madrid)
- [EMT Bus Live](https://github.com/Borjagodoy/emtBusLive)
- [Bitcoin price ticker with Arduino](https://github.com/UlisesGascon/Bitcoin-price-ticker-with-Arduino)
- [MovieFire con Nodejs](https://github.com/UlisesGascon/Simple-API-REST-with-Firebase-and-IMBD)

### Ejercicios

**1 -** Crearemos una aplciación usando Firebase y Express para gestionar las peliculas que nos gustan.
- Objetivos:
    - Crear un APIRest para poder gestionar la aplicación desde otros dominios
    - Habilita CORS para la API
    - Utiliza JADE para gestionar las vistas de tu aplicación
    - Crea módulos para gestionar las rutas
    - Enriquece los datos facilitados por el usuario con la [API de OMBD](http://omdbapi.com/)
    - Guardate una copia de las portadas de las peliculas y sirvelas en la carpeta de los archivos estáticos para evitar el error 403 de IMBD

```javascript
  // Tu solución
```