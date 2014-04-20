---
layout: post
title:  "Laboratorio #3"
subtitle:  "Active Record II"
date:   2014-03-17 21:28:27
categories: labs
published: true
due_date: 2014-04-2
excerpt: Validaciones de Active Record.
tags: ror validations active record
---

## Objetivos

Los objetivos para este laboratorio son:

- Seguir trabajando con Active Record.
- Mejorar la calidad de los modelos definidos hasta ahora, agregando validaciones.
- Poner en práctica lo visto en clase sobre las validaciones provistas por AR.

---

## Ambiente de trabajo

Necesita una instalación de Ruby para poder completar este laboratorio, la recomendación del chef es instalar Ruby utilizando [RVM](http://rvm.io)
Puede trabajar en el sistema operativo de su elección, pero le recomendamos utilizar alguna distribución de Linux, o Mac OS en su defecto.

Si no desea instalar Ruby, puede descargar la máquina virtual de [Ubuntu 12.04](https://www.dropbox.com/s/n3exax2mm81aoi0/ubuntu12.04.ova) 
preparada por el equipo docente, la cual ya incluye Ruby 2.0 y Rails.

---

## Descripción

Para Rails, una base de datos no es más que un sistema de persistencia, algo que permite guardar información, de forma confiable.

Rails prefiere que toda la lógica de negocio, así como reglas de integridad y consistencia se apliquen en los modelos, en vez de la data como tal.
Esto tiene algunas ventajas, al hacerse en código de Ruby, tenemos una forma estándar, independiente del sistema de persistencia de los datos.

Al utilizar un lenguaje de programación de alto nivel, tenemos construcciones más completas y fáciles de escribir para definir las reglas.
Además, se definen de forma declarativa, haciéndolas fácil de administrar y mantener.

---

## 1. Validaciones

Para definir reglas de validez sobre un modelo, ActiveRecord (AR) presenta el concepto de validación, lo cual consiste en una regla,
que determina si el valor ingresado para un campo es aceptado por el modelo, o no. En caso de no ser aceptado, la validación provee un mensaje de error,
el cual puede ser entregado al usuario, de forma que pueda corregir.

Cada uno de nuestros modelos debe imponer algunas validaciones, de forma que pueda garantizar la consistencia e integridad de los datos que maneja.

Vamos por partes.

### Equipos

Un equipo posee diferentes características que lo definen, por ejemplo, todo equipo tiene un nombre. ¿Puede existir algún equipo sin nombre? No,
por lo que una validación de **presencia** se ajusta bien a este caso.

Aplique las siguientes validaciones al modelo de equipo:

- Todo equipo debe tener un nombre, el cual sólo puede estar formado por letras (mayúsculas o minúsculas).
- Todo equipo debe tener un nombre de entrenador.
- Todo equipo debe tener un url a una foto de su bandera, el cual debe ser un url con formato válido.
- Todo equipo debe tener un url a una foto de su uniforme, el cual debe ser un url con formato válido.
- Todo equipo debe tener un texto que lo describa, un mínimo de 15 caracteres, y un máximo de 200.
- No deben haber equipos con el mismo nombre.
- Un entrenador no puede entrenar a más de un equipo.

### Grupos

Aplique las siguientes validaciones al modelo de grupo:

- Todo grupo debe tener un nombre.
- El nombre de un grupo debe ser único.
- El nombre del grupo no puede tener más de una letra.

**Extra**: Agregue una validación que impida que existan más de 8 grupos.

### Estadios

Aplique las siguientes validaciones al modelo de grupo:

- Todo estadio debe tener un nombre, el cual debe ser único.
- Todo estadio debe tener una ciudad, la cual debe ser única.
- Todo estadio debe tener una fecha de construcción, la cual debe ser una fecha válida.
- Todo estadio debe tener una capacidad máxima, descrita en un número entero positivo.
- Todo estadio debe tener un url a una foto del mismo, el cual debe ser un url con formato válido.
- La ciudad del estadio debe ser una de las siguientes: Belo Horizonte, Brasilia, Cuiaba, Curitiba, Fortaleza, Manaus, Natal, Recife, Rio de Janeiro, Salvador, Sao Paulo.

### Partidos

Aplique las siguientes validaciones al modelo de grupo:

- Todo partido debe tener una fecha de juego, la cual debe ser válida.
- Todo partido debe ser jugado en alguna fase.
- Todo partido debe encontrarse en un estado.
- Todo partido debe tener un equipo local.
- Todo partido debe tener un equipo visitante.
- Todo partido debe tener un marcador, el cual incluye una cantidad entera no negativa de goles locales, y una cantidad entera no negativa de goles visitantes.
- Todo partido terminado debe tener un ganador (a menos que haya sido empate).
- Todo partido terminado debe tener un perdedor (a menos que haya sido empate).
- Todo partido que tenga la misma cantidad de goles locales y visitantes debe ser un empate.
- Todo partido debe tener un estadio.
- No se debe permitir más de un partido en la misma fecha en el mismo estadio.
- El equipo local debe ser distinto al equipo visitante.
- Un mismo equipo no puede jugar dos partidos en la misma fecha.

Todo partido debe corresponder a una de las siguientes fases:

- Grupos
- Octavos de final (eliminación)
- Cuartos de final (eliminación)
- Semifinales (eliminación)
- Final

Todo partido se debe encontrar en **uno** de los siguientes estados:

- Por jugar
- En juego
- Finalizado

---

## Recordatorio

Para más información sobre validaciones puede consultar:

[http://guides.rubyonrails.org/active_record_validations.html](http://guides.rubyonrails.org/active_record_validations.html)

### ¿Cómo lo pruebo?

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
2.0.0p247 :001 > g = Group.new
#<Group id: nil, name: nil, created_at: nil, updated_at: nil>
2.0.0p247 :004 > g.valid?
false
2.0.0p247 :004 > g.errors
{% endhighlight %}

Para salir de la consola escriba *exit*.

--
## Entrega

La entrega se realizará a través del `GES` antes de las **23:55:00** del día **Miércoles 2 de Abril 2014**, debe enviar un link a un repositorio de github de su proyecto con los cambios necesarios.

--