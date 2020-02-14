### 1. Descàrrega i instal·lació de VS Code

***Instal·lació de code a Ubuntu***

Tal i com es descriu a la documentació, podem obtenir VS Code des del mateix repositori de Microsoft. Per a això seguirem els passos següents. Potser siga necessari instal·lar prèviament el paquet curl:

1 Obtenim la clau GPG amb la que estan signats els paquets de MS i la incorporem al sistema (si no tenim instal·lat prèviament el paquet curl caldrà instal·lar-lo amb sudo apt-get install curl):


```
$ curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
$ sudo install -o root -g root -m 644 packages.microsoft.gpg /usr/share/keyrings/
```

2 Creem el fitxer vscode.list dins la carpeta de fonts de programari del sistema amb la línia referent al repositori de VSCode:


```
$ sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
$ sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
```

3 Ara només ens quedarà actualitzar la memòria caché de paquets i instal·lar VSCode amb:


```
$ sudo apt-get install apt-transport-https
$ sudo apt-get update
$ sudo apt-get install code
```

### 2. Instal·lació de plugins en VSCode

***Extensioons markdown***

Veurem que ens apareix gran quantitat d'extensions per a Markdown. Podeu donar un cop d'ull a totes elles, però de moment, instal·larem l'extensió markdownlint, que ens ajuda a comprovar la correcta sintaxi del codi Markdown i ens ofereix la possibilitat de previsualitzar el resultat al temps que escrivim. Per a això, només haurem de **fer click en el botó Install que apareix bé al costat de l'extensió o en la descripció d'aquesta`. Si ho desitgeu, podeu instal·lar també l'extensió Markdown PDF que us permet guardar els fitxers creats en format md a pdf.

Per tal de començar a treballar amb algun exemple, podem anar a l'activitat de l'Explorador de fitxers i prémer el botó Open Folder per tal d'obrir una carpeta de treball, o fer-ho directament a través del menú File > Open Folder.


### 3. Comprovació de l'entorn

Per a vore la versio:

```
$ javac -version
```

O si no en tenim cap, se'ns avisarà dels diferents paquets que ens ofereixen l'eina, és a dir, dels diferents JDKs que tenim disponibles, i com instal·lar-los:


```
Command 'javac' not found, but can be installed with:

sudo apt install default-jdk
sudo apt install openjdk-11-jdk-headless
sudo apt install ecj
sudo apt install openjdk-8-jdk-headless
sudo apt install openjdk-9-jdk-headless
```

### 4. Instal·lació de les extensions bàsiques de Java per a VSCode

Per tal d'instal·lar el suport per a Java en VSCode, farem clic al botó de l'activitat d'extensions per obrir de nou l'Extension Marketplace, que ens mostrarà de nou llistats d'extensions recomanades i d'extensions populars.

Busquem ara l'extensió java extension pack i l'instalarem.


### 5. Configuració de l'entorn

Com hem comentat, VSCode és àmpliament personalitzable, a través d'un fitxer de configuració en format JSON. A més, ens permet establir dos àmbits diferents per a la configuració:

Ajustos d'usuari, que s'apliquen de forma global a totes les instàncies de VSCode que llancem amb el nostre usuari, i
Ajustos de l'espai de treball, associats dins de cada espai de treball, i només aplicable a aquest. En cas que tinguem definits ajustos d'usuari i de l'espai de treball, aquests últims sobreescriuran els de l'usuari.

Per tal d'accedir als ajustos, ho fem a través de File > Preferences > Settings, o bé mitjançant Ctrl+,, o amb la paleta d'ordres, accessible amb Ctrl+Shift+P i buscant Preferences: Open User Settings o Preferences: Open Workspace Settings.

Podem veure aquesta finestra de configuració a la figura \label{settings_1}.

Ajustos

En versions anteriors se'ns presentava directament el fitxer JSON de configuració. En les últimes actualitzacions de VSCode, ja ens ofereix una interfície més amigable per tal de modificar les preferències, ordenades en diverses seccions.

Com veiem, a la part superior disposem d'una barra per filtrar ajustos, i a sota les preferències que podem modificar, ordenades per seccions. A la imatge, de moment, només veiem les preferències de l'usuari (User), però si tinguérem un espai de treball obert, també se'ns mostrarien les preferències d'aquest Workspace.

Si desitgem veure directament el fitxer JSON de configuració, haurem de fer clic a la pestanya corresponent (veieu figura \label{settings_1}). Aquest fitxer està compost de parells \"clau\":\"valor\", separats per comes, i tancats entre claus { }. Els valors, a més de valors simples (cadenes o números), també poden ser llistes de valors, tancats entre claudàtors [], o bé altre conjunt de parells \"clau\":\"valor\", tancats també entre claus { }. Més endavant veurem en detall aquest format, però veiem un exemple autoexplicatiu de fitxer de configuració en aquest format:


```
{
    "languageTool.language": "ca",
    "[markdown]": {
        "editor.tabSize": 2
    },
    "markdown-toc.depthFrom": 2,
    "markdown-toc.depthTo": 3,
    "window.zoomLevel": 0,
    "editor.wordWrap": "on",
    "markdown.styles": [
        "CustomMDStyles.css"
    ],
    "java.home": "/usr/lib/jvm/openjdk-11"
}
```

Com veiem, tenim:

diferents atributs en forma clau : valor, com \"editor.wordWrap\":\"on\", per activar la separació de línies en arribar al final de l'editor;
Atributs en clau : llista de valors, com \"markdown.styles\", i
Atributs en forma clau : llista de parells clau:valor, com el cas de \"[markdown]\".

