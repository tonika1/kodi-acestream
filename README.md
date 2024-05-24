# kodi-acestream
Conexión de Kodi con acestream

## Consideraciones previas

Aquí no vas a encontrar enlaces acestream, sólo como conectar contenedores acestream con tvheadend. Los enlaces acestream que aparecen en esta guía son enlaces inventados que no apuntan a ningún stream.

No vamos a poder grabar las emisiones, para poder grabar hay que usar la guía [tvheadend-acestream-docker](https://github.com/tonika1/tvheadend-acestream-docker/blob/main/README.md)

Debemos tener instalado la última versión de [acestream](https://docs.acestream.net/products/)

Debemos teber instalado [kodi](https://kodi.tv/download/)

Debemos tener instalado el addon IPTV Simple Client que es un addon que puedes instalar desde los repositorios de kodi, está dentro de la sección Clientes PVR. Después nos meteremos con su configuración.

Debemos tener instalado el [addon Horus](https://mundokodi.com/addon-horus-en-kodi/)

Configura el addon de Horus para utilizar un reproductor externo ya que con algunos sistemas operativos (android seguro) si no repoduces el video con el ACE Player se para la reproducción a los 10 minutos:

![Acestream_2-1024x549](https://github.com/tonika1/kodi-acestream/assets/36047512/8e8b4e08-e8db-448b-a11f-fa2cce84c870)

## Configurar el fichero m3u con nuestros enlaces acestream para usarlos en kodi

La primera fila siempre contiene #EXTM3U para identificar este archivo como una lista m3u de reproducción y opcionalmente se le puede añadir la guía que se va usar mediante url-tvg:

```bash
#EXTM3U url-tvg="https://raw.githubusercontent.com/davidmuma/EPG_dobleM/master/guiatv.xml"
```
Las filas restantes contienen dos filas distintas por canal, la primera: 
a) Comienza con #EXTINF que es donde se definen las propiedades

```bash
#EXTINF:-1 group-title="grupo" tvg-id="Nombre del canal" tvg-name="Nombre del canal",Nombre del canal
```
Donde tvg-id="Nombre del canal" debe ser el nombre del canal de la guía, en mi caso, sería un canal de [EPG_DobleM](https://github.com/davidmuma/EPG_dobleM/blob/master/Varios/Canales_soportados.txt)

b) otro inmediatamente debajo de él que contiene la dirección del canal con la IP del servidor acestream (no puede ser 127.0.0.1) y el id del stream: 

```bash
plugin://script.module.horus?action=play&id=d00223931b1854163e24c5c22475015d7d45abcd
```
Donde d00223931b1854163e24c5c22475015d7d45abcd es el id del enlace acestream, es decir, sería la última parte de la url http://127.0.0.1:6878/ace/getstream?id=d00223931b1854163e24c5c22475015d7d45abcd

Después repetiríamos la opción a) y b) como enlaces acestream tengamos. Por ejemplo:

```bash
#EXTM3U url-tvg="https://raw.githubusercontent.com/davidmuma/EPG_dobleM/master/guiatv.xml"
#EXTINF:-1 group-title="infantil" tvg-id="Canal infantil" tvg-name="Canal infantil",Canal infantil
plugin://script.module.horus?action=play&id=e6f06d697f66a8fa606c4d61236c24b0d604dabc
#EXTINF:-1 group-title="SERIES" tvg-id="Canal de series" tvg-name="Canal de series",Canal de series
plugin://script.module.horus?action=play&id=e6f06d697f66a8fa606c4d61236c24b0d604d000
```
Una vez creado el fichero m3u, por ejemplo canales.m3u, lo guardaremos en una ubicación a la que kodi pueda acceder (un USB, un servidor web, etc).

## Configurar el addon IPTV Simple Client

Vamos a la configuración y hacemos clic sobre "Añadir configuración del Add-on" y ponemos estos valores:

![Captura de pantalla_2024-05-24_20-40-49](https://github.com/tonika1/kodi-acestream/assets/36047512/583f5ae6-72c8-4f38-8e9c-faa789f876f9)



![Captura de pantalla_2024-05-24_20-41-18](https://github.com/tonika1/kodi-acestream/assets/36047512/91696c5d-ec65-4362-a924-d2bc2ad68cec)

![Captura de pantalla_2024-05-24_20-41-53](https://github.com/tonika1/kodi-acestream/assets/36047512/8a91a74e-cb60-403f-8a22-e5e4ae16d846)

![Captura de pantalla_2024-05-24_20-42-07](https://github.com/tonika1/kodi-acestream/assets/36047512/bc282b59-81fd-44dd-83e4-d3e426032b8b)

La URL del fichero XML que yo uso es: 

```bash
https://raw.githubusercontent.com/davidmuma/EPG_dobleM/master/guiafanart_color.xml.gz
```

![Captura de pantalla_2024-05-24_20-42-24](https://github.com/tonika1/kodi-acestream/assets/36047512/9f30ea0d-b6d7-4073-8e96-91a700074885)

![Captura de pantalla_2024-05-24_20-42-34](https://github.com/tonika1/kodi-acestream/assets/36047512/0d9a9bfc-3ca4-4bec-8050-260d6b054fa5)

Guardamos los cambios y activamos el addon
