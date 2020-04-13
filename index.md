---
title: "Matrices - Array - Dataframe"
author: "Mohamed Essaied Hamrita, PhD"
date: "13/04/2020"
output: 
  html_document: 
    code_folding: hide
    fig_width: 5
    highlight: tango
    theme: simplex
    keep_md: yes
    toc: yes
    toc_float: yes
---




## Matrices
Les matrices sont les objets R dans lesquels les éléments sont disposés selon une disposition rectangulaire à deux dimensions. Ils contiennent des éléments de **<span style="color: red;">mêmes types atomiques</span>**. Nous utilisons des matrices contenant des éléments numériques à utiliser dans les calculs mathématiques.
La syntaxe de base pour créer une matrice est:


```r
matrix(data, ncol, nrow, byrow)
```

Où les arguments sont décrit comme suit:
- data: un vecteur (nmérique, ou caractère ou logique)
- ncol: un nombre représentant le nombre des colonnes
- nrow: un nombre représentant le nombre des lignes
- byrow: c'est une valeur logique (TRUE si le remplissage se fait ligne par ligne et FALSE (par défaut) sinon.



```r
# Exemple 1:
matrix(1:12,ncol=3,nrow=4) # remplissage par colonnes
```

```
     [,1] [,2] [,3]
[1,]    1    5    9
[2,]    2    6   10
[3,]    3    7   11
[4,]    4    8   12
```


```r
# Exemple 2:
matrix(1:12,ncol=3,nrow=4, byrow=T) # remplissage par lignes
```

```
     [,1] [,2] [,3]
[1,]    1    2    3
[2,]    4    5    6
[3,]    7    8    9
[4,]   10   11   12
```


```r
# définir des noms pour les colonnes et les lignes
M1=matrix(1:12,ncol=3,nrow=4) 
colnames(M1)=c("x1","x2","x3")
rownames(M1)=c("l1","l2","l3","l4")
M1
```

```
   x1 x2 x3
l1  1  5  9
l2  2  6 10
l3  3  7 11
l4  4  8 12
```

On peut aussi créer une matrice en utilisant cbind() ou rbind()



```r
xx1=c(1,4,5); xx2=c(2,7,1)
(matx=cbind(xx1,xx2))
```

```
     xx1 xx2
[1,]   1   2
[2,]   4   7
[3,]   5   1
```

```r
(matxxt=rbind(xx1,xx2))
```

```
    [,1] [,2] [,3]
xx1    1    4    5
xx2    2    7    1
```

### Accès aux éléments d'une matrice
Les éléments d'une matrice sont accessibles en utilisant l'index de la ligne et de la colonne de l'élément.



```r
M1[2,3]  # extraire l'élément de la 2ieme ligne et 
```

```
[1] 10
```

```r
# la 3ieme colonne
M1[,2] # extraire la deuxième colonne
```

```
l1 l2 l3 l4 
 5  6  7  8 
```

```r
M1[-1, 2:3] # extraire la 2ieme et la 3ieme colonne privé 
```

```
   x2 x3
l2  6 10
l3  7 11
l4  8 12
```

```r
 # de la première ligne.
```

### Opérations sur les matrices
Diverses opérations mathématiques sont effectuées sur les matrices à l'aide des opérateurs R. Le résultat de l'opération est également une matrice.
Les dimensions (nombre de lignes et de colonnes) doivent être identiques pour les matrices impliquées dans l'opération.

### Addition, soustraction, multiplication et division
Les opérateurs +, -, * et / font, respectivement, l'addition, la soustraction, la multiplication et la division **<font color=red>terme à terme</font>**. Donc les matrices, dans ce cas, doivent être de mêmes dimensions.



```r
(A=matrix(c(-2,1,0,4),2,2))
```

```
     [,1] [,2]
[1,]   -2    0
[2,]    1    4
```

```r
(B=matrix(c(4,-1,7,3),2,2))
```

```
     [,1] [,2]
[1,]    4    7
[2,]   -1    3
```

```r
A+B  # addition
```

```
     [,1] [,2]
[1,]    2    7
[2,]    0    7
```
#### soustraction
A-B
```

```r
# Multiplication
A*B
```

```
     [,1] [,2]
[1,]   -8    0
[2,]   -1   12
```


```r
# Division
A/B
```

```
     [,1]     [,2]
[1,] -0.5 0.000000
[2,] -1.0 1.333333
```

### Calcul matriciel

* La transposée d'une matrice se fait à l'aide de l'instruction *t()*.
* Le produit matriciel se fait par la commande *%*%*.
* La fonction *det()* renvoie le déterminant.
* La fonction *diag(arg)* donne la diagonale si l'argument (arg) est une matrice et crée une matrice diagonale si l'argument (arg) est un vecteur.
* La fonction *solve()* a double rôle:
  * solve(A) donne l'inverse de la matrice A
  * solve(A,b) donne la solution du système AX=b



```r
# transposée
t(A)
```

```
     [,1] [,2]
[1,]   -2    1
[2,]    0    4
```

```r
# Produit matriciel (noter qu'il faut ncA=nrB)
A%*%B
```

```
     [,1] [,2]
[1,]   -8  -14
[2,]    0   19
```


```r
det(A) # déterminant
```

```
[1] -8
```

```r
diag(A) # extraire la diagonale de A
```

```
[1] -2  4
```

```r
diag(c(2,8,7)) # créer une matrice diagonale
```

```
     [,1] [,2] [,3]
