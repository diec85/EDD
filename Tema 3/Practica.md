# Practica 2

## Sistemes de control de versio


Exercici.

Realitzeu les següents operacions amb rcs:

1.Creeu un fitxer anomenat exercici.md, i afegiu-li algun contingut en format Markdwon.
2.Registreu el fitxer per a que el controle RCS.
3.Intenteu modificar el fitxer, per veure si teniu o no permís.
4.Feu uncheckoutdel fitxer, ara sí, per afegir canvis.
5.Modifiqueu el fitxer i afegiu-li més contingut. Aquesta serà la versió 1.2.
6.Amb un altre usuari, intenteu modificar el fitxer (fent el checkout abans).
7.Com a l’usuari original, registreu els canvis al fitxer.
8.Amb l’altre usuari de nou, intenteu ara modificar el fitxer (també fent un checkout).
9.Si podeu, afegiu més informació al fitxer, ara serà la versió 1.3.
10.Com a l’usuari original, visualitzeu les diferències entre les versions, i torneu a la versió 1.2.
11.Apliqueu més canvis i guardeu-los amb la versió 1.4


En primer lloc, caldrà instal·lar els paquets rcs i rcs-blame:

```
1 sudo apt-get install rcs rcs-blame
```

Anem a crear, dins un directori de treball un fitxer anomenat exercici.md, amb el següent contingut:

```
1 Fitxer,versió 1
```

El guardem i eixim. Si feu un ls -l veureu que disposem els permisos habituals (rw-rw-r–)sobre elfitxer:

```
1-rw-rw-r-- 1 alumne a lumne 0 ’doct18 06:23 exercici.md
```

El primer que haurem de fer per tal de portar un control de versions sobre aquest fitxer seràregistrar-lo (check in)al sistema de control de versions. Per a això farem:

```
1 $ ci -u exercici.md
2 exercici.md,v <-- exercici.md 3 enterdescription,terminated with single '.' or end of file: 4 NOTE: This is NOT the log message!
5 >> v1
6 >> .
7 initial revision: 1.1
8 done
```

Com veiem, hem fet ús de l’ordreci, que significacheck-in, i ens serveix exactament per això, perindicar que el fitxer va a estar sota el control de versions.I com sap RCS que el fitxer ara està sota el control de versions? Si tornem a fer unls-lsobre eldirectori de treball, ens trobem:

```
1 $ ls -l
2 total 8
3 -r-xr-xr-x 1 alumne a lumne 18 oct 18 06:23 exercici.md
4 -r-xr-xr-x 1 alumne a lumne 200 oct 18 06:25 exercici.md,v
```

Fixeu-vos en dos detalls:

El fitxer original ara ja no té permís de lectura

S'ha creat un fitxer nou, anomenat exercici.md,v, amb els mateixos permisos que té ara l'original.

Fixeu-vos que quan hem fet el check-in, ens indica la generació d'un fitxere de control de versions exercici.md,v i a més ens ha demanar posar una descripció. Recordeu que per finalitzar d'escriiure ladescripció hem d'escriure una línia amb un únic punt. Aquesta descripció s'inclourà també dins el fitxerde control de versions.

Bé, vist açò, veiem què fa RCS per marcar el control de versions. Quan registrem un fitxer en RCS, aquestpot fer dues coses per recordar a l'usuari que el fitxer es troba sota el control de RCS


