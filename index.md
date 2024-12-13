<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Aplicacion Twitsnap](#aplicacion-twitsnap)
  - [Manuales](#manuales)
  - [Arquitectura](#arquitectura)
- [Analisis Post Mortem](#analisis-post-mortem)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Aplicacion Twitsnap

## Manuales

[Manual De usuario](https://twitsnap.github.io/docs/user_manual)

[Manual de Backoffice](https://twitsnap.github.io/docs/backoffice_manual)

## Arquitectura

Se decidio ir por una arquitecutra de microservicios como se puede ver a continuacion:

![arquitectura](docs/images/Arquitectura%20Aplicacion.jpg)

Para cada microservicio se agregó un link al repositorio correspondiente

1) **Gateway**: Este microservicio es el punto de entrada de todos los usuarios de la aplicación. Se encargará tambien de autenticar a los usuarios mediante una API call al microservicio de autenticacion y de rechazarlos si no esta autorizado. [Repo](https://github.com/TwitSnap/TwitSnap-Gateway)
2) **Autenticación**: Este microservicio es el que se encargará de verificar que los token que le lleguen del Gateway sean validos y que no hayan expirado. Se encarga tambien de todo el proceso de login de los usuarios y la generación de tokens JWT para que un usuario pueda ser autenticado. Se encargará tambien de todo lo relacionado con las passwords de los usuarios. [Repo](https://github.com/TwitSnap/TwitSnap-Auth-API) [Docs](https://twitsnap-auth-api-m6v0.onrender.com/api-docs)
3) **Users**: Este microservicio es el que se encarga de gestionar la información de los usuarios (a excepcion de la password) y de registrar a los usuarios nuevos a nuestra aplicación. Es el trabajo de este microservicio tabmien gestionar todas las interacciones entre usuarios (seguidores y seguidos). [Repo](https://github.com/TwitSnap/TwitSnap-User-API) [Docs](https://twitsnap-user-api-af1u.onrender.com/docs)
4) **Twits**: Este microservicio se encarga de todo lo relacionado con los twits y sus interacciones (likes,retwits, comentarios, favoritos, feed, etc...).[Repo](https://github.com/TwitSnap/TwitSnap-Twits-API) [Docs](https://twitsnap-twits-api.onrender.com/api-docs/)
5) **Chats**: Este microservicio es el encargado de gestionar y guardars los mensajes directos que se envíen los usuarios. [Repo](https://github.com/TwitSnap/TwitSnap-Chat)
6) **Notificaciones**: Este microservicio es el que se encarga de enviar las notificaciones (ya sea mail o push notifications) de los eventos que vayan ocurriendo a traves de la app: [Repo](https://github.com/TwitSnap/TwitSnap-Notifs-API)
   * Push notifications:
     * Menciones
     * Mensajes Directos
     * Nuevos seguidores
   * Mail:
     * Recuperacion de contraseña
     * PIN de registro
     * Cambio de contraseña

7) **Service Registry**: Maneja todo lo que tenga que ver con las api-keys de los microservicios. Se encarga de autenticar dichas keys y verificar si el servicio esta activo o no. [Repo](https://github.com/TwitSnap/TwitSnap-ServiceRegistry-API)


# Analisis Post Mortem
