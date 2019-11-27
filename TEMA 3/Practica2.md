
Al document annexe sobre Docker, hem vist com instal·lar el servidor Subversion Edge en un contenidor. Perals exemple següents, anem a donar per fet que tenim el servidor funcionant en

```
http://localhost:18080/svn/.
```

Si accedim a la URL http://localhost:18080/viewvc a través d'un navegador web, podrem navegar através d'aquest pels diferents repositoris que tenim creats al servidor:

El paquet que ens ofereix el client de subversion, s'anomena subversion, i podem instal·lar-lo de la manerahabitual amb apt:

```
$ sudo apt install subversion
```

Si no ho heu fet encara, creeu un repositori nou al servidor, anomenat, per exemple Projecte1. Com veuremal navegador, aquest ens suggereix directament l'ordre Checkout Command com a svn co


http://localhost:18080/svn/Projecte1 --username=joamuran.


Així doncs, si llancem el checkout:


```
$ svn co http://localhost:18080/svn/Projecte1 --username=joamuran
Authentication realm: <http://localhost:18080> CollabNet Subversion
Repository
Password for 'joamuran': *********
A    Projecte1/trunk
A    Projecte1/branches
A    Projecte1/tags
Checked out revision 1.
```

Ara, si entrem dins la carpeta Projecte1, podrem anar treballant per pujar els canvis posteriorment.

De moment, anem a treballar únicament amb la branca principal trunk, on crearem un fitxer anomenatexemple1.js, amb el següent codi:


```
function saluda() {
    console.log("Hola Subversion");
}

saluda()
```

Com veiem, es tracta de codijavascriptque podrem executar des de consola ambnodejs:

```
1 $ nodejstrunk/saluda.js
2 Hola Subversion
```

Si ara, des de dins el directori on estem (Projecte1) llancem l’ordresvnst(status), obtindrem:

```
1 $ svn st
2 ?       trunk/saluda.js
```

fixeu-se que ens indica un signe d’interrogant?i la ruta al fitxertrunk/saluda.js. Açò ens indicaque aquest fitxer és nou ino està sota el control de versions.

Per afegir el fitxer al control de versions, fem ús de l’ordresvnadd, de la següent forma:

```
1 $ svn add trunk/saluda.js
2 A         trunk/saluda.js
```

Com veiem, ara, en lloc d’un?ens mostra unaA, que indica quehem afegit aquest fitxer al controlde versions, però encara no l’hem pujat al servidor.

Si fem de nou unsvnst, veurem que ens indica la mateixa línia. Per tal de pujar els canvis al servidor,haurem de fer uncommit, ambsvnci, de la següent manera:

```
1 $ svnci-m"Afegintelfitxersaluda.js"
2 Authenticationrealm: <http://localhost:18080>CollabNetSubversion

Repository

3 Passwordfor'joamuran': *********
4
5 Adding      trunksaluda.js
6 Transmittingfiledata.done
7 Committing transaction...
8 Committedrevision 2.
```

Actualizem la nostra carpetaper si altre usuari ha pujat canvis, només haurem de fer unupdateambsvnup. Sempre serà unabona pràctica fer aquesta operació abans de posar-nos a fer qualsevol modificació.


```
1 $ svn up 
2 Updating '.':
3 Authentication realm: <http://localhost:18080> CollabNet Subversion 
    Repository
4 Passwordfor'joamuran': *********
5 
6 Atrunk/prova.txt
7 Updatedtorevision4.
```