Elimina el fitxer original, deixant només el fitxer sota control de RCS. Aquest nou fitxer sota el controlde versions s'anomena per defecte com l'original, i s'acaba amb ,v. Generalment, es conservarà almateix directori que l'original, sempre i quan no tinguem creada una carpeta en el mateix directorianomenada RCS (creada per l'usuari); en eixe cas, es guardaria en esta carpeta.A més, si fem ús de l'opció -u, torna a revisar el fitxer (no l'esborra), però deixa els seus permissoscom a només lectura.


Aleshores, com modifiquem un fitxer sota control de versions si és només de lectura? Per a això hem de ferun check out del fitxer, amb:


```
$ co -l ./exercici.md
./exercici.md,v  -->  ./exercici.md
revision 1.1 (locked)
done
```

Fixeu-se ara que al fer el co ens ha indicat que tenim un nou exercici.md a partir del fitxer exercici.md,v,i si tornem a llistar la carpeta:


```
$ ls -l
total 8
-rwxr-xr-x 1 alumne alumne  18 oct 18 06:55 exercici.md
-r-xr-xr-x 1 alumne alumne 212 oct 18 06:55 exercici.md,v
```

Veurem com disposem de permís de lectura sobre el exercici.md. L'opció -l (lock) de co ens serveix perbloquejar el fitxer, de manera que altre usuari del sistema no el puga modificar mentre estem fent els canvis.Si fem ara un cop d'ull al fitxer de control de versions podreu deduïr alguna informació d'interès, com lesdiferents revisions que s'han anat fent, o quin usuari té el fitxer bloquejat.Una vegada fet el checkout, podem modificar el fitxer de nou, per exemple amb el següent contingut:


```
Fitxer, versió 1

Afegim més text al fitxer, per veure com ho gestiona el RCS.
```


Com veiem, hem afegit una línia més. Ara per indicar a RCS que hem acabat de fer canvis per a aquestanova versió, i que desbloquege el fitxer. Per a això, farem de nou un check-in:


```
$ ci -u ./exercici.md
./exercici.md,v  <--  ./exercici.md
new revision: 1.2; previous revision: 1.1
enter log message, terminated with single '.' or end of file:
>> Segona versió del fitxer
>> .
done
```

Amb el que ja tindrem de nou el fitxer sense permís d'escriptura. Si donem un cop d'ull al exercici.md,v,veurem com han aparegut més canvis. Aquest fitxer, anirà guardant de forma eficient les modificacions cadavegada que es fa el registre o check-in del fitxer, i té un número de revisió, que guarda junt als comentarisque afegim a cadascuna.A partir d'aquesta informació, disposem d'eines per tal de revisar els canvis realitzats. Per fer això, disposemde l'ordre rlog. Veiem el resultat d'aplicar-la sobre el nostre fitxer:


```
$ rlog ./exercici.md

 RCS file: ./exercici.md,v
 Working file: ./exercici.md
 head: 1.2
 branch:
 locks: strict
 access list:
 symbolic names:
 keyword substitution: kv
 total revisions: 2; selected revisions: 2
 description:
 v1
 ----------------------------
 revision 1.2
 date: 2019/10/18 05:11:05;  author: alumne;  state: Exp;  lines: +2 -0
 Segona versió del fitxer
 ----------------------------
 revision 1.1
 date: 2019/10/18 04:24:55;  author: alumne;  state: Exp;
 Initial revision
 ===========================================================================
 ==
```

Ara, si volem veure l'estat d'una versió concreta, farem ús de co -p x.y fitxer, sent x.y el número deversió. Per exemple, per veure les dues revisions del fitxer, tenim:

```
$ co -p1.1 ./exercici.md 
./exercici.md,v  -->  standard output
revision 1.1
Fitxer, versió 1
```

```
$ co -p1.2 ./exercici.md 
./exercici.md,v  -->  standard output
revision 1.2
Fitxer, versió 1

Afegim més text al fitxer, per veure com ho gestiona el RCS.
```

Si ara el que volem és veure les diferències entre les dues versions, fem ús de rcsdiff.


```
$ rcsdiff -r1.1 -r 1.2 ./exercici.md
 rcsdiff: RCS/1.2,v: No such file or directory
 ===================================================================
 RCS file: ./exercici.md,v
 retrieving revision 1.1
 retrieving revision 1.2
 diff -r1.1 -r1.2
 1a2,3
 >
 > Afegim més text al fitxer, per veure com ho gestiona el RCS.
 ```

 Com veiem, el que fa internament és utilitzar un diff entre les dues versions del fitxer.
 
 Finalment, si el que volem és tornar a una versió anterior del fitxer, només haurem de fer un check out amb elnúmero de revisió concret:
 
 Tenint la versió 1.2 del fitxer:


```
$ cat exercici.md
Fitxer, versió 1

Afegim més text al fitxer, per veure com ho gestiona el RCS.
```

Revertim a la versió 1.1:


```
$ co -r1.1 ./exercici.md 
./exercici.md,v  -->  ./exercici.md
revision 1.1
done

$ cat exercici.md
Fitxer, versió 1
```