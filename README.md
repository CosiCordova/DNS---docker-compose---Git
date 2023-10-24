# DNS---docker-compose---Git
###Las opciones que ofrece el docker compose son:

 ###Services: Define los servicios que componen la aplicación y sus configuraciones. Cada servicio es un contenedor individual. Por ejemplo:

  services:
    bind9:

 ###image: Especifica la imagen de Docker que se utilizará para construir el contenedor del servicio.

    image: ubuntu/bind9

 ###container_name: Define un nombre personalizado para el contenedor, que en este caso es asir_bind9.

    container_name: asir_bind9 

 ###ports: Mapea los puertos 53 en el contenedor a los puertos 53 tanto TCP como UDP en el host, lo que permite que el servicio DNS esté disponible en el host.

  ports:
      - 53:53/tcp
      - 53:53/udp

 ###networks: Define la red bind9_subnet, con una dirección IP estática de 172.28.5.1. Esta red se utiliza para conectar el servicio bind9 a una red específica.

  networks:
      bind9_subnet:
        ipv4_address: 172.28.5.1

 ###volumes: Monta dos volúmenes locales (./conf y ./zonas) en el contenedor, que se utilizan para configurar la configuración y las zonas de BIND9

  volumes:
      - ./conf:/etc/bind
      - ./zonas:/var/lib/bind

 ###environment: Establece la variable de entorno TZ en Europe/Paris, lo que configura la zona horaria del contenedor

  environment:
      - TZ=Europe/Paris

 ###La definición de la red bind9_subnet se marca como externa con external: true, lo que indica que esta red ya debe existir fuera del archivo docker-compose.yml y se utiliza para conectar el servicio bind9 

  networks:
  bind9_subnet: 
    external: true