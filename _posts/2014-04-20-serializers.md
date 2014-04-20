---
layout: post
title:  "Laboratorio #6"
subtitle:  "Serializadores"
date:   2014-04-20 10:28:27
categories: labs
published: true
due_date: 2014-05-21
excerpt: Active Model Serializers
tags: ror active model serializers
---

## Objetivos

Los objetivos para este laboratorio son:

- Agarrar práctica utilizando serializadores.
- Comprender la relación entre un modelo, el controlador y su representación en JSON.

---

## Ambiente de trabajo

Necesita una instalación de Ruby para poder completar este laboratorio, la recomendación del chef es instalar Ruby utilizando [RVM](http://rvm.io)
Puede trabajar en el sistema operativo de su elección, pero le recomendamos utilizar alguna distribución de Linux, o Mac OS en su defecto.

Si no desea instalar Ruby, puede descargar la máquina virtual de [Ubuntu 12.04](https://www.dropbox.com/s/n3exax2mm81aoi0/ubuntu12.04.ova) 
preparada por el equipo docente, la cual ya incluye Ruby 2.0 y Rails.

---

## Descripción

Hasta este punto, ha construido una aplicación simple, capaz de representar un modelo de datos a través de JSON, e interactuar con él por medio de HTTP.
Esta representación es una copia exacta de los datos subyacentes, lo cual no nos da mucha flexibilidad, de forma que no podemos escojer qué datos mostrar, ni 
cómo se deben mostrar.

Para mejorar esto, y resolver esas deficiencias, existe una herramienta llamada Active Model Serializers.

Ya hemos platicado de esto en clase, es hora de ponerlo en práctica.

---

## Serializadores

En nuestro API, de momento tenemos los siguientes modelos:

- Equipo
- Grupo
- Estadio
- Partido

Escriba un serializador para cada uno de esos modelos, de forma que la representación en JSON de cada uno incluya los siguientes datos:

### 1. Equipo

* Nombre
* Grupo
* Entrenador
* Bandera
* Uniforme
* Partidos de la fase de grupos para el equipo
* URL al equipo

**Ejemplo:**

{% highlight json %}
{
  name: "Brazil",
  group: "A",
  description: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce non volutpat tellus, sit amet imperdiet dolor. Nullam porta sapien ut ipsum rhoncus, vestibulum ornare arcu ultricies.",
  coach: "Luiz Felipe Scolari",
  matches: [
  {
    group: {
      name: "A"
    },
    teams: {
      local: "Brazil",
      visitor: "Croatia"
    },
    stadium: {
      name: "Arena de Sao Paulo"
    },
    stage: "group",
    state: "scheduled",
    date: "2014-06-12T14:00:00.000-06:00",
    url: "http://wc14.herokuapp.com/matches/1"
  }
  ],
  flag_url: "http://url-to-somewhere",
  photo_url: "http://url-to-somewhere",
  url: "http://wc14.herokuapp.com/teams/brazil"
}
{% endhighlight %}

### 2. Grupo

* Nombre
* Equipos (incluyendo: nombre del equipo, URL al equipo)
* Posiciones de los equipos (incluyendo: nombre del equipo, partidos jugados, ganados, empatados, perdidos, goles a favor y en contra y total de puntos)
* URL al grupo

**Ejemplo:**

{% highlight json %}
{
  name: "A",
  teams: [
    {
      name: "Brazil",
      url: "http://wc14.herokuapp.com/teams/brazil"
    },
    {
      name: "Cameroon",
      url: "http://wc14.herokuapp.com/teams/cameroon"
    },
    {
      name: "Croatia",
      url: "http://wc14.herokuapp.com/teams/croatia"
    },
    {
      name: "Mexico",
      url: "http://wc14.herokuapp.com/teams/mexico"
    }
  ],
  standings: [
    {
      team: "Brazil",
      played: 0,
      wins: 0,
      loses: 0,
      draws: 0,
      goals_scored: 0,
      goals_against: 0,
      goal_average: 0,
      points: 0
    }, ...
  ],
  url: "http://wc14.herokuapp.com/groups/a"
}
{% endhighlight %}

### 3. Estadio

* Nombre
* Ciudad
* Año de construcción
* Capacidad
* Partidos de la fase de grupos a jugarse en el estado
* URL al stadio

**Ejemplo:**

{% highlight json %}
{
  name: "Arena Amazonia",
  city: "Manaus",
  construction_year: "2013",
  capacity: 42374,
  matches: [
    {
      group: {
	name: "A"
      },
      teams: {
	local: "Cameroon",
	visitor: "Croatia"
      },
      stadium: {
	name: "Arena Amazonia"
      },
      stage: "group",
      state: "scheduled",
      date: "2014-06-18T16:00:00.000-06:00",
      url: "http://wc14.herokuapp.com/matches/4"
    }, ...
  ],
  image_url: "http://url-to-somewhere",
  url: "http://wc14.herokuapp.com/stadiums/6"
}
{% endhighlight %}

### 4. Partido

* Grupo
* Equipos
* Marcador
* Estadio
* Fase
* Estado
* Fecha
* Goles
* URL

**Ejemplo:**

{% highlight json %}
{
  group: {
    name: "A"
  },
  teams: {
    local: "Brazil",
    visitor: "Croatia"
  },
  score: {
    local: 2,
    visitor: 0
  },
  stadium: {
    name: "Arena de Sao Paulo"
  },
  stage: "group",
  state: "finished",
  date: "2014-06-12T14:00:00.000-06:00",
  url: "http://wc14.herokuapp.com/matches/1",
  goals: [
    {
      minute: 14,
      scorer: "Neymar Jr",
      team: "Brazil"
    },
    {
      minute: 60,
      scorer: "Neymar Jr",
      team: "Brazil"
    }
  ]
}
{% endhighlight %}

---

## Recordatorio

Para más información sobre serializadores:

[https://github.com/rails-api/active_model_serializers](https://github.com/rails-api/active_model_serializers)

### ¿Cómo lo pruebo?

Para interactuar con sus controladores, debe iniciar un servidor web:

{% highlight console %}
  $ rails server
  # también se puede
  $ rails s
{% endhighlight %}

Para salir de la consola escriba *exit*.

Por defecto, esto inicia WEBrick en el puerto 3000, por lo que puede entrar desde su navegador a [http://localhost:3000](http://localhost:3000)

Puede hacer requests hacia su aplicación a través del navegador, o utilizando aplicaciones como cURL o chrome apps como [POSTman](https://chrome.google.com/webstore/detail/postman-rest-client/fdmmgilgnpjigdojojpjoooidkmcomcm?hl=en).

--
## Entrega

La entrega se realizará a través del `GES` antes de las **23:55:00** del día **Miércoles 21 de Mayo 2014**, debe enviar un link a un repositorio de github de su proyecto con los cambios necesarios.

--