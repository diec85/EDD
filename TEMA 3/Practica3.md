### Instal·lació

Per tal d’instal·largiten un sistema Ubuntu, ho fem a travès d’apt:

```
1 sudo apt update
2 sudo apt install git 
```

Per saber la versió que tenim intal·lada fem ús de git --version.

### Ajuda en git

```
git help ordre
```
3.5.2. Creació d’un fitxer nou:
### Configuració inicial


Identitat de l’usuari, que es compon del nom i el correu electrònic.

```
1 $ gitconfig-- global user.name "Diego"
2 $ gitconfig-- global user.email diec85@hotmail.es
```

Editor per defecte

```
1 diec85@diec85:~$ git config--global core.editor nano
```

Per a que utilitze l’eixida en colors significatius:

```
1 $ git config --global color.ui true
```

Per indicar a git que realitze conversions entre finals de línia quan treballem en entorns híbridsLinux/Windows/Mac:

```
1 git config --global core.autocrlf true
```

```
1 git config --list
```


### Creació i inicialització del projecte i el repositori


Ens situem en el directori on anem a guardar els projectes, i creem la carpeta del projece amb:

```
1 $ mkdir projecte
```

Ara ens ubiquem dins d`ell:

```
1 cd projecte
```

I inicialitzem aci el repositori:

```
1 git status
```

Git ens dirà que ha inicialitzat un repositori buït.Si volem veure l’estat de git, farem:

```
1 git status
```

I veurem el següent missatge:


```
1 On branch master
2 
3 No commits yet 
4 
5 nothing to commit (create/copy files and use "gitadd" to track)
```

### Creació d’un fitxer nou:

```
1 $ touch exercici.md
```

Amb açò hem creat un fitxer buit.


### Fer el seguiment del fitxer


Per tal de marcar el fitxer per a que git en faça el seguiment, farem:


```
1 $ git add exercici.md
```

#### Fent el commit del fitxer

Per afegir, ara sí, el fitxer al repositori, fem el nostre primer commit:


```
1 git commit -a -m "Exercici tema 3"
2 [master (root-commit) 46c5f91] primer commit 
3 1 file changed, 0 insertions(+), 0 deletions(-)
4 create mode 100644 exercici.md
```

Fem un git ststus:

```
1 $ git status 
2 On branch master 
3 nothing to commit, working tree clean
```

### Esborrant fitxers

En primer lloc, anem a crear, dins el repositori dos fitxers per esborrar postariorment:

```
1 $ touch tmp1.md
2 $ touch tmp2.md
```

Ara els afegim:

```
1 $ git add .
```

Ara fem el commit:

```
1 $ git commit -a -m "fitxersdeprova"
2 [master fb3bcef] fitxersdeprova
3 2 files changed, 0 insertions(+), 0 deletions(-)
4 create mode 100644 tmp1.md
5 create mode 100644 tmp2.md
```

Esborrar-lo en local i després engit:

```
1 $ rm tmp1.md
```

Ara el status a canviat a deleted


Ara fem un:

```
1 $ git rm tmp1.md
```

Ara fem el commit amb el fitxer esborrat:


```
1 $ git commit -a -m "Esborrat tmp1.md" 
2 [master5e3b2e1] Esborrat tmp1.md 
3 1 file changed, 0 insertions(+), 0 deletions(-)
4 delete mode 100644 tmp1.md
```


### Movent fitxers

En primer lloc, creem un fitxer, l’afegim al control de versions i el pugem al repositori:

```
1 $ touch mv1.md 
2 $ git add mv1.md 
3 $ git commit -a -m "Afegitmv1.md" 
4 [masterb063c63] Afegitmv1.md 
5 1 file changed, 0 insertions(+), 0 deletions(-)
6 rename tmp2.md => mv1.md (100%)
```

Ara, per moure el fitxer, farem ús de git mv:

```
1 $ git mv mv1.md mv1_renomenat.md 
2 $ git status 
3 On branch master 
4 Changes to be committed:
5  (use "git reset HEAD <file>..." to unstage)
6 
7     renamed:    mv1.md -> mv1_renomenat.md
```

 Només ens queda doncs, pujar-lo:


 ```
 1 $ git commit -a -m "Renomena tmv1.md a mv1_renomenat.md" 
 2 [master 3ec28c1]Renomenat mv1.md a mv1_renomenat.md
 3  1 file changed, 0 insertions(+), 0 deletions(-)
 4 rename mv1.md => mv1_renomenat.md (100%)
 ```

### Altres aspectes d’interès

Veiem un exemple d’aquest tipus de fitxer.gitignore:

```
1 # Ignora els fitxers amb nom temporal_6.txt i temporal_7.zio 
2 temporal_6.txt 
3 temporal_7.zip 
4 
5 # Ignora tots els fitxers amb extensió zip,gz,changes o deb:
6 *.zip
7 *.gz
8 *.changes
9 *.deb
10
11 # Ignora tots els fitxers amb extensió.log de la carpeta log, així
12 # com les extensions .log0, .log1, log2...
13 log/*.log
14 log/*.log[0-9]
15
16 # Ignora tots els fitxers del directori imatges
17 imatges/*
18 19 # Ignora tots els fitxers que acaben en 'a' o 'o' de la carpeta 
    compilats
20 compilats/*[ao]
```

### Altres operacions

Revertir a l’estat d’uncommit:

```
1 git revert SHA_DEL_COMMIT_A_REVERTIR
```

Veiem el llistat de commits:

```
1 $ git log --oneline
2    3ec28c1 (HEAD->master)Renomenat mv1.md a mv1_renomenat.md 3 b063c63 Afegit mv1.md 
4 5e3b2e1 Esborrat tmp1.md
5 fb3bcef Afegits dos fitxers de prova 
6 46c5f91 primer commit
```

Revertim el commit5e3b2e1:


```
1 $ git revert 5e3b2e1
```

Eliminar fitxers no seguits:

```
1 $ git clean -f
```

Amb aquesta ordre eliminem tots els fitxers del directori de treball que no estan sent seguits per git.Si a més volem que esborre també els directoris no seguits, farem:

```
1 $ git clean -f -d
```

### Clonat de repositoris: Github

En general, per tal de clonar un projecte farem:

```
1 git clone URL [directori]
```

Així, per exemple, si volem clonar un repositori que es troba en una carpeta del nostre mateix equip,farem

```
1 $ git clone exemple_inicial/projecte exemple_inicial/projecte2
```