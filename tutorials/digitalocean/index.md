---
layout: default
title:  Digitalocean deployment howto - Alf.io
categories: tutorial
---

Deze tutorial is gemaakt voor Ubuntu 14.04 en is niet getest op andere versies. Ook zit de kans erin dat dit niet alleen op een DO VPS werkt, maar ook op andere VPS'en die niet getest zijn.

We beginnen de tutorial met het opzetten dan een droplet. Hier hebben wij gekozen voor een 512MB droplet, omdat we dit niet in productie gaan gebruiken en er niet veel RAM nodig is. Qua diskspace kan je ook nog wel even mee vooruit.

Requirements:
 - Postgresql 9.4.4+
 - NGINX 1.6.2+
 - Ubuntu 14.04

We beginnen met het opzetten van PostgreSQL, dit is de database software waar alf.io gebruik van maakt.
Om alf.io gebruik te laten maken van de database moet we het eerst installeren met:
    $ apt-get update
    $ apt-get install postgresql
Als het eenmaal geinstalleerd is moeten we de gebruiker aanmaken, dat doen we door eerst in de `postgres` in te loggen met `sudo su postgres`. Nu gaan we de gebruiker aanmaken (NOTE: Schrijf deze informatie op, deze zal je later nodig hebben).

Voordat we een gebruiker aan kunnen maken moet we eerst met de server connecten.
    $ psql template1
    
Nu we in de database zitten kunnen we beginnen met het maken van de user en de database voor alf.io.
    CREATE USER alfio WITH PASSWORD 'superSecretPwd';
    CREATE DATABASE alfio;
    GRANT ALL PRIVILEGES ON DATABASE alfio TO alfio;
    \q;

Om te kijken of de user goed aangemaakt is proberen we in  te loggen met deze user