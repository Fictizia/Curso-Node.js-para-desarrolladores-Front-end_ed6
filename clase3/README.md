
# Clase 3

### ECMA6

- **Soporte**
	- [Compatibilidad de kangax](https://kangax.github.io/compat-table/es6/)

- **Compiladores y transpiladores**
	- [Babel - web](https://babeljs.io/)
	- [Babel - Github](https://babeljs.io/repl/)
	- [Lebab by David Walsh](https://davidwalsh.name/lebab)
	- [lebab - web](https://lebab.io/try-it)
	- [Lebab - Github](https://github.com/lebab/lebab)

- **Recursos**
	- [Pensar asíncronamente en un mundo síncrono](https://medium.com/@ulisesGascon/pensar-as%C3%ADncronamente-en-un-mundo-s%C3%ADncrono-8e25cfcafd83)
	- [ECMAScript 6 Features - jsfeatures.in](https://jsfeatures.in/ES6)
	- [ECMAScript 6 Features by Luke Hoban](https://github.com/lukehoban/es6features#readme)
	- [Learn ES2015 - A detailed overview of ECMAScript 6 features by Babel team](https://babeljs.io/docs/learn-es2015/)
	- [ECMAScript 6 Cheatsheet by Erik Moeller](http://help.wtf/es6)
	- [First Steps with ECMAScript 6 by Axel Rauschmayer](http://exploringjs.com/es6/ch_first-steps.html)
	- [JS Features by Hemanth.HM](http://jsfeatures.in/)
	- [Minimalist examples of ES6 functionalities by Hemanth.HM](https://github.com/hemanth/paws-on-es6)
	- [Understanding ECMAScript 6 by Nicholas C. Zakas](https://leanpub.com/understandinges6/read/)
	- [ES6 Overview in 350 Bullet Points by Ponyfoo](https://ponyfoo.com/articles/es6)
	- [Promise visualization playground for the adventurous](https://bevacqua.github.io/promisees/)
	- [ECMAScript 6 equivalents in ES5 by Addi Osmani](https://github.com/addyosmani/es6-equivalents-in-es5)


**[Principales cambios](http://es6-features.org/)**

- Constantes (cons):
```javascript
	const PI = 3.141593
  
  PI = 3.1; // Uncaught TypeError: Assignment to constant variable.
  
  const objeto = {
    usuario: "yo mismo",
    role: "profe"
  }
  
  objeto.role = "estudiante" // Propiedades no protegidas al cambio
  objeto.nuevo = "" // Se peuden crear nuevas propiedades
  objeto = "" // Uncaught TypeError: Assignment to constant variable. 
  
```

- Scoping:
	- Variables Internas (let):
	```javascript
		for (let i = 0; i < a.length; i++) {
	    let = a[i];
	    //...
		}

		/* ECMA5
		for (var i = 0; i < a.length; i++) {
	    var = a[i];
	    //...
		}
		*/
    
    
    var uno = 1;
    let dos = 2;
    if( uno === 1 ){
      var uno = 10;
      let dos = 20;
      console.log(uno); // 10
      console.log(dos); // 20
    }
    console.log(uno); // 10
    console.log(dos); // 2
    
	```
	- Funciones Internas:
	```javascript
		{
		    function nivel1 () { return 1 }
		    nivel1 ();
		    {
		        function nivel2() { return 2 }
		        nivel2 ();
		    }
		}

		/* ECMA5
		(function () {
		    var nivel1 = function () { return 1; }
		    nivel1();
		    (function () {
		        var nivel2 = function () { return 2; };
		        nivel2();
		    })();
		})();
		*/
	```

- Arrow Functions:
	- No pueden usarse con *yield*
	- No pueden ser usadas como constructores
	```javascript
	var Foo = () => {};
	var foo = new Foo(); // TypeError: Foo is not a constructor
	```
	- No tienen una propiedad de prototipo prototype
	```javascript
	var Foo = () => {};
	console.log(Foo.prototype); // undefined
	```
	- No pueden tener saltos de línea
	```javascript
	var func = ()
           => 1; 
	// SyntaxError: expected expression, got '=>'
	```
	- Retorno de objetos literales
	```javascript
	var func = () => {  foo: 1  };               
	// Al llamar func() retorna undefined!
	
	var func = () => {  foo: function() {}  };   
	// Error de sintaxis: SyntaxError: function statement requires a name
	
	// Funciona correctamente
	var func = () => ({ foo: 1 });
	```
	- Orden de parseo
	```javascript
	let callback;

	callback = callback || function() {}; // ok
	
	callback = callback || () => {};      
	// SyntaxError: invalid arrow-function arguments
	
	callback = callback || (() => {});    // ok
	```
	- Siempre son anónimas:
	```javascript
		impares  = numeros.map(v => v + 1);
		pares = evens.map(v => ({ even: v, odd: v + 1 }))
		otrosNumeros  = evens.map((v, i) => v + i)

		/* ECMA5
		impares  = numeros.map(function (v) { return v + 1; });
		pares = evens.map(function (v) { return { even: v, odd: v + 1 }; });
		otrosNumeros  = numeros.map(function (v, i) { return v + i; });
		*/

	```
	- *return* implicito en declaración inline
	```javascript
		var odds = [1,2,3,4,5].filter(num => num % 2);
		console.log(odds); // Array [ 1, 3, 5 ]
	```
	- *return* con cuerpo de bloque
	```javascript
	var func = x => x * x;                  
	// sintaxis de cuerpo conciso, el "return" está implícito
	
	var func = (x, y) => { return x + y; }; 
	// con cuerpo de bloque, se necesita "return" explícito
	```
	- *this* contextual:
	```javascript
	this.nums.forEach((v) => {
	    if (v % 5 === 0)
	        this.fives.push(v)
	})

	/* ECMA 5
	var self = this;
	this.nums.forEach(function (v) {
	    if (v % 5 === 0)
	        self.fives.push(v);
	});
	*/
	```
	- Las Arrow functions no exponen un objeto arguments 
	```javascript
	var arguments = 42;
	var arr = () => arguments;
	
	arr(); // 42
	
	function foo() {
	  var f = () => arguments[0]; // Referencia al objeto arguments
	  return f(2);
	}
	
	foo(1); // 1
	```
	- El parámetro rest es la mejor alternativa
	```javascript
	function foo() { 
	  var f = (...args) => args[0]; 
	  return f(2); 
	}
	
	foo(1); // 2
	```
	- Arrow functions usadas como métodos
	```javascript
	var obj = {
	  i: 10,
	  b: () => console.log(this.i, this),
	  c: function() {
	    console.log(this.i, this);
	  }
	}
	obj.b(); // prints undefined, Window {...} (or the global object)
	obj.c(); // prints 10, Object {...}
	```
	```javascript
	var obj = {
	  a: 10
	};
	
	Object.defineProperty(obj, 'b', {
	  get: () => {
	    console.log(this.a, typeof this.a, this);
	    return this.a + 10; // represents global object 'Window', therefore 'this.a' returns 'undefined'
	  }
	});
	```
	- Invocación a través de los métodos call y apply
	```javascript
	var adder = {
	  base : 1,
	    
	  add : function(a) {
	    var f = v => v + this.base;
	    return f(a);
	  },
	
	  addThruCall: function(a) {
	    var f = v => v + this.base;
	    var b = {
	      base : 2
	    };
	            
	    return f.call(b, a);
	  }
	};
	
	console.log(adder.add(1));         // Imprime 2 como es esperado
	console.log(adder.addThruCall(1)); // También imprime 2 aunque se esperaba 3
	```
	- Sintaxis básica
	```javascript
	(param1, param2, paramN) => {declaraciones} 
	(param1, param2, paramN) =>expresion
	// Equivalente a: () => { return expresion; } 
	
	// Los paréntesis son opcionales cuando sólo dispone de un argumento: singleParam => { statements } 
	singleParam => expresion 
	
	// Una función sin argumentos requiere paréntesis: 
	() => { declaraciones }
	```
	- Sintaxis Avanzada
	```javascript
	// Incluir entre paréntesis el cuerpo para retornar un objeto literal:
	params => ({foo: bar})
	
	// Soporta parámetros rest y parámetros por default
	(param1, param2, ...rest) => { statements }
	(param1 = valorPredef1, param2, ..., paramN = valorPredefN) => { statements }
	
	// Destructuración mediante la lista de parámetros también es soportada
	var f = ([a, b] = [1, 2], {x: c} = {x: a + b}) => a + b + c; f(); // 6
	```

- Gestión de Parámetros en funciones:
	- Parametros opcionales:
	```javascript
		function f (x, y = 7, z = 42) {
		    return x + y + z
		}

		/* ECMA5
		function f (x, y, z) {
		    if (y === undefined){
				y = 7;
			}
		    z = z || 42;
		    return x + y + z;
		};
		*/
	```
	- Parametros adicionales:
	```javascript
		function f (x, y, ...a) {
		    return (x + y) * a.length
		}

		/* ECMA5
		function f (x, y) {
		    var a = Array.prototype.slice.call(arguments, 2);
		    return (x + y) * a.length;
		};
		*/
	```

- Las plantillas de cadena de texto:
	- Concepto:
	```javascript
		`cadena de texto ${expresión} texto`
	```
	- Multiples líneas:
	```javascript
		console.log(`línea 1 de texto
		línea 2 de texto`);

		/* ECMA5
		console.log("línea 1 de texto\nlínea 2 de texto");
		*/
	```
	- Expresiones:
	```javascript
		var customer = { name: "Foo" }
		var card = { amount: 7, product: "Bar", unitprice: 42 }
		message = `Hello ${customer.name},
		want to buy ${card.amount} ${card.product} for
		a total of ${card.amount * card.unitprice} bucks?`

		/* ECMA5
		var customer = { name: "Foo" };
		var card = { amount: 7, product: "Bar", unitprice: 42 };
		message = "Hello " + customer.name + ",\n" +
		"want to buy " + card.amount + " " + card.product + " for\n" +
		"a total of " + (card.amount * card.unitprice) + " bucks?";
		*/
	```
- Mejoras en Objetos (propiedades y métodos):
	- Acortador de propiedades
	```javascript
	let obj = { x, y }
	
	/* ECMA5
	var obj = { x: x, y: y };
	*/
	```
	- Definición de propiedades computerizadas:
	```javascript
		obj = {
		    foo: "bar",
		    [ "prop_" + foo() ]: 42
		}

		/* ECMA5
		obj = {
		    foo: "bar"
		};
		obj[ "prop_" + foo() ] = 42;
		*/
	```
	- Métodos:
	```javascript
		obj = {
		    foo (a, b) {
		        …
		    },
		    bar (x, y) {
		        …
		    },
		    // Generador
		    *quux (x, y) {
		        …
		    }
		}

		/* ECMA5
		obj = {
		    foo: function (a, b) {
		        …
		    },
		    bar: function (x, y) {
		        …
		    },
		    //  quux: no equivalent in ES5
		    …
		};
		*/
	```
- Parsear Binarios y Octales:
```javascript
	0b111110111 === 503
	0o767 === 503

	/* ECMA 5
	parseInt("111110111", 2) === 503;
	parseInt("767", 8) === 503;
	*/
```

- Asignación desestructurada:
	- Objetos:
	```javascript
	//Object Matching, Shorthand Notation & Deep Matching
	var { op: a, lhs: { op: b }, rhs: c } = getASTNode()
	
	//Default Values
	var obj = { a: 1 }
	var { a, b = 2 } = obj
	
	// Parameter Context Matching
	function g ({ name: n, val: v }) {
    	console.log(n, v)
	}
	function h ({ name, val }) {
	    console.log(name, val)
	}
	g({ name: "foo", val:  7 })
	h({ name: "bar", val: 42 })
	
	/* ECMA5
	//Object Matching, Shorthand Notation & Deep Matching
	var tmp = getASTNode();
	var a = tmp.op;
	var b = tmp.lhs.op;
	var c = tmp.rhs;
	
	//Default Values
	var obj = { a: 1 };
	var a = obj.a;
	var b = obj.b === undefined ? 2 : obj.b;
	
	// Parameter Context Matching
	function g (arg) {
	    var n = arg.name;
	    var v = arg.val;
	    console.log(n, v);
	};
	function h (arg) {
	    var name = arg.name;
	    var val  = arg.val;
	    console.log(name, val);
	
	g({ name: "foo", val:  7 });
	h({ name: "bar", val: 42 });
	*/
	```
	- Arrays:
	```javascript
		// Matching
		var list = [ 1, 2, 3 ]
		var [ a, , b ] = list

		// Parameter Context Matching
		function f ([ name, val ]) {
		    console.log(name, val)
		}

		f([ "bar", 42 ]);

		// Fail-Soft Destructuring
		var list2 = [ 7, 42 ]
		var [ a = 1, b = 2, c = 3, d ] = list2

		/* ECMA5
		// Matching
		var list = [ 1, 2, 3 ];
		var a = list[0], b = list[2];

		// Parameter Context Matching
		function f (arg) {
		    var name = arg[0];
		    var val  = arg[1];
		    console.log(name, val);
		};

		f([ "bar", 42 ]);

		// Fail-Soft Destructuring
		var list2 = [ 7, 42 ];
		var a = typeof list2[0] || 1;
		var b = typeof list2[1] || 2;
		var c = typeof list2[2] !== "undefined" ? list2[2] : 3;
		var d = typeof list2[3] !== "undefined" ? list2[3] : undefined;
		*/
	```
- Nuevos Métodos Integrados:
	- Asignación de propiedades enumerables en objetos:
	```javascript
		var dst  = { quux: 0 }
		var src1 = { foo: 1, bar: 2 }
		var src2 = { foo: 3, baz: 4 }
		Object.assign(dst, src1, src2)

		// Verificación
		dst.quux === 0
		dst.foo  === 3
		dst.bar  === 2
		dst.baz  === 4

		/* ECMA5
		var dst  = { quux: 0 };
		var src1 = { foo: 1, bar: 2 };
		var src2 = { foo: 3, baz: 4 };
		Object.keys(src1).forEach(function(k) {
		    dst[k] = src1[k];
		});
		Object.keys(src2).forEach(function(e) {
		    dst[k] = src2[k];
		});

		// Verificación
		dst.quux === 0;
		dst.foo  === 3;
		dst.bar  === 2;
		dst.baz  === 4;
		*/
	```
	- Repetir
	```javascript
	" ".repeat(4 * depth)
	"foo".repeat(3)
	
	/* ECMA5
	Array((4 * depth) + 1).join(" ");
	Array(3 + 1).join("foo");
	*/
	```
	- Busqueda en sub-cadenas:
	```javascript
		"hello".startsWith("ello", 1) // true
		"hello".endsWith("hell", 4)   // true
		"hello".includes("ell")       // true
		"hello".includes("ell", 1)    // true
		"hello".includes("ell", 2)    // false

		/* ECMA5
		"hello".indexOf("ello") === 1;    // true
		"hello".indexOf("hell") === (4 - "hell".length); // true
		"hello".indexOf("ell") !== -1;    // true
		"hello".indexOf("ell", 1) !== -1; // true
		"hello".indexOf("ell", 2) !== -1; // false
		*/
	```
	- Chequear No-Numericos e infinitos:
	```javascript
		Number.isNaN(42) === false
		Number.isNaN(NaN) === true

		Number.isFinite(Infinity) === false
		Number.isFinite(-Infinity) === false
		Number.isFinite(NaN) === false
		Number.isFinite(123) === true

		/* ECMA5
		var isNaN = function (n) {
		    return n !== n;
		};
		var isFinite = function (v) {
		    return (typeof v === "number" && !isNaN(v) && v !== Infinity && v !== -Infinity);
		};
		isNaN(42) === false;
		isNaN(NaN) === true;

		isFinite(Infinity) === false;
		isFinite(-Infinity) === false;
		isFinite(NaN) === false;
		isFinite(123) === true;
		*/
	```
	- isSafeInteger():
	```javascript
		Number.isSafeInteger(42) === true
		Number.isSafeInteger(9007199254740992) === false

		/* ECMA5
		function isSafeInteger (n) {
		    return (
		           typeof n === 'number'
		        && Math.round(n) === n
		        && -(Math.pow(2, 53) - 1) <= n
		        && n <= (Math.pow(2, 53) - 1)
		    );
		}
		isSafeInteger(42) === true;
		isSafeInteger(9007199254740992) === false;
		*/
	```
	- Truncar Número Flotante:
	```javascript
	console.log(Math.trunc(42.7)) // 42
	console.log(Math.trunc( 0.1)) // 0
	console.log(Math.trunc(-0.1)) // -0

	/* ECMA5
	function mathTrunc (x) {
	    return (x < 0 ? Math.ceil(x) : Math.floor(x));
	}
	console.log(mathTrunc(42.7)) // 42
	console.log(mathTrunc( 0.1)) // 0
	console.log(mathTrunc(-0.1)) // -0
	*/
	```

- For... of (iteración sobre valores y no propiedades):
```javascript
  let arr = [3, 5, 7];
  arr.foo = "hello";

  for (let i in arr) {
     console.log(i);
     // "0", "1", "2", "foo"
  }

  for (let i of arr) {
     console.log(i);
     // "3", "5", "7"
  }

```
- Generadores:
	- [Ejemplo de Miguel Sánchez](http://miguelsr.js.org/2015/06/08/es6-generators.html)
	```javascript
		function* greatGenerator(name) {
		    yield "Hola " + name + "!";
		    yield "Esta línea saldrá en la segunda ejecución";
		    yield "Esta otra, en la tercera";
		    if (name === "Miguel") yield "Esta otra, saldrá en la cuarta solo si te llamas miguel"
		}
		var generatorInstance = greatGenerator("paco");
		console.log(generatorInstance.next().value); // Hola paco!
		console.log(generatorInstance.next().value); // Esta línea saldrá la segunda ejecución
		console.log(generatorInstance.next().value); // Esta otra, en la tercera
		console.log(generatorInstance.next().value); // undefined
	```

- Map:
	- Manejando datos independientes con una estructura clave/valor
	```javascript
		let miMap = new Map();
		let miArray = [];

		miMap.set('cadena', 'Hola!');
		miMap.set(miArray, [500, "hola", true, false]);

		console.log(miMap.get(miArray)); // [500, "hola", true, false]
		console.log(miMap.get('cadena')); // Hola!

		console.log(miMap.size); // 2

		miMap.delete('cadena');

		console.log(miMap.size); // 1
	```
- Set:
	```javascript
	let s = new Set()
	s.add("hello").add("goodbye").add("hello")
	s.size === 2
	s.has("hello") === true
	for (let key of s.values()) // insertion order
	    console.log(key)
	```
- Set vs Map:
	```javascript
	//@see: https://stackoverflow.com/a/24085746
	var array = [1, 2, 3, 3];

	var set = new Set(array); // Will have [1, 2, 3]
	assert(set.size, 3);
	
	var map = new Map();
	map.set('a', 1);
	map.set('b', 2);
	map.set('c', 3);
	map.set('C', 3);
	map.set('a', 4); // Has: a, 4; b, 2; c: 3, C: 3
	assert(map.size, 4);
	```

- Clases:
	- La idea es POO sin prototipos
	- Definición de Clase:
	```javascript
		class coche{
		  constructor(marca, modelo, antiguedad, color, tipo) {
		    this.marca = marca;
		    this.modelo = modelo;
		    this.antiguedad = antiguedad;
		    this.color = color;
		    this.tipo = tipo;
		  }
		  detalles() {
		    console.log(`Tu coche es un ${this.marca} ${this.modelo} con ${this.antiguedad} años, clase ${this.tipo} y color ${this.color}`);
		  }
		}

		let miCoche = new coche ("Seat", "Panda", 20, "azul", "turismo");
		miCoche.detalles();

		/* ECMA 5
		var coche = function (marca, modelo, antiguedad, color, tipo) {
		    // Propiedades
		    this.marca = marca;
		    this.modelo = modelo;
		    this.antiguedad = antiguedad;
		    this.color = color;
		    this.tipo = tipo;
		    // Metodos
		    this.detalles = function(){
		      console.log("Tu coche es un "+this.marca+" "+this.modelo+" con "+this.antiguedad+" años, clase "+this.tipo+" y color "+this.color);
		    }
		};

		var miCoche = new coche ("Seat", "Panda", 20, "azul", "turismo");
		miCoche.detalles();
		*/
	```
	- Extensión de Clase:
	```javascript
		class perro {
		  constructor(nombre) {
		    this.patas = 4;
		    this.ojos = 2;
		    this.nombre = nombre;
		  }

		  ladrar() {
		    console.log(`${this.nombre} esta ladrando!`);
		  };
		}

		class pastorAleman extends perro {
		  constructor(nombre) {
		    super('pastorAleman');
		    this.colorLengua = "negra";
		    this.colorOjos = "marrón";
		    this.capacidadTrabajo = true;
		    this.especialidad = "Pastoreo";
		  }

		  informacion() {
		  	console.log(`Nombre: ${this.nombre}
		  	Número patas: ${this.patas}
		  	Número ojos: ${this.ojos}
		  	Color ojos: ${this.colorOjos}
		  	Color Lengua: ${this.colorLengua}
		  	Capacidad de trabajo: ${this.capacidadTrabajo}
		  	Especialidad: ${this.especialidad}`);
		  }
		}

		let miPerro = new pastorAleman('Golden');
		miPerro.informacion();
		miPerro.ladrar();

		/* ECMA 5
		var perro  = function (nombre) {
		    this.patas = 4;
		    this.ojos = 2;
		    this.nombre = nombre;
		    this.ladrar = function(){
		    	console.log(this.nombre + " esta ladrando!");
		    }
		};

		var pastorAleman = function () {
		    this.colorLengua = "negra";
		    this.colorOjos = "marrón";
		    this.capacidadTrabajo = true;
		    this.especialidad = "Pastoreo";
		    this.informacion = function(){
				console.log("Nombre: "+this.nombre+"\nNúmero patas: "+this.patas+"\nNúmero ojos: "+this.ojos+"\nColor Lengua: "+this.colorLengua+"\nColor ojos: "+this.colorOjos+"\nCapacidad de trabajo: "+this.capacidadTrabajo+"\nEspecialidad: "+this.especialidad);
		    }
		};

		pastorAleman.prototype = new perro("Golden");

		var miPerro = new pastorAleman();
		miPerro.informacion();
		miPerro.ladrar();
		*/
	```
	- Métodos Estáticos:
	```javascript
		class coche{
		  static info (edad){
		  	console.info(`Tienes ${edad} años ${ edad >= 18 ? "y puedes conduccir": "y ... ¡Sorpresa! No puedes conduccir."}`);
		  }
		  constructor(marca, modelo, antiguedad, color, tipo) {
		    this.marca = marca;
		    this.modelo = modelo;
		    this.antiguedad = antiguedad;
		    this.color = color;
		    this.tipo = tipo;
		  }
		  detalles() {
		    console.log(`Tu coche es un ${this.marca} ${this.modelo} con ${this.antiguedad} años, clase ${this.tipo} y color ${this.color}`);
		  }
		}

		coche.info(50);
		coche.info(8);
		let miCoche = new coche ("Seat", "Panda", 20, "azul", "turismo");
		miCoche.detalles();
	```
	- Getter/Setter
	```javascript
	class Rectangle {
	    constructor (width, height) {
	        this._width  = width
	        this._height = height
	    }
	    set width  (width)  { this._width = width               }
	    get width  ()       { return this._width                }
	    set height (height) { this._height = height             }
	    get height ()       { return this._height               }
	    get area   ()       { return this._width * this._height }
	}
	var r = new Rectangle(50, 20)
	r.area === 1000
	
	/* ECMA5
	var Rectangle = function (width, height) {
	    this._width  = width;
	    this._height = height;
	};
	Rectangle.prototype = {
	    set width  (width)  { this._width = width;               },
	    get width  ()       { return this._width;                },
	    set height (height) { this._height = height;             },
	    get height ()       { return this._height;               },
	    get area   ()       { return this._width * this._height; }
	};
	var r = new Rectangle(50, 20);
	r.area === 1000;
	*/
	```
- Módulos (Exportación):
	- Único
	```javascript
		// config.js
		let config = {
			token: "secreto",
		}

		export default config;
	```
	- Mutiples
	```javascript
		// config.js
		let config = {
			token: "secreto",
		}

		let config_details = {
			detalles: "más datos"
		}

		export config;
		export config_details;
	```
	- Combinada
	```javascript
		// config.js
		let config = {
			token: "secreto",
		}

		let config_details = {
			detalles: "más datos"
		}

		let configuraciones = {config, config_details}

		export default configuraciones;
		export config;
		export config_details;
	```
- Módulos (Importación):
	- Síncrona
	```javascript
		// único
		import config from './config.js';

		// Multiples
		import * as config from './config.js';

		// Combinandos
		import configuraciones from './config.js';
		import { config, config_details } from './config.js';
	```
	- Asíncrona (solo un módulo)
	```javascript
		System.import('modulo')

	    .then(modulo => {
	        // Uso del módulo importado
	    })
	    .catch(error => {
	        // Gestión de errores
	    });
	```
	- Asíncrona (multiples módulos)
	```javascript
	    Promise.all(
	        ['module1', 'module2', 'module3']
	        .map(x => System.import(x)))
	    .then(([module1, module2, module3]) => {
	        // Use module1, module2, module3
	    });
	```
- Módulos (Comparativa):
	- Export/Import
	```javascript
	//  lib/math.js
	export function sum (x, y) { return x + y }
	export var pi = 3.141593
	
	//  someApp.js
	import * as math from "lib/math"
	console.log("2π = " + math.sum(math.pi, math.pi))
	
	//  otherApp.js
	import { sum, pi } from "lib/math"
	console.log("2π = " + sum(pi, pi))

	/* ECMA5
	//  lib/math.js
	LibMath = {};
	LibMath.sum = function (x, y) { return x + y };
	LibMath.pi = 3.141593;
	
	//  someApp.js
	var math = LibMath;
	console.log("2π = " + math.sum(math.pi, math.pi));
	
	//  otherApp.js
	var sum = LibMath.sum, pi = LibMath.pi;
	console.log("2π = " + sum(pi, pi));
	
	*/
	```
	- Default & Wildcard
	```javascript
	//  lib/mathplusplus.js
	export * from "lib/math"
	export var e = 2.71828182846
	export default (x) => Math.exp(x)
	
	//  someApp.js
	import exp, { pi, e } from "lib/mathplusplus"
	console.log("e^{π} = " + exp(pi))
	
	/* ECMA5
	//  lib/mathplusplus.js
	LibMathPP = {};
	for (symbol in LibMath)
	    if (LibMath.hasOwnProperty(symbol))
	        LibMathPP[symbol] = LibMath[symbol];
	LibMathPP.e = 2.71828182846;
	LibMathPP.exp = function (x) { return Math.exp(x) };
	
	//  someApp.js
	var exp = LibMathPP.exp, pi = LibMathPP.pi, e = LibMathPP.e;
	console.log("e^{π} = " + exp(pi));
	*/
	```

- Promesas
![promises_ecma6](https://mdn.mozillademos.org/files/8633/promises.png)
> A promise represents the eventual result of an asynchronous operation. The primary way of interacting with a promise is through its *then* method, which registers callbacks to receive either a promise’s eventual value or the reason why the promise cannot be fulfilled.
> From [promisesaplus.com/](http://promisesaplus.com/)

- Estados:
    - Fulfilled – La acción en relación con la promesa se logró.
    - Rejected – La acción en relación con la promesa falló.
    - Pending – Pendiente, no se ha cumplido o rechazado aún.
    - Settled - Arreglada, se ha cumplido o se ha rechazado (resuelta).

- En ECMA6:
- [Soporte en navegadores](http://caniuse.com/#search=promise)  
    - Una promesa
    ```javascript
        var cuentaPromesas = 0;
        var errorMode = false;
        function testPromesa() {

          var numPromesaActual = ++cuentaPromesas;

          console.warn("Promesa Asíncrona numero ("+numPromesaActual+") - Iniciada")

          var miPromesa = new Promise(
            function(resolve, reject) {       

              console.info("Promesa Asíncrona numero ("+numPromesaActual+") - Proceso asincrónico empezado");

              if(errorMode){
                  reject(numPromesaActual)
              } else{
                window.setTimeout(
                  function() {
                    resolve(numPromesaActual)
                  }, Math.random() * 2000 + 1000);
              }
            });
          miPromesa.then(
            function(val) {
              console.info("Promesa Asíncrona numero ("+val+") - Proceso asincrónico terminado");
              console.warn("Promesa Asíncrona numero ("+numPromesaActual+") - Finalizada");
            }).catch(
              function(val){
                console.error("Promesa Asíncrona numero ("+val+") - ERROR FATAL");
            });
        };

        testPromesa();
    ```
- [Internationalization & Localization](http://kangax.github.io/compat-table/esintl/
)



### Implementados

#### [Array.prototype.includes](http://2ality.com/2016/02/array-prototype-includes.html)
- Retorna un booleno si encuentra el elemento. Tiene muchas mejoras respecto `Array.prototype.indexOf`
- Propuesto por Domenic Denicola y Rick Waldron
- [ECMA documentation](http://www.ecma-international.org/ecma-262/7.0/index.html#sec-array.prototype.includes)

```javascript
['a', 'b', 'c'].includes('a') // true
['a', 'b', 'c'].includes('d') // false

// similitud con indexOf:
// arr.includes(x) -> arr.indexOf(x) >= 0

[NaN].includes(NaN) // true
[NaN].indexOf(NaN) // -1

// @see: http://speakingjs.com/es5/ch11.html#two_zeros
[-0].includes(+0) // true

// Arrays tipados también lo incluyen
let arrTip = Uint8Array.of(12, 5, 3);
console.log(arrTip.includes(5)); // true
```


#### [Exponentiation Operator](http://2ality.com/2016/02/exponentiation-operator.html)
- Añade el operador exponencial `x ** y`, su comportamiento es igual que `Math.pow(x, y)`
- Propuesto por Rick Waldron, Claude Pache y Brendan Eich
- [ECMA documentation](http://www.ecma-international.org/ecma-262/7.0/index.html#sec-exp-operator)

```javascript
let cuadrado = 3 ** 2; // 9
let numero = 3;
numero **= 2; // 9
```

## ES2017 (ES8)

### Recursos
- [Async Functions for ECMAScript](https://github.com/tc39/ecmascript-asyncawait)
- [Simplifying asynchronous computations via generators (section in “Exploring ES6”)](http://exploringjs.com/es6/ch_generators.html#sec_co-library)
- [ES proposal: async functions](http://2ality.com/2016/02/async-functions.html)
- [Compatibilidad 2016+](http://kangax.github.io/compat-table/esnext/)
- [Axel Rauschmayer blog | ES2017](http://2ality.com/2016/02/ecmascript-2017.html)
- [Shared memory and atomics for ECMAscript](https://github.com/tc39/ecmascript_sharedmem)
- [ES8, el estándar Javascript de 2017 de Enrique Oriol](http://blog.enriqueoriol.com/2017/07/es8-estandar-javascript-2017.html)

### Implementados cambios principales

#### [Async Functions](http://2ality.com/2016/02/async-functions.html)
Propuesto por Brian Terlson


**Código asíncrono utilizando promesas y generadores**
- Nativo

```javascript
function fetchJson(url) {
    return fetch(url)
    .then(request => request.text())
    .then(text => {
        return JSON.parse(text);
    })
    .catch(error => {
        console.log(`ERROR: ${error.stack}`);
    });
}
fetchJson('http://example.com/some_file.json')
.then(obj => console.log(obj));
```

- Funciones Asíncronas

```javascript
async function getGithubUser(username) {
  const url = `https://api.github.com/users/${username}`;
  const response = await fetch(url);
  const json = await response.json();
 
  return json;
}

// Forma asíncrona
(async function() {
  const userData = await getGithubUser('ulisesGascon');
  console.log(userData); // { "login": "UlisesGascon", "id": 5110813, ... }
})();

// Utilizando promesas
getGithubUser('ulisesGascon').then((userData) => {
  console.log(userData); // { "login": "UlisesGascon", "id": 5110813, ... }
})
```

- Variantes

```javascript
// Declaración
async function foo() {}

// Expresión
const foo = async function () {};

// Método
let obj = { async foo() {} }

// Formato Arrow Function
const foo = async () => {};
```


### Implementados cambios menores

#### [Object.values/Object.entries](http://2ality.com/2015/11/stage3-object-entries.html)
- Retornan un array o una matriz con los valores o las propiedades iterables de los objetos
- Propuesto por Jordan Harband

**Objetos**
```javascript
const data = { elemnto: 'primero', otro_dato: 1 };
Object.values(data); // ["primero", 1]
Object.entries(data); // [["elemnto", "primero"], ["otro_dato", 1]]
```

**Arrays**
```javascript
const obj = ['p1', 'p2', 'p3']; // equivale a { 0: 'a', 1: 'z', 2: '5' };
Object.values(obj); // ["p1", "p2", "p3"]
Object.entries(obj); // [["0", "p1"], ["1", "p2"], ["2", "p3"]]
```

**Cadenas**
```javascript
Object.values('Fictizia'); // ["F", "i", "c", "t", "i"]
Object.entries('Ficti'); // [["0", "F"], ["1", "i"], ["2", "c"], ["3", "t"], ["4", "i"]]
```


#### [String padding](http://2ality.com/2015/11/string-padding.html)
- Se rellena una cadena por delante con `padStart` o por detras con `padEnd`, puedes especificar el relleno
- Propuesto por Jordan Harband y Rick Waldron

```javascript
// .padStart()
'data'.padStart(1);          // "data"
'data'.padStart(7);          // "   data"
'data'.padStart(6, '-');     // "--data"
'data'.padStart(10, 'info'); // "infoindata"
'data'.padStart(5, '*');     // "*data"

// .padEnd()
'data'.padEnd(1);          // "data"
'data'.padEnd(7);          // "data   "
'data'.padEnd(6, '-');     // "data--"
'data'.padEnd(10, 'info'); // "datainfoin"
'data'.padEnd(5, '*');     // "data*"
```

#### [Trailing commas in function parameter lists and calls](http://2ality.com/2015/11/trailing-comma-parameters.html)
- Se ignorarán las comas extras al final del último parámetro de una función
- Propuesto por Jeff Morrison

```javascript
//En declaración
function foo(p1, p2, p3,) { 
    //... 
}

//En ejecución
foo("a", "b", "b",);
```



### Trabajando con APIs

> Una API representa la capacidad de comunicación entre componentes de software.

**CRUD**

![CRUD](http://radzserg.com/wp-content/uploads/2016/04/mongodb-crud-operations1.png)

- Create (POST):
  - Respuesta 200 - OK
  - Respuesta 204 - Sin contenido
  - Respuesta 404 - No encontrado
  - Respuesta 409 - Conflicto, ya existe
- Read (GET):
  - Respuesta 200 - OK
  - Respuesta 404 - No encontrado
- Update (PUT):
  - Respuesta 200 - OK
  - Respuesta 204 - Sin contenido
  - Respuesta 404 - No encontrado
- Delete (DELETE):
  - Respuesta 200 - OK
  - Respuesta 404 - No encontrado


![HTTP Protocolo](http://fundamentos-redes.wikispaces.com/file/view/3.3.2_Servicio_WWW_y_HTTP.jpg/255291246/960x432/3.3.2_Servicio_WWW_y_HTTP.jpg)


**Códigos de respuesta HTTP**:

- 1xx Informativas
- 2xx Peticiones Correctas
- 3xx Redirecciones
- 4xx Errores Cliente
- 5xx Errores Servidor


[Lista de respuestas HTTP](https://es.wikipedia.org/wiki/Anexo:C%C3%B3digos_de_estado_HTTP)

[Especificación](https://tools.ietf.org/html/rfc2616#section-10)

**Ejemplos**:
- [API RTVE](https://github.com/UlisesGascon/RTVE-API)
- [API Github](https://developer.github.com/v3/)


### AJAX

> Asynchronous JavaScript And XML, es una técnica de desarrollo web para crear aplicaciones interactivas.

![Ajax comparación](http://gemsres.com/story/feb07/338111/fig1.jpg)

**Con Jquery**

```javascript
function peticionJqueryAjax (url) {
  $.ajax({
    dataType: "json",
    url,
  }).done((data, textStatus, jqXHR) => {
    console.log('La solicitud se ha completado correctamente.');
    console.log( data );
  }).fail((jqXHR, textStatus, errorThrown) => {
    console.log(`La solicitud a fallado: ${textStatus}`);
  });
}
  
peticionAjax('https://api.github.com/users/josex2r')
```

**Vanilla JS** (`XMLHttpRequest`)

- *readyState*:
  - 0 es *uninitialized*
  - 1 es *loading*
  - 2 es *loaded*
  - 3 es *interactive*
  - 4 es *complete*

```javascript
function peticionAjax(url) {
  const xmlHttp = new XMLHttpRequest();

  xmlHttp.onreadystatechange = function() {

    if (xmlHttp.readyState === 4 && xmlHttp.status === 200) {
      console.info(JSON.parse(xmlHttp.responseText));
    } else if (xmlHttp.readyState === 4 && xmlHttp.status === 404) {
      console.error('ERROR! 404');
      console.info(JSON.parse(xmlHttp.responseText));
    }
  };
  xmlHttp.open('GET', url, true);
  xmlHttp.send();
}

peticionAjax('https://api.github.com/users/josex2r')
```

**Vanilla JS** (`fetch`)

```javascript
function peticionAjax(url) {
  fetch(url)
    .then((response) => response.json())
    .then((json) => {
      console.log(json);
    }, () => {
      console.error('ERROR!!!');
    });
}

peticionAjax('https://api.github.com/users/josex2r')
```

### JSON

- `JSON.parse()`: Analiza la cadena y retorna los valores

- `JSON.stringify()`: Analiza los valores y retorna una cadena 

### JSONP

> JSONP o JSON con padding es una técnica de comunicación utilizada en los programas JavaScript para realizar llamadas asíncronas a dominios diferentes.

El objeto JSON se devuelve envuelto en la llamada de una función. De esta forma, una función ya definida en el entorno de JavaScript podría manipular los datos JSON.

```javascript
jsonCallback({
  api_key: '224Wrf2asfSDfcea23reSDfqW',
  status: 'good',
  name: 'wikipedia',
  date: '27-09-1995'
});
```

Por convención, el nombre de la función de retorno se especifica mediante un parámetro de la consulta, normalmente, utilizando jsonp o callback como nombre del campo en la solicitud al servidor.

```html
<script type="text/javascript" src="http://servidor.ejemplo.com/datos.json?callback=parseJSON"></script>
```

Soporte en cliente (librerías):

- Jquery:

  ```javascript
  // Using YQL and JSONP
  $.ajax({
    url: 'http://query.yahooapis.com/v1/public/yql',
    // The name of the callback parameter, as specified by the YQL service
    jsonp: 'callback',
    // Tell jQuery we're expecting JSONP
    dataType: 'jsonp',
    // Tell YQL what we want and that we want JSON
    data: {
      q: 'select title,abstract,url from search.news where query="cat"',
      format: 'json'
    },
    // Work with the response
    success(response) {
      console.log(response); // server response
    }
  });
  ```
- [jsonp.js de Przemek Sobstel](https://github.com/sobstel/jsonp.js/blob/master/jsonp.js)
- [J50Npi.js de Roberto Decurnex](https://github.com/robertodecurnex/J50Npi/blob/master/J50Npi.js)


### Programación dirigida a eventos

> La programación dirigida por eventos es un paradigma de programación en el que tanto la estructura como la ejecución de los programas van determinados por los sucesos que ocurran en el sistema, definidos por el usuario o que ellos mismos provoquen.

![events](http://2.bp.blogspot.com/_x8Kft4g8fUQ/TQsMSgsWcLI/AAAAAAAAAJM/ph8Hm0yZF18/s1600/000alisten.jpg)

> Para entender la programación dirigida por eventos, podemos oponerla a lo que no es: mientras en la programación secuencial (o estructurada) es el programador el que define cuál va a ser el flujo del programa, en la programación dirigida por eventos será el propio usuario —o lo que sea que esté accionando el programa— el que dirija el flujo del programa. Aunque en la programación secuencial puede haber intervención de un agente externo al programa, estas intervenciones ocurrirán cuando el programador lo haya determinado, y no en cualquier momento como puede ser en el caso de la programación dirigida por eventos. [Wikiwand](https://www.wikiwand.com/es/Programaci%C3%B3n_dirigida_por_eventos)

- **Ejemplo:**

  ```javascript
  function setRandomColor(e) {
    let color = 'rgb(' + Math.floor((Math.random() * 255)) + ',';
    color += Math.floor((Math.random() * 255)) + ',';
    color += Math.floor((Math.random() * 255)) + ')';
    document.body.style.backgroundColor = color;
    console.info("Nuevo color:", color);
  }

  document.addEventListener('click', setRandomColor);
  // document.removeEventListener('click', setRandomColor);
  ```


### Terminal UNIX

- [400 comandos que deberias conocer](http://blog.desdelinux.net/mas-de-400-comandos-para-gnulinux-que-deberias-conocer/)
- [Terminal online](http://www.tutorialspoint.com/unix_terminal_online.php)
- [Webminal](http://www.webminal.org/)
- [C9 - Terminal - Documentación](https://docs.c9.io/docs/terminal)
- **Librerías**
  - [shelljs](https://www.npmjs.com/package/shelljs)
  - [node-cmd](https://www.npmjs.com/package/node-cmd)


### Multipurpose Internet Mail Extensions (MIME)

- **Más usadas:**
  - text/html
  - text/plain
  - text/css
  - image/gif
  - image/x-png
  - image/jpeg
  - application/pdf
  - application/zip
  - text/javascript
  - *[Lista Completa](http://sites.utoronto.ca/webdocs/HTMLdocs/Book/Book-3ed/appb/mimetype.html)*


### Nodejs
![Node_logo](https://nodejs.org/static/images/logos/nodejs.png)

- Versiones:
  - Pares -> Estables
  - Impares -> inestables

- Versiones LTS:

  ![lts_schedule](https://raw.githubusercontent.com/nodejs/LTS/master/schedule.png)
  - [Planes e información](https://github.com/nodejs/LTS)


- Grandes Cambios:
    - [De v0.2 a v0.3](https://github.com/nodejs/node/wiki/Migrating-from-v0.2-to-v0.3)
    - [De v0.3 a v0.4](https://github.com/nodejs/node/wiki/Migrating-from-v0.2-to-v0.4)
    - [De v0.4 a v0.6](https://github.com/nodejs/node/wiki/API-changes-between-v0.4-and-v0.6)
    - [De v0.6 a v0.8](https://github.com/nodejs/node/wiki/API-changes-between-v0.6-and-v0.8)
    - [De v0.8 a v0.10](https://github.com/nodejs/node/wiki/API-changes-between-v0.8-and-v0.10)
    - [De v0.10 a v0.12](https://github.com/nodejs/node/wiki/API-changes-between-v0.10-and-v0.12)
    - [De v0.10 a v4](https://github.com/nodejs/node/wiki/API-changes-between-v0.10-and-v4)
    - [De v4 a v5](https://github.com/nodejs/node/wiki/Breaking-changes-between-v4-and-v5)
    - [De v5 a v6](https://github.com/nodejs/node/wiki/Breaking-changes-between-v5-and-v6)
    - [De v6 a v7](https://github.com/nodejs/node/wiki/Breaking-changes-between-v6-and-v7)
    - [De v4 LTS a v6 LTS](https://github.com/nodejs/node/wiki/Breaking-changes-between-v4-LTS-and-v6-LTS)
    - [io.js](https://github.com/nodejs/node/wiki/Breaking-Changes)


- Comprobar version:
  - Node

    ```
    node -v
    ```


### Hello World

```javascript
console.log("Hola Mundo!");
```


### Librerías Nativas (CORE)

**Los estados**
- `0` *Deprecated*
- `1` *Experimental*
- `2` *Unstable*
- `3` *Stable*
- `4` *API Frozen*
- `5` *Locked*

**Los módulos**
- [Assertion testing](https://nodejs.org/api/assert.html)
- **[Buffer](https://nodejs.org/api/buffer.html)** - *Permite el trabajo con datos binarios*
- [C/C++ Addons](https://nodejs.org/api/addons.html) - *Permite integrar librerias de C/C++*
- **[Child Processes](https://nodejs.org/api/child_process.html)** - *Permite crear y gestionar subprocesos*
- [Cluster](https://nodejs.org/api/cluster.html) - *Permite gestionar nuestro proceso principal e "hijos" entre diversos módulos*
- [Command Line Options](https://nodejs.org/api/cli.html) - *Controla el lanzamiento de Node por Consola*
- [Console](https://nodejs.org/api/console.html) - *Permite trabajar con la consola (terminal), imitando la consola del navegador*
- [Crypto](https://nodejs.org/api/crypto.html) - *Relacionado a las funcionalidades de criptografía necesarias apra algunso protocolos como SSL*
- [Debugger](https://nodejs.org/api/debugger.html) - *Utilidades de depuración*
- [DNS](https://nodejs.org/api/dns.html) - *Gestion y resolución de nombres de Dominios*
- [Domain](https://nodejs.org/api/domain.html) - *DEPRECIADO*
- [Errors](https://nodejs.org/api/errors.html) - *Gestión de errores*
- **[Events](https://nodejs.org/api/events.html)** - *Permite gestionar y crear eventos*
- **[File System](https://nodejs.org/api/fs.html)** - *Permite manipular y crear ficheros en el sistema*
- [Globals](https://nodejs.org/api/globals.html) - *Ámbito global*
- **[HTTP](https://nodejs.org/api/http.html)** - *Gestión del protocolo HTTP*
- **[HTTPS](https://nodejs.org/api/https.html)** - *Gestión del protocolo HTTPS (http y tls/ssl)*
- **[Modules](https://nodejs.org/api/modules.html)** - *Gestión y carga de módulos*
- [Net](https://nodejs.org/api/net.html) - *Nos aporta una capa de red asíncrona y permite gestionar "streams" tanto cliente como servidor.*
- [OS](https://nodejs.org/api/os.html) - *Información básica sobre el sistema operativo en el que estamos funcionando*
- **[Path](https://nodejs.org/api/path.html)** - *Gestión de rutas dentro del sistema (navegación de carpetas y archivos)*
- **[Process](https://nodejs.org/api/process.html)** - *Objeto global que gestiona el proceso del sistema que representa nuestra ejecución de Node*
- [Punycode](https://nodejs.org/api/punycode.html) - *Sintaxís de codificación a RFC 3492 y RFC 5891*
- **[Query Strings](https://nodejs.org/api/querystring.html)** - *Manipualción y gestion de cadenas URL*
- [Readline](https://nodejs.org/api/readline.html) - *Puede leer línea a línea información de entrada como la consola*
- [REPL](https://nodejs.org/api/repl.html) - *Read-Eval-Print-Loop (REPL)*
- **[Stream](https://nodejs.org/api/stream.html)** - *Interfaz abstracta usada por otros módulos para gestionar el flujo de la información*
- **[Timers](https://nodejs.org/api/timers.html)** - *Funciones globales de tiempo como setInterval, clearInterval, etc...*
- [TLS/SSL](https://nodejs.org/api/tls.html) - *Capa de encriptación basada en OpenSSL*
- [UDP/Datagram](https://nodejs.org/api/dgram.html) - *Gestión del protocolo UDP*
- **[URL](https://nodejs.org/api/url.html)** - *Facilita la resolución y parseo de URLs*
- **[Utilities](https://nodejs.org/api/util.html)** - *Utilidades varias, la mayoría depreciadas*
- [V8](https://nodejs.org/api/v8.html) - *Información sobre v8*
- [VM](https://nodejs.org/api/vm.html) - *Permite aislar código en "sandboxes"*
- [ZLIB](https://nodejs.org/api/zlib.html) - *Permite trabajar con Gzip/Gunzip, Deflate/Inflate y DeflateRaw/InflateRaw*


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