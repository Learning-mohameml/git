# cour : **``Rebase``**

## 1. Introduction 
- **Definiton :**

>En Git, la commande `git rebase` est utilisée pour remanier l'historique des commits. Contrairement à la fusion (`git merge`), qui crée un commit de fusion pour intégrer les changements de différentes branches, le rebase réapplique séquentiellement chaque commit d'une branche sur une autre.


- **exemple:**

Avant le rebase :
```
A---B---C  (branche cible)
     \
      D---E---F  (branche source)
```

Après le rebase :
```
A---B---C---D'---E'---F'  (branche cible, branche source réappliquée)
```

Dans cet exemple, les commits `D`, `E`, et `F` ont été réappliqués séquentiellement sur la branche cible, créant de nouveaux commits `D'`, `E'`, et `F'`.

Il est important de noter que le rebase peut être une opération sensible, en particulier sur des branches partagées. Il est recommandé de l'utiliser avec précaution .


## 2 . **la commande ``git rebase `` :**

- **syntaxe :**
```bash
git rebase <nom_branche>
```
La commande `git rebase` est utilisée pour remanier l'historique des commits. Voyons comment utiliser `git rebase` avec un exemple simple :

- **Exemple:**

Supposons que nous sommes dans la situation où nous avons deux branches, `master` et `feature`, et nous voulons réappliquer les commits de `feature` sur `master`. 

```bash
# Créer une branche "feature" et effectuer des commits
git checkout -b feature
echo "Commit 1" > fichier.txt
git add fichier.txt
git commit -m "Commit 1"
echo "Commit 2" >> fichier.txt
git add fichier.txt
git commit -m "Commit 2"

# Revenir à la branche "master"
git checkout master
echo "Commit 3" >> fichier.txt
git add fichier.txt
git commit -m "Commit 3"
```

À ce stade, notre historique ressemble à ceci :

```
master:  A---B---C
                  \
feature:           D---E
```

Ensuite, nous voulons réappliquer les commits de `feature` sur `master` :

```bash
# Aller sur la branche "feature"
git checkout feature

# Réappliquer les commits de "feature" sur "master"
git rebase master
```

À ce stade, si tout se passe bien, Git aura réappliqué les commits de `feature` sur la branche `master`. L'historique pourrait ressembler à ceci :

```
master:  A---B---C
                  \     \
feature:           D'---E'
```

Cependant, pour mettre à jour la branche `master` avec ces changements, nous devons basculer vers `master` et fusionner avec `feature` :

```bash
# Aller sur la branche "master"
git checkout master

# Fusionner avec la branche "feature"
git merge feature
```

L'historique final serait alors :

```
master:  A---B---C---D'---E'
```

Maintenant, la branche `master` a été mise à jour pour inclure les changements de la branche `feature`, et l'historique est resté linéaire grâce au rebase.