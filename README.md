**Project: “Cloud Computing in European schools”**  
<img src="/media/cloud-computing-logoproject.jpg" height="100" width="170">

 Number: Project: 2019-4-ES01-KA202-038471

<img src="/media/cofinanciadoEN.png" height="50" width="200"> <img src="/media/logoIES-Modificado.png" height="75" width="200">  




# Introducción a PaaS: desarrollar, implementar, ejecutar y administrar aplicaciones en la nube
  



#### Disclaimer
&nbsp;&nbsp;&nbsp;  *"El apoyo de la Comisión Europea para la producción de esta publicación no constituye una aprobación de los contenidos que refleje únicamente las opiniones de los autores, y la Comisión no se hace responsable del uso que pueda hacerse de la información contenida en el mismo."*




#### Autores

&nbsp;&nbsp;&nbsp;  Este trabajo está realizado por Manuel Santos, José Antonio Busto, José María Parrilla y Víctor López bajo la licencia Creative Commons :  <img src="/media/Licencia-Tipo2.png" height="25" width="75">
  



### Objetivo
&nbsp;&nbsp;&nbsp; Plataforma como servicio(PaaS), es un modelo de computación en la nube que permite a los usuarios desarrollar, implementar, ejecutar y administrar aplicaciones sin preocuparse por las capas subyacentes. Las alternativas utilizadas hoy se centran en el uso de contenedores que promueven el enfoque de desarrollo de **aplicaciones basado en microservicios** (frente a **aplicaciones monolíticas**), ya que los diferentes servicios en los que estamos separados de la aplicación pueden ejecutarse fácilmente en diferentes contenedores. Realizaremos un estudio de Docker, Kubernetes y OpenShift para desarrollar, implementar, ejecutar y administrar aplicaciones basadas en microservicios.

&nbsp;&nbsp;&nbsp; Esta actividad ha sido desarrollada para desarrollar la competencia profesional incluida en el proyecto Erasmus + "Cloud Computing en escuelas europeas".

## Indice
- Instalación de Minikube y Kubectl
- Tolerancia a fallos
- Escalabilidad
- Balanceo de Cargas
- Actualizaciones
- Rollback 
- Enrutando nuestra aplicación

<br>

<h1>Kubernetes</h1>
<br>
<p>En el documento anterior hablamos sobre Docker pero en este caso vamos a hablar sobre Kubernetes.</p>
<p>Kubernetes es un orquestador de contenedores de aplicación escrito en Go y con licencia Apache-2.0, fue lanzado el 21 de julio de 2015 por Google que rápidamente se alió con la Linux Foundation para crear la Cloud Native Computing Foundation (CNCF) y dejó el proyecto en sus manos.</p>
<p>Ahora pasaremos a explicar como descargarlo y usarlo de forma adecuada.</p>
<br>
<h2>Instalación de Minikube y Kubectl</h2>
<p>Minikube es una versión ligera de Kubernetes, por lo que usaremos Minikube para trabajar. Primero tenemos que descargarlo, después le daremos los permisos correspondientes, haremos una copia a la ruta de carpetas /usr/local/bin/ y por último, se muestra como podemos borrar Minikube:</p>
<br>
<img src="media/1.Instalacion de minikube y kubectl/1-1.png" height="400" width="550"/>
<br>
<p>Ahora en la siguiente captura hacemos lo mismo pero con Kubectl, es decir, descargar, dar permisos, copiarlo a la misma ruta y como borrarlo:</p>
<br>
<img src="media/1.Instalacion de minikube y kubectl/1-2.png" height="400" width="550"/>
<br>
<p>Una vez descargado Minikube arrancamos la máquina con el comando de la siguiente imagen:</p>
<br>
<img src="media/1.Instalacion de minikube y kubectl/1-4.png" height="400" width="550"/> 
<br>
<p>En la siguiente captura podemos comprobar el número de nodos que tenemos(en este caso, el nodo que tenemos actualmente) y aparece clasificado por los siguientes datos: Nombre, Status, Roles, Age y Version.</p>
<img src="media/1.Instalacion de minikube y kubectl/1-5(para comprobar el numero de nodos).png" height="400" width="550"/>
<br>
<p>Por último, en este punto para añadir el componente ingress deberemos poner la siguiente línea de comando:</p>
<br>
<img src="media/1.Instalacion de minikube y kubectl/1-6(para agregar el componente ingress).png" height="400" width="550"/>

