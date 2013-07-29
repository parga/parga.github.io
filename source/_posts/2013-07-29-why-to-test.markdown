---
layout: post
title: "Why to create unit test"
date: 2013-07-29 09:55
comments: true
published: false
categories:
- Test
---


&nbsp;Es comun que al estar programando con concentremos mas en crear el codigo y que simplemente "funcione", dejamos a un lado todo tipo de analisis previo a la implementacion olvidando generar un orden para atacar ese codigo, no es simplemente decir __"manos a la obra"__. Esto se acentua mas cuando trabajas en un equipo,debido a que la implementacion no siempre esta aislada y puede ser afectada y afectar otros modulos en los cuales nuestro equipo este trabajando, antes de comenzar a generar codigo recomendaria satisfacer estos puntos

1. __Crear casos de uso__
2. __Analizar dependencias__
3. __Definir la implementacion__
4. __Crear pruebas para satisfacer los casos de uso__

---
### Definir casos de uso

&nbsp;Estos son los alementos a atacar, o que es lo que nunca debemos perder de foco cuando estamos haciendo nuestra implementacion, son los requerimientos del cliente, podemos crear una lista de los elementos que son importantes y generar un jerarquia, la cual nos ayudara a definir cuales son los elementos escenciales y cuales son agregados no indispensables.

### Analizar dependencias

&nbsp;Esto nos ayudara a poder tener un contexto de los elementos con los cuales tendra que interacturar el componente, revelara preguntas que al recibir el requerimiento no se nos ocurrieron o descubrira elementos implicitos de la aplicacion que tendran que volverse a discutir dado que tendran que cambiar.


### Definir implementacion

&nbsp;Una vez que ya sabemos en que contexto se va a estar trabajando, ahora tenemos que definir como lo vamos a querer solucionar, este paso puede ser retroalimentado conforme se avance en la implementacion , pero siempre es bueno tener una idea general de como se va a crear, hacerte preguntas como ... ¿quiero que sea un modulo o es parte de una vista (MVC)?, ¿que parametros tengo para inicializarlo?.

### Crear pruebas unitarias

&nbsp;Esta es la parte donde se uniran los 3 elementos anteriores ya que las pruebas deben satisfacer los casos de uso que es al final realmente lo que tiene que resolver el codigo qeu generemos, verificaras que realmente la implementacion del producto genere los elementos que esperabas, y verificaras si el codigo tiene los elementos en su contexto para poder funcionar y si se integrara adecuadamente con los elementos con los cuales va a interactuar para esto tenemos 2 tipos de pruebas:

+ __Pruebas unitarias__
+ __Pruebas de integracion__

###Pruebas Unitarias

&nbsp;Las pruebas unitarias se enfocan principalmente en que el comportamiento de cada funcion interna se el adecuado y cumpla con los requerimientos establecidos en tu implementacion, hay que recordar que en ellas se debe verificar el funcionamiento de cada funcion de manera aislada, no se debe confundir como parte de la prueba que funciones ajenas a ella se ejecuten adecuadamente, estas pruebas nos ayudaran a saber si los cambios que generamos en nuestro modulo afectan a el mismo o el orden en la ejecucion de otras dependencias. Tambien nos pueden ayudar a darnos cuenta si nuestro codigo tiene erorres de diseño, si estamos dejando funciones sin desacoplar tomemos por ejemplo este bloque sencillo de codigo

{% codeblock user_acounts.js %}
	var users_acouts = {

		users_names: [],

		get_user_info: function (user_id){
			$.get({
				url:'/foo/users/' + id,
				success: this.on_users_fetched
			});
		},

		on_users_fetched: function (users){
			_.each(users, function (user){
				this.users_names.push(user.id);
			}, this);
		}
	};
{% endcodeblock %}


La function _on_users_fetched_ aun que es utilizada por _get_user_info_ se debe checar de manera aislada, independeintemente de donde se obtengan los usuarios esta debe de colocar los nombres de los usuarios que recibe en el array de nombres de usuarios