---
layout: post
title:  "Laboratorio #5"
subtitle:  "Controladores, controladores, controladores"
date:   2014-04-18 21:28:27
categories: labs
published: true
due_date: 2014-05-07
excerpt: Controladores de RoR.
tags: ror controllers
---

## Objetivos

Los objetivos para este laboratorio son:

- Agarrar práctica escribiendo controladores.
- Comprender la relación entre modelo y controlador.

---

## Ambiente de trabajo

Necesita una instalación de Ruby para poder completar este laboratorio, la recomendación del chef es instalar Ruby utilizando [RVM](http://rvm.io)
Puede trabajar en el sistema operativo de su elección, pero le recomendamos utilizar alguna distribución de Linux, o Mac OS en su defecto.

Si no desea instalar Ruby, puede descargar la máquina virtual de [Ubuntu 12.04](https://www.dropbox.com/s/n3exax2mm81aoi0/ubuntu12.04.ova) 
preparada por el equipo docente, la cual ya incluye Ruby 2.0 y Rails.

---

## Descripción

Hasta este punto, ha construido un modelo de datos robusto, el cual expresa las distintas relaciones entre las entidades en forma de asociaciones
y aplica diferentes validaciones para asegurar la consistencia e integridad de los datos.

Ahora vamos a abrir al mundo la posibilidad de interactuar con sus modelos por medio de una interfaz HTTP, a través de controladores de RoR.

Ya hemos platicado de esto en clase, es hora de ponerlo en práctica.

---

## 1. Controladores

En nuestro API, de momento tenemos los siguientes modelos:

- Equipo
- Grupo
- Estadio
- Partido

Escriba un controlador para cada uno de esos modelos, estos controladores deben tener las siguientes acciones:

1. index
2. show
3. create
4. update
5. delete

---

## Recordatorio

No olvide agregar las rutas necesarias para estos controladores en su archivo de rutas.

{% highlight ruby %}
  resources :teams
  # etc...
{% endhighlight %}


Para más información sobre controladores o rutas puede consultar:

* [http://guides.rubyonrails.org/action_controller_overview.html](http://guides.rubyonrails.org/action_controller_overview.html)
* [http://guides.rubyonrails.org/routing.html](http://guides.rubyonrails.org/routing.html)

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

La entrega se realizará a través del `GES` antes de las **23:55:00** del día **Miércoles 7 de Mayo 2014**, debe enviar un link a un repositorio de github de su proyecto con los cambios necesarios.

--