***********
XCI BUILDER (v0.7)
***********
Elaborado por JulesOnTheRoad para elotrolado.net
https://github.com/julesontheroad/XCI_Builder
---------------
0. Changelog
---------------
v0.7   - Limpiados echos, dando al usuario un mejor entendimiento del proceso
         A�adida compatibilidad con XCI_BatchBuilder.
         Eliminado auto-exit al final del programa para que pueda ser usado por l�nea de comandos.
	 Realizados un par de arreglos en el c�digo.

v0.6.5.2- Reformada carpeta ztools para eliminar sfk.exe ya que no era necesario. A�adida la build de Bigjokker de hacbuild para eliminar la advertencia de falta de 
REV2     header_key.txt en hacbuild, ya que esta clave no es realmente necesaria. 
         Se ha vuelto a la anterior build de hactool en lugar de la prebuild publicada por SciresM ya que parec�a dar problemas a usuarios de sistemas 32bits.
	 En caso de necesitar la build de SciresM https://github.com/SciresM/hactool/releases/tag/1.2.0

v0.6.5.2 - Peque�o arreglo. L�nea a�adida para prevenir la generaci�n de [lc].nsp en archivos sin ticket (archivos custom nsp).
v0.6.5 - Realizados bastantes cambios desde la versi�n inicial. Los cu�les se detallan a continuaci�n:
  I - A�adida compatibilidad con juegos con m�s de 5 nca. (Juegos con manual en html) En estos se ha decidido eliminar 
      el manual del juego, lo cu�l no impide su ejecuci�n. 
	  El intento de acceder al manual desde los juegos que lo incluyen resulta en una acci�n que no da lugar a ning�n 
	  resultado. Los juegos probados pueden jugarse perfectamente sin manual.
   II - La ruta de salida se ha movido ha la carpeta "output_xcib" para tenerlo todo m�s organizado y de cara a que se pueda tener NX-Trimmer
	en la misma carpeta que XCI_Builder, el cu�l usa "output_nxt" como salida.
   III - Reformado de carpeta ztools, eliminando aplicaciones. 
   IV - Actualizaci�n de hacbuild.exe para corregir el warning por falta de "xci_header_key", la cu�l no es necesaria para completar el
	proceso pero ahora se puede incorporar rellenando el archivo "header_key.txt" en ztools.
   V  - A�adida plantilla para keys.txt en la carpeta ztools
   VI - A�adido sistema de c�digos para la salida de los ficheros. Este consiste en lo siguiente:
	a) Se eliminan las tags [] de los ficheros. Para eliminar cosas como trimmed.
        b) Se eliminan los caracteres _ (m�s que nada porque no me gusta como quedan)
	c) Se a�ade las siguientes tags a la salida.
	   [xcib] xci convertido con XCI_Builder
	   [nm] "no manual", es decir se ha eliminado el manual para hacer funcionar el xci.
	   [lc] En nsp de salida: nsp de peque�o tama�o necesario para hacer funcionar el xci.

NOTA: Si se viene de una versi�n anterior sustituir las aplicaciones de ztools. Se ha actualizado hactool y se ha realizado una peque�a 
      modificaci�n en hacbuild.

v0.5.1 - v0.5.5.1 - Peque�as correcciones
v0.5.0 - Lanzamiento inicial

---------------
1. Descripci�n
---------------
Esta herramienta est� pensada para facilitar la conversi�n de archivos nsp a archivos xci.
Esta herramienta est� dise�ada en c�digo batch sirviendo de interfaz de intercambio entre los siguientes programas:
a.) hacbuild: Programa para creaci�n de archivos xci mediante archivos nca. Dise�ado por LucaFraga
https://github.com/LucaFraga/hacbuild
b.) hactool: Programa cuya funci�n es mostrar la informaci�n, desencriptar y extraer diversos tipos de archivos de datos de Nintendo Switch.
Hactool ha sido dise�ado por SciresM
https://github.com/SciresM/hactool
c.) nspBuild: Programa destinado a la creaci�n de archivos nsp a partir de archivos nca. 
nspBuild ha sido dise�ado por CVFireDragon
https://github.com/CVFireDragon/nspBuild

