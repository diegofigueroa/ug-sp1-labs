---
layout: post
title:  "Laboratorio #2"
subtitle:  "Active Record"
date:   2014-02-16 21:28:27
categories: labs
published: true
due_date: 2014-03-26
excerpt: Introducción a Rails y Active Record.
tags: ror intro active record
---

## Objetivos

Esta práctica es para familizarizarse con Ruby on Rails, el framework con el que trabajarán el resto del curso.  
Los objetivos para este laboratorio son:

- Entender la abstraccion creada por el Active Record de Rails para acceder y manipular información de una base de datos mediante programación orientada a objetos.
- Aprender las funciones basicas provistas por Active Record.
- Aprender a utilizar las herramientas de consola de Rails.

---

## Ambiente de trabajo

Necesita una instalación de Ruby para poder completar este laboratorio, la recomendación del chef es instalar Ruby utilizando [RVM](http://rvm.io)
Puede trabajar en el sistema operativo de su elección, pero le recomendamos utilizar alguna distribución de Linux, o Mac OS en su defecto.

Si no desea instalar Ruby, puede descargar la máquina virtual de [Ubuntu 12.04](https://www.dropbox.com/s/n3exax2mm81aoi0/ubuntu12.04.ova) 
preparada por el equipo docente, la cual ya incluye Ruby 2.0 y Rails.

---

## Descripción

Durante las siguientes 7 semanas estará trabajando en construir un RESTful API, utilizando las herramientas de Ruby on Rails como base.
En este laboratorio dará los primeros pasos hacia ese objetivo, comenzará desde abajo, definiendo un modelo de datos.

Por cierto, le gusta el fútbol? ...Claro que sí le gusta, a todo el mundo le gusta. :)

Tenemos excelentes noticias para usted, el API que construirá estará basado en el próximo mundial, a celebrarse en Brasil, (pero usted ya sabe esto).

Un mundial, es un evento muy importante, por lo que es crítico que construya un API que permita a un desarrollador construir aplicaciones
que atraigan a los cientos de millones de aficionados a este deporte.

---
## 1. Modelo de datos

Queremos representar un mundial de fútbol por medio de un API, ¿qué elementos considera importantes?

Seguramente usted está pensando en los equipos, muy bien. Ahora seguro se recordó que estos equipos están organizados en grupos, cada grupo de 4 equipos.
Vamos muy bien esta ahora. ¿Dónde juegan esos equipos? En varias sedes al rededor de Brasil. Y claro, los partidos, cada partidos se juega en un estadio,
entre dos equipos, un local, y un visitante.

Recopilemos, hasta ahora identificamos lo siguiente:

- Equipos
- Grupos
- Estadios
- Partidos

Vamos por partes.

### Equipos

En un mundial de fútbol pariticipan un total de 32 equipos, cada uno en representación de un país. Necesitamos una forma de llevar un registro por cada uno de estos equipos, y sus acciones dentro del torneo. Vamos a representar esto por medio de una tabla de base de datos, y un modelo.

#### ¿Qué información nos interesa capturar?

- Nombre del equipo (país)
- Nombre del entrenador
- Bandera del país (url a imagen)
- Uniforme del equipo (url a imagen)
- Texto que narre un poco sobre la historia de este equipo en mundiales, así como su proceso de clasificación al torneo actual.

Defina una tabla de base de datos que pueda almacenar los datos descritos, y un modelo de ActiveRecord para dicha tabla.

{% highlight ruby %}
class Team < ActiveRecord::Base
    # code
end
{% endhighlight %}

### Grupos

La primera fase del torneo se lleva acabo entre grupos. Los 32 equipos clasificados se dividen en 8 grupos, del A al H.
Cada grupo está compuesto por 4 equipos.

#### ¿Qué información nos interesa capturar?

- Nombre del grupo

Defina una tabla de base de datos que pueda almacenar los datos descritos, y un modelo de ActiveRecord para dicha tabla.

{% highlight ruby %}
class Group < ActiveRecord::Base
  # code
end
{% endhighlight %}

### Estadios

Como sabe, un partido de fútbol se lleva acabo en un estadio. En Brasil 2014 tendremos un total de 12 estadios.

#### ¿Qué información nos interesa capturar?

- Nombre
- Ciudad
- Fecha de construcción
- Capacidad máxima (personas)
- Foto (url a imagen)

Defina una tabla de base de datos que pueda almacenar los datos descritos, y un modelo de ActiveRecord para dicha tabla.

{% highlight ruby %}
class Stadium < ActiveRecord::Base
  # code
end
{% endhighlight %}


### Partidos

Los partidos es la parte más interesante del mundial, cada equipo deja todo de si en el campo buscando la victoria.

#### ¿Qué información nos interesa capturar?

- Fecha del juego
- Fase (fase de grupos, octavos de final, semi-finales, etc.)
- Estado (por jugar, en juego, finalizado)
- Equipo local
- Equipo visitante
- Marcador (goles del local, y goles del visitante)
- Ganador
- Perdedor
- Empate?
- Grupo
- Estadio

Note que necesita una **referencia** para el equipo local, y otra **referencia** para el equipo visitante. Lo mismo para el grupo, y el estadio.
Por convenio, las referencias deben tener un nombre que termina en `_id`, por ejemplo: `team_id`, o `group_id`.

Rails le permite definir una referencia de 2 formas, utilizando el tipo de dato `reference`, o el tipo `integer`.

Un partido se juega en **una** fase del torneo, las fases son las siguientes:

- Grupos
- Octavos de final (eliminación)
- Cuartos de final (eliminación)
- Semifinales (eliminación)
- Final

Un partido puede encontrarse en **uno** de varios estados:

- Por jugar
- En juego
- Finalizado

¿Cómo almacenar esta información? Como diseñador del API, queda a su discreción. ¿Un string? ¿Un entero? ¿?

Defina una tabla de base de datos que pueda almacenar los datos descritos, y un modelo de ActiveRecord para dicha tabla.

{% highlight ruby %}
class Match < ActiveRecord::Base
  # code
end
{% endhighlight %}

---

## Recordatorio

Recuerde que Rails provee generadores para facilitarle la vida. No estamos obligados a utilizar generadores, podemos crear todo a mano, pero esto
nos deja la responsabilidad de cuidar que escribamos todo correctamente, en el lugar correcto (migraciones en el folder de migraciones, modelos en el folder de modelos, etc.)
por lo que es mejor práctica utilizar un generador, el cual es un método más cómodo.

### Migraciones

Para crear una tabla de base de datos, debe utilizar una **migración**.

Puede crear una `migración` con el siguiente comando:

{% highlight console %}
$ rails g migration
{% endhighlight %}

Una vez creada la migración, debe ejecutarla:

{% highlight console %}
$ rails db:migrate
{% endhighlight %}

### Modelos

Para crear un modelo, también tenemos un generador:

{% highlight console %}
$ rails g model
{% endhighlight %}

### Notas adicionales

Antes de poder ejecutar una migración, debe crear su base de datos, lo cual es súmamente fácil:

{% highlight console %}
$ rails db:create
{% endhighlight %}

Si se está preguntando cómo puede destruir una base de datos, es muy fácil también:

{% highlight console %}
$ rails db:drop
{% endhighlight %}

### ¿Cómo lo pruebo?

Rails le dará un error si intenta ejecutar una migración con errores de sintaxis, o si definió un modelo para una tabla no existente, o con errores.  

Recuerde que el convenio de Rails define las tablas en **plural**, y los modelos en **singular**. Por ejemplo, tendremos una tabla `groups`, y un modelo `Group`.

Para interactuar con sus modelos, puede utilizar la consola de Rails:

{% highlight console %}
  $ rails console
  # también se puede
  $ rails c
{% endhighlight %}

Una vez dentro de la consola, debe poder hacer llamadas sobre su modelo, por ejemplo:

{% highlight console %}
$ rails c
Loading development environment (Rails 4.0.2)
2.0.0p247 :001 > Group.new
#<Group id: nil, name: nil, created_at: nil, updated_at: nil>
2.0.0p247 :004 > Group.find(1)
  Group Load (3.8ms)  SELECT "groups".* FROM "groups" WHERE "groups"."id" = ? LIMIT 1  [["id", 1]]
 => #<Group id: 1, name: "A", created_at: "2014-03-02 22:10:48", updated_at: "2014-03-02 22:10:48"> 
{% endhighlight %}

Para salir de la consola escriba *exit*.

--
## Entrega

Debe entregar todo el directorio del proyecto, con una migración por cada tabla, y un modelo para cada una de esas tablas.

La entrega se realizará a través del `GES` antes de las **23:55:00** del día **Miércoles 2 de abril 2014**, debe enviar un link a un repositorio de github de su proyecto.

--