<h2>Tolerancia a fallos</h2>
<p>Un POD es un grupo de: una dirección "IP", una o más aplicaciones y uno o<br> más volúmenes.Representa una unidad que puede realizar una tarea / servicio.<p>
<br>
Creamos un Pod para meter nuestra aplicación web
<img src="media/2.Tolerancia a fallos/2-1(creamos un pod).png" height="400" width="550"/>
<br>
Podemos comprobar el número de Pods con el siguiente comando
<img src="media/2.Tolerancia a fallos/2-2(podemos comprobar el numero de pods con este comando).png" height="400" width="550"/>
<br>
Si eliminamos el pod con el siguiente comando nos podemos dar cuenta de que Kubernetes 
nos crea automáticamente otro pod
<img src="media/2.Tolerancia a fallos/2-3(si eliminamos el pod con el comando puesto, podemos observar que kubernete crea otro pod automaticamente).png" height="400" width="550"/>
<br>
<p>Utilizamos el siguiente comando para comprobar el recurso deployment:</p>
<br>
<img src="media/2.Tolerancia a fallos/2-4(comando para comprobar el recurso deployment)" height="400" width="550"/>
<br>
<p>Y por último ejecutaremos el siguiente comando para comprobar el recurso<br> ReplicaSet</p><br>
<img src="media/2.Tolerancia a fallos/2-5(y comando para comprobar el recurso Replicaset)" height="400" width="550"/>


<h2>Escalabilidad</h2>

<p>RepiclateSet nos permite replicar los pods. Nosotros utilizaremos el siguiente<br> comando para replicar los pods:</p><br>
<img src="media/3.Escalabilidad/3-1(podemos replicar un pod con este comando)" height="400" width="550"/>
<br>

<p>Con el siguiente comando comprobaremos cómo se han creado los 4 pods en base<br> al primero y que cada uno se está ejecutando en un nodo diferente:</p><br>

<img src="media/3.Escalabilidad/3-2(y comprobaremos con este otro comando como se ha creado 4 pods en base al primero que creamos)" height="400" width="550"/>
<br>

<h2>Balanceo de carga</h2>
<p>Crearemos un recurso Servicio para acceder a la aplicación que vamos a crear,<br> mediante el siguiente comando:</p><br>

<img src="media/4.Balanceo de carga/4-1(con este comando crearemos un recurso Servicio para acceder a la aplicación que estamos creando)" height="400" width="550"/>
<br>

<p>Ahora comprobaremos el puerto y la ip asignada de nuestra aplicación con los<br> siguientes comandos:</p><br>

<img src="media/4.Balanceo de carga/4-2(Ahora simplemente comprobamos el puerto y la ip asignada de nuestra aplicación con los siguientes comandos)" height="400" width="550"/>
<br>

<p>Por último comprobaremos que accede correctamente a nuestra aplicación<br> introduciendo la ip y el puerto</p><br>

<img src="media/4.Balanceo de carga/4-3(y comprobamos que accede correctamente introduciendo la ip y el puerto)" height="400" width="550"/>
<br>

<h2>Actualizaciones</h2>
Si queremos actualizar nuestra aplicación , después de hacer los cambios correspondientes y subirlo a la Web DockerHub basta con poner este el siguiente comando
<img src="media/5.Actualizaciones/5-1(si quisieramos actualizar nuestra aplicacion a otra version mas nueva, despues de hacer los cambios correspondientes y subirlo a dockerhub, basta con poner el comando siguiente).png" height="400" width="550"/>
<br>
En esta imagen podremos observar si se ha actualizado nuestra aplicación <img src="media/5.Actualizaciones/5-2(comprobamos que se ha actualizado correctamente).png" height="400" width="550"/>
<br>
<h2>Rollback</h2>
Si queremos volver a la versión anterior solo bastará con hacer un rollback
<img src="media/6.rollback/6-1.png" height="400" width="550"/>
<br>
<h2>Enrutando nuestra aplicación</h2>
Para enrutar nuestra aplicación previamente creamos el archivo
<img src="media/7.Enrutando nuestra aplicacion/7-1(creamos el archivo).png" height="400" width="550"/>
<br>
Configuramos el archivo ingress.yaml 
<img src="media/7.Enrutando nuestra aplicacion/7-2(configuramos el archivo ingress.yaml).png" height="400" width="550"/>
<br>
Creamos el recurso Ingress
<img src="media/7.Enrutando nuestra aplicacion/7-3(creamos el recurso ingress).png" height="400" width="550"/>
<br>
Comprobamos el recurso creado
<img src="media/7.Enrutando nuestra aplicacion/7-4(y comprobamos el recurso creado).png" height="400" width="550"/>
Finalmente comprobamos su funcionamiento
<img src="media/7.Enrutando nuestra aplicacion/7-5(y comprobamos que funciona).png" height="400" width="550"/>
<br>









