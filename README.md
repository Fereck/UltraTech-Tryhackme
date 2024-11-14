# UltraTech-Tryhackme
Conceptos basicos en Pentesting, Webapp testing and Pivoting 

### Herramientas.

 - Gobuster
 - Nmap
 - GTFOBins
 - Os Command Injection

## Para la estrutura de la prueba me basare en _iso 27001_

	-Reconocimiento. 
	-Análisis de Vulnerabilidades. 
	-Explotacion de Vulnerabilidades.
	-Escalada de Privilegios y Movimiento lateral.
	-Post-Explotacion y Impacto.
	-Reporte y Documetacion de Resultados.




## Reconocimiento.

Necesitamos investigar a lo que estamos atacando. 

![imagen](https://github.com/user-attachments/assets/596c4537-c395-499f-a235-790318d906aa)


### Explicaciones de los parametros: 
`-Pn`: Evita el "pinguear" el puerto para ver si esta activo, con esto asume que esta activo y sirve contra redes que tiene bloqueado los pings ICMP.

`-sVC`: Estos dos `-sV` el cual detecta servicios y sus versiones, `-sC` obtiene informacion adicional sobre servicios ademas de posibles vulnerabilidades.

`-p-`: Escanea todos lo puertos posibles, a diferencia de un escaneo normal que solo escanea los 1000 más comunes.

`-n`: Desactiva la resolucion DNS. (Nmap no intentara convertir la direccion IP a un nombre de Host)

`--min-rate 500`: Ajusta la velocidad minima de envio de paquetes a 500 por segundo, esto genera demasiado ruido en la red, por lo que hace el escaneo mas rapido pero mas detectable.  




### Task 2 :

  (1) R/ Node.js
  
  (2) R/ 31331
  
  (3) R/ Apache
  
  (4) R/ Ubuntu

  (5) R/ 2 

### Puerto 8081

![imagen](https://github.com/user-attachments/assets/f8f0c87f-f4bb-4efd-806b-8aa64217f0c3)

Por encima no se ve nada, ahora usando Gobuster para ver si tiene directorio ocultos.


![imagen](https://github.com/user-attachments/assets/1a7a866e-2af2-460d-b93b-1a306d36aaf1)

En puerto podemos notar una direcorio llamado /Ping , por lo que puede indicar una vulnerabilidad de OS command Injection

Para comprobar que se puede injectar, vamos a ingresar /Ping?ip=10.9.0.72 

![imagen](https://github.com/user-attachments/assets/b118dc30-8ee3-4ce6-80c2-d5fa831f272b)

Como podemos ver el equipo nos leyo el comando por lo que nos podemo comunicar a un sistema, ahora 

![imagen](https://github.com/user-attachments/assets/205b51f2-2fdd-4180-972d-f21a850c3ac9)




### Puerto 31331

![imagen](https://github.com/user-attachments/assets/6e957b64-2cd4-408a-bf61-9ba10d8c89c4)

Podemos ver que es una pagina en beta, muy poca funciones que funcionen.

Usaremos "Gobuster" para ver que directorios ocultos.

![imagen](https://github.com/user-attachments/assets/d4292f54-9151-4a53-af00-22a58c3a4036)


Despues del escaneo vemos varios directorios ocultos.

![imagen](https://github.com/user-attachments/assets/7d30ab1f-0f94-4666-b435-43cdf3ec6ffb)

Revisando dicho directorios encontramos /js el cual contiene algo bastante interesante. 

![imagen](https://github.com/user-attachments/assets/622703c3-ab79-4367-9e23-c1035d28b982)

Un codigo que se encarga de las _*Peticiones*_ verifica el estado de una API y actualiza el formulario de la página para que envíe datos a una dirección específica

y como vimos en el puerto 8081 

![imagen](https://github.com/user-attachments/assets/fdf6da3f-377f-4e61-b6e5-2c6fd6e59a2b)

es por eso que podemos hacer OS Inyeccion

ademas de que gracias al "ls" pudimo ver que tiene una base sql y si leemos la con un "cat" 

![imagen](https://github.com/user-attachments/assets/da94b295-0c02-46fc-8e52-713298761daa)

podemos ver que se mencionan Mr00t: f357a0c52799563c7c7b76c1e7543a32 lo cual lo pasamos por Crackstation

![imagen](https://github.com/user-attachments/assets/902f8988-d847-4b11-90af-9d5ab0453a27)

### Task 3 

  (1) R/ utech.db.sqlite
  
  (2) R/ f357a0c52799563c7c7b76c1e7543a32
  
  (3) R/ n100906


![imagen](https://github.com/user-attachments/assets/368a74c5-e075-465c-ac6b-4213d29d8220)

![imagen](https://github.com/user-attachments/assets/fabe21a6-fa18-4010-ac35-d10eeecb48d5)

usamos GTFOBins para buscar una vulnerabilidad 

![imagen](https://github.com/user-attachments/assets/24e23969-a705-47eb-ad39-713e0d1abfb1)

`docker run -v /:/mnt --rm -it alpine chroot /mnt sh`

Como en este caso ingresamos como root cambiamos el `alpine` por `bash`.

![imagen](https://github.com/user-attachments/assets/153abec3-225f-4099-ae62-952122ecb588)

![imagen](https://github.com/user-attachments/assets/4a7d49b2-31ea-4cba-8258-ccd217aa6ed9)

![imagen](https://github.com/user-attachments/assets/b5865c6c-86d0-4b57-bf07-ae9bdd11c83e)

![imagen](https://github.com/user-attachments/assets/aa95c603-5d9c-41e2-a76c-75c765a13730)

### Task 4

 R/ MIIEogIBA

Y con eso damos por finalizada la maquina 





