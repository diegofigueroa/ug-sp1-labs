---
layout: post
title:  "Laboratorio #4"
subtitle:  "Active Record III"
date:   2014-03-18 21:28:27
categories: labs
published: false
due_date: 2014-04-9
excerpt: Asociaciones de Active Record.
tags: ror associations active record
---

## Objetivos

Los objetivos para este laboratorio son:

- Seguir trabajando con Active Record.
- Mejorar la calidad de los modelos definidos hasta ahora, agregando asociaciones.
- Poner en práctica lo visto en clase sobre las asociaciones provistas por AR.

---

## Ambiente de trabajo

Necesita una instalación de Ruby para poder completar este laboratorio, la recomendación del chef es instalar Ruby utilizando [RVM](http://rvm.io)
Puede trabajar en el sistema operativo de su elección, pero le recomendamos utilizar alguna distribución de Linux, o Mac OS en su defecto.

Si no desea instalar Ruby, puede descargar la máquina virtual de [Ubuntu 12.04](https://www.dropbox.com/s/n3exax2mm81aoi0/ubuntu12.04.ova) 
preparada por el equipo docente, la cual ya incluye Ruby 2.0 y Rails.

---

## Descripción

Como ya vimos, para Rails, una base de datos no es más que un sistema de persistencia, algo que permite guardar información, de forma confiable.

Rails prefiere que toda la lógica de negocio, así como reglas de integridad y consistencia se apliquen en los modelos, en vez de la data como tal.
Esto tiene algunas ventajas, al hacerse en código de Ruby, tenemos una forma estándar, independiente del sistema de persistencia de los datos.

Al utilizar un lenguaje de programación de alto nivel, tenemos construcciones más completas y fáciles de escribir para definir las reglas.
Además, se definen de forma declarativa, haciéndolas fácil de administrar y mantener.

Para manifestar las relaciones entre nuestros modelos, ActiveRecord presenta el concepto de asociación, el cual crea un enlance
entre dos modelos, (en realidad, instancias de esos modelos).

Rails provee distintos tipos de asociación, pensandos para los distintos tipos de relaciones que conocemos:

- belongs_to
- has_many
- has_many through
- has_one
- has_and_belongs_to_many

Ya hemos platicado de esto en clase, es hora de ponerlo en práctica.

---

## 1. Asociaciones

En nuestro API, de momento tenemos los siguientes modelos:

- Equipo
- Grupo
- Estadio
- Partido

¿Existe algun tipo de relación entre ellos? En su mente la respuesta debe ser **sí**. 
De hecho existen varias relaciones entre algunos de esos modelos.

Vamos por partes.

### Equipos

- Un equipo pertenece a un grupo.
- Un equipo tiene varios partidos por jugar.

### Grupos

- Un grupo tiene varios equipos.

### Estadios

- Un estadio tiene varios partidos.

### Partidos

- Un partido pertenece a un equipo local.
- Un partido pertenece a un equipo visitante.
- Un partido pertenece a un estadio.
- Un partido pertenece a un ganador.
- Un partido pertenece a un perdedor.
- Un partido pertenece a un grupo.


### Observación

Si recuerda, cuando definimos las tablas de equipos y grupos, no colocamos ninguna referencia entre ellos, sin embargo, ahora estamos definiendo
algunas relaciones entre los modelos que los representan. Esto significa que nuestro modelo de datos está incompleto.  


#### ¿Qué información nos interesa sobre la participación de un equipo en un grupo?

Recordemos que durante la fase de grupos, se asignan 3 puntos al equipo que gane un partido, 0 puntos al perdedor, y 1 punto a cada uno en caso de empate.
Al finalizar todos los partidos del grupo, se escogen a los 2 equipos con más puntos. En caso de empate, se revisan otros criterios, como los goles.

Esto significa que necesitamos un **tercer modelo** que represente la *participación* de un equipo dentro de un grupo, y debemos almacenar:

- El equipo (referencia)
- El grupo (referencia)
- Total de puntos conseguidos por el equipo.
- El total de partidos jugados.
- El total de partidos ganados.
- El total de partidos perdidos.
- El total de partidos empatados.
- El total de goles anotados.
- El total de goles recibidos.

Esto significa que las asociaciones entre equipos y grupos se darán **a través** de este modelo.

---

## Recordatorio

Para más información sobre asociaciones puede consultar:

[http://guides.rubyonrails.org/association_basics.html](http://guides.rubyonrails.org/association_basics.html)

### ¿Cómo lo pruebo?

Para interactuar con sus modelos, puede utilizar la consola de Rails:

{% highlight console %}
  $ rails console
  # también se puede
  $ rails c
{% endhighlight %}

Para salir de la consola escriba *exit*.

--
## Entrega

La entrega se realizará a través del `GES` antes de las **23:55:00** del día **Miércoles 9 de abril 2014**, debe enviar un link a un repositorio de github de su proyecto con los cambios necesarios.

--