[1,]    2    0    0
[2,]    0    8    0
[3,]    0    0    7
```

```r
# noter que la trace est déduite à l'aide sum(diag(mat))
sum(diag(A)) # la trace de A
```

```
[1] 2
```

```r
solve(A) # l'inverse de A
```

```
       [,1] [,2]
[1,] -0.500 0.00
[2,]  0.125 0.25
```

```r
solve(A, c(-2,1))
```

```
[1] 1 0
```

### Vecteurs et valeurs propres
La fonction *eigen(mat)* renvoie une liste comprenant les valeurs et les vecteurs propres de la matrice *mat*.



```r
eig=eigen(A)
eig$values  # valeurs propres
```

```
[1]  4 -2
```

```r
eig$vectors # vecteurs propres
```

```
     [,1]       [,2]
[1,]    0  0.9863939
[2,]    1 -0.1643990
```
## Array
Les tableaux (array) sont les objets de données R qui peuvent stocker des données dans plus de deux dimensions. Par exemple - Si nous créons un tableau de dimensions (2, 3, 4), cela crée 4 matrices rectangulaires chacune avec 2 lignes et 3 colonnes. Les tableaux peuvent stocker uniquement le type de données.

Un tableau est créé à l'aide de la fonction array (). Il prend des vecteurs en entrée et utilise les valeurs du paramètre dim pour créer un tableau.



```r
vect1 <- c(5,9,3)
vect2 <- c(10,11,12,13,14,15)

result <- array(c(vect1,vect2),dim = c(3,3,2))
result
```

```
, , 1

     [,1] [,2] [,3]
[1,]    5   10   13
[2,]    9   11   14
[3,]    3   12   15

, , 2

     [,1] [,2] [,3]
[1,]    5   10   13
[2,]    9   11   14
[3,]    3   12   15
```

```r
result[,1,1]
```

```
[1] 5 9 3
```

```r
result[1,1,]
```

```
[1] 5 5
```
## Data frames
Une data frame est une table ou une structure de type tableau à deux dimensions dans laquelle chaque colonne contient les valeurs d'une variable et chaque ligne contient un ensemble de valeurs de chaque colonne.
Une data frame se caractérise par:
* Les noms des colonnes **ne doit pas être vide**.
* les noms des lignes doivent être uniques.
* les données stockées dans une data frame de données peuvent être de type numérique, facteur, logique ou caractère.
* chaque colonne doit contenir le même nombre d'éléments de données.
Considérons le tableau des données suivant:

| Noms    | Genre | Age | Taille (cm) | Poids (Kg) |
|---------|:-----:|-----|:-----------:|:----------:|
| Youssef |   M   | 8   |     100     |     35     |
| Selma   |   F   | 4   |      60     |     21     |
| Khaled  |   M   | 40  |     172     |     81     |
| Sarra   |   F   | 12  |     120     |     42     |



```r
Noms=c("Youssef", "Selma", "Khaled", "Sarra")
Genre=c("M", "F", "M", "F")
Age=c(8,4,40,12)
Taille=c(100,60,172,120)
Poids=c(35,21,81,42)
(tab1=data.frame(Noms=Noms, Genre=Genre,
                 Taille=Taille, Poids=Poids, stringsAsFactors = FALSE))
```

```
     Noms Genre Taille Poids
1 Youssef     M    100    35
2   Selma     F     60    21
3  Khaled     M    172    81
4   Sarra     F    120    42
```

`str()` renvoie la structure de l'objet. La fonction `summary()` donne un résumé statistique du tableau des données (min, max, mean, etc)



```r
str(tab1)
```

```
'data.frame':	4 obs. of  4 variables:
 $ Noms  : chr  "Youssef" "Selma" "Khaled" "Sarra"
 $ Genre : chr  "M" "F" "M" "F"
 $ Taille: num  100 60 172 120
 $ Poids : num  35 21 81 42
```


```r
summary(tab1)
```

```
     Noms              Genre               Taille        Poids      
 Length:4           Length:4           Min.   : 60   Min.   :21.00  
 Class :character   Class :character   1st Qu.: 90   1st Qu.:31.50  
 Mode  :character   Mode  :character   Median :110   Median :38.50  
                                       Mean   :113   Mean   :44.75  
                                       3rd Qu.:133   3rd Qu.:51.75  
                                       Max.   :172   Max.   :81.00  
```

L'accés aux éléments du tableau des données de classe `data.frame` se fait de diverses façons. On peut accéder aux éléments d'une `data.frame` de la même manière comme les matrices (puisque une `data.frame` est un tableau à deux dimensions). 



```r
tab1[1,3]  
```

```
[1] 100
```

```r
tab1[, 2]  # accéder à la deuxième colonne
```

```
[1] "M" "F" "M" "F"
```

```r
tab1[-1,]  # tab1 sauf la première ligne
```

```
    Noms Genre Taille Poids
2  Selma     F     60    21
3 Khaled     M    172    81
4  Sarra     F    120    42
```

On peut aussi accéder aux éléments d'une `data.frame` en utilisant les noms des variables. Avant d'appliquer cette manière, affichons les noms du tableau des données en utilisant la fonction `names()`.



```r
names(tab1)
```

```
[1] "Noms"   "Genre"  "Taille" "Poids" 
```


```r
tab1$Noms # ou encore tab1['noms']
```

```
[1] "Youssef" "Selma"   "Khaled"  "Sarra"  
```

```r
tab1['Noms']
```

```
     Noms
1 Youssef
2   Selma
3  Khaled
4   Sarra
```

Pour ajouter une ligne (une colonne), on peut utiliser la fonction `rbind()`(`cbind()`).