Aplicaci�n inspirada en "A Simple XCI, NCA, NSP Extracting Batch file (Just Drag and Drop) with Titlekey decrypt"
creada por Bigjokker y publicada en gbatemp:
https://gbatemp.net/threads/a-simple-xci-nca-nsp-extracting-batch-file-just-drag-and-drop-with-titlekey-decrypt.513300/
---------------
2. Requisitos
---------------
- Es necesario emplear un ordenador con sistema operativo windows.
- Es necesario disponer de un archivo keys.txt con las claves necesarias para el funcionamiento de hactool.
- Es necesario tener Python instalado para el funcionamiento de nspbuild
- Es necesario tener instalado al menos net frameworks 4.5.2 para el funcionamiento de hactool.
---------------
3. Funciones
---------------
- Conversi�n de archivos nsp a xci
- Obtenci�n de archivo nsp de peque�o tama�o (normalmente menos de 1mb) para la instalaci�n de la licencia del juego
- Obtenci�n de archivos game_info.ini a partir de archivos xci
- Los archivos obtenidos no incorporan partici�n update ni normal siendo m�s ligeros que un xci normal.
---------------
4. Limitaciones
---------------
- Actualmente los archivos xci solo funcionan en SX OS
- Para la carga de los archivos constru�dos hace falta tener instalada la licencia del juego (titlekey).
  Esto puede conseguirse de varias formas:
a.) Habiendo sido descargado el juego previamente v�a eshop
b.) Habiendo sido instalado previamente el nsp usado para la conversi�n en la consola. 
    (Solo hace falta que haya sido instalado previamente, no hace falta que est� instalado en la actualidad)
c.) Instalando el archivo de licencia obtenido "t�tulo_lc.nsp"
    Este nsp debe de ser instalado mediante el instalador de SX OS    
d.) Para los archivos con 5nca es necesario eliminar el manual
e.) El tiempo de procesado de los juegos de m�s de 4gb es en proporci�n m�s lento debido al fix empleado en hacbuild para darles compatibilidad.
    (Podr�a ser interesante investigar si existe una forma mejor de procesarlos)
f.) El s�mbolo "!" da fallo al ser pasado a hacbuild. Evitad usarlo de momento en el nombre de los ficheros.

-----------------------
5. Uso de la aplicaci�n
-----------------------
I.-   Para el correcto funcionamiento de la aplicaci�n introducir archivo "keys.txt" en la carpeta ztools.
      M�s informaci�n: https://github.com/SciresM/hactool
      Para ello se puede cubrir el archivo "keys_plantilla.txt", renombrar a "keys.txt" e introducir en la carpeta ztools.
II.-  La aplicaci�n crea cartuchos con los datos almacenados en game_info_preset.ini
III.- Para convertir un nsp a xci arrastrar el archivo nsp sobre "XCI_Builder_v0.6.x.bat" y esperar a que se cierre
      la consola de sistema.
IV.-  Se obtendr� una carpeta con el "nombre del archivo original". Dentro habr� dos archivos:
      - "nombre del archivo original"[xcib].xci -> Resultado de la conversi�n.
      - "nombre del archivo original"[lc].nsp -> Archivo de licencia.
V.-   Los datos del archivo game_info.ini pueden cambiarse manualmente o ser obtenidos de alg�n xci dumpeado previamente.
      > Para la obtenci�n del archivo "game_info.ini" desde un xci arrastrar el xci sobre "XCI_Builder_v0.6.x.bat".
      > Se obtendr� un archivo .ini con el nombre del juego en la carpeta game_info
      > Sustituir los datos de game_info.ini en la ra�z 
VI.-  Instalar archivo [lc].nsp con el instalador de SX OS o versiones antiguas de tinfoil para poder usar el juego xci
      obtenido en SX OS.
------------------
6. Compatibilidad
------------------
Con los cambios a�adidos y aceptando las limitaciones descritas este m�todo deber�a de ser compatible con todos los nsp actuales.
Al menos yo no he encontrado incompatibilidades.
--------------------
7. Agradecimentos a: 
--------------------
LucaFraga, SciresM y CVFireDragon 
Bigjokker de gbatemp por los consejos sobre como limpiar echos en archivos batch.
A todos los miembros de gbatemp, elotrolado.net y a mis amigos de discord ;)