Com hem comentat, poc a poc anirem familiaritzant-nos amb aquest format. De moment, anem a buscar a la barra superior l'ajust java.home (figura \ref{settings_2})


***Configuració del JDK***

Com veiem, aquesta opció no es pot editar directament, i ens indica que ho fem de fer a través del fitxer JSON de configuració. Si fem clic en Edit in Settings, obrirem aquest fitxer, i indicarem a la propietat java.home el directori on tenim el nostre JDK. Per al cas de l'OpenJDK 11 serà:


```
{
    "java.home": "/usr/lib/jvm/java-11-openjdk-amd64"
}
```

Amb açò hem modificat el fitxer de preferències d'usuari. Per tal que els canvis tinguen efecte, haurem de guardar el fitxer (File > Save o directament Ctrl+s), i reiniciar el component Java Language Server, tal i com se'ns indicarà quan guardem el fitxer.

Podeu trobar més informació sobre els ajustos a la web de VSCode:

https://code.visualstudio.com/docs/getstarted/settings


### 6. Hola VSCode. Un passeig per l'editor. Depuració

Anem ja a posar-nos mans en l'obra, i veure una adaptació del clàssic Hola Món en VSCode.

Per a això, creem una carpeta per als exemples de java i un fitxer a dins anomenat HelloVSC.java:


```
ExemplesJava
  `-- HelloVSC.java
```

Per tal d'obrir la carpeta, si hem tancat totes les pestanyes obertes, i no tenim res obert, tindrem disponible un botó amb el text Open Folder per obrir-la. També podem obrir la carpeta directament a través del menú File > Open Folder.

Una vegada tinguem la carpeta oberta, la veurem a l'explorador de fitxers. Si passem el ratolí per damunt, veurem que apareixen unes icones, per tal de crear nous fitxers dins la carpeta, noves carpetes, refrescar el contingut o col·lapsar la jerarquia de carpetes que tinguem expandides a la finestra. Per crear el nou fitxer, farem clic a la icona de New File, i indicarem el nom del nou fitxer (HelloVSC.java):

També podrem crear un fitxer nou a través de File > New File, o bé amb Ctrl+N, tenint en compte que haurem d'indicar el nom del fitxer i la seua ubicació posteriorment.

El contingut de HelloVSC.java és el clàssic de l'Hola Món, amb dos escriptures per pantalla.


```
public class HelloVSC {

    public static void main(String[] args) {
        System.out.println("Hola Visual Studio Code!");
        System.out.println("Estem provant un nou editor!");
    }

}
```

Execució i Depuració

Per tal d'executar el nostre programa, seleccionarem Debug > Start Without Debugging, o bé premerem Ctrl+F5. Si volem depurar-lo, ho fem amb Debug > Start Debugging, o directament amb F5.

Una vegada iniciada la depuració, disposarem del resultat al panell de la consola de depuració (Debug Console), amb el corresponent resultat:

...
Hola Visual Studio Code!
Estem provant un nou editor!

Si no ens apareix aquest panell directament, podem activar-lo, des de la barra lateral en l'activitat de depuració, fent clic en la icona de la consola, situada a la dreta.

Per altra banda, veurem que a la jerarquía de fitxers se'ns ha creat una nova carpeta anomenada .vscode, amb un fitxer launch.json a dins. Aquest fitxer el crea l'extensió de depuració de Java, i conté informació per a la depuració.
Establint Breakpoints

VSCode ens permet establir punts de ruptura en el codi. Per a això, disposem d'una columna, que ens permet establir els punts fent clic al costat esquerre del número de línia corresponent.

Quan fem clic, veurem com apareix un punt roig marcant el breakpoint. Ara podrem executar el codi en mode depuració (F5) i veure quin és l'efecte que té. Ho podem veure a la figura \ref{debug_1}

Depuració

A més, si ens ubiquem damunt d'aquesta columna de l'esquerra dels números de línia i fem clic amb el botó dret del ratolí, ens apareixerà un menú contextual amb tres opcions, en funció de si ja tenim un breakpoint a la línia o no:

Si la línia ja disposa d'un Breakpoint, podem:
Eliminar el Breakpoint
Editar el Breakpoint
Desactivar el breakpoint

En canvi, si la línia no té cap breakpoint, podem:
Afegir un breakpoint
Afegir un breakpoint condicional
Afegir un breakpoint de log

Si volem afegir un punt de ruptura condicional, només hem de seleccionar l'opció d'afegir el breakpoint o editar-lo. En estos moments, ens demanarà una expressió condicional. L'escrivim i polsem Enter per a que els canvis tinguen efecte (figura \ref{debug_2}).

Breakpoints condicionals

Fet açò, si tornem a depurar, veurem com atura l'execució en el moment que es compleix l'expressió que li hem indicat. Veiem un exemple més complet a la (figura \ref{debug_3}).

Breakpoints condicionals 2

I finalment, recordar, que a la part de l'esquerra, tenim disponibles les finestres que ens mostren l'estat de la variable en el punt de ruptura que hem establert (Secció Variables), o bé que indiquem explícitament (Watch) (figura \ref{debug_4}).

Estat de les variables
Execució des de consola

Per altra banda, també cal destacar que podem compilar i llançar el nostre programa java des de la pròpia terminal integrada en VSCode o la terminal del sistema, com podem veure a la figura \ref{debug_5}.

Execució des de consola

Si voleu més informació sobre la depuració en Java podeu trobar-la a:

https://code.visualstudio.com/docs/editor/debugging