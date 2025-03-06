<h1 align="center">Push Swap</h1>

<p align="center">
  <a href="#explication-fr">🇫🇷</a> | <a href="#explanation-en">🇬🇧</a>
</p>

---

## <a name="explication-fr"></a>🇫🇷 Explication

### Ce qu’on devait faire

Pour ce projet, l’objectif était de créer un programme capable de trier une liste de nombres fournie, en respectant certaines contraintes :
- Les nombres sont **uniques** (pas de doublons) et ne dépassent pas la taille d’un `int`.
- Pour effectuer le tri, on ne peut utiliser que **deux stacks maximum** (stack A et stack B).
- Le but est d’utiliser **le moins d’instructions possible**.

#### Instructions disponibles :
- **`push (a/b)`** : Déplace un élément vers la stack cible (ex. `push_a` déplace de B vers A).
- **`rotate (a/b/r)`** : Déplace l’élément du haut de la stack vers le bas, tout en préservant l’ordre des autres éléments. Avec `r`, les deux stacks sont rotatées en une seule instruction.
- **`reverse_rotate (a/b/r)`** : Déplace l’élément du bas de la stack vers le haut, en conservant l’ordre du reste. Avec `r`, les deux stacks sont affectées simultanément.
- **`swap (a/b/s)`** : Échange les deux premiers éléments de la stack cible. Avec `s`, les deux stacks sont swappées en une seule instruction.


### Comment je m’y suis pris

Dans ce projet, je voulais approfondir ma maîtrise de deux concepts : les **pointeurs de type `void *`** et les **pointeurs sur fonctions**. Pour cela, j’ai décidé d’utiliser les fonctions de listes chaînées de la bibliothèque `libft`.

#### Étapes suivies :

1. **Création d’une structure de données**  
   J’ai défini une structure `data` qui constitue le contenu des nœuds de ma liste chaînée. Pour rendre la liste **doublement chaînée**, j’ai inclus un pointeur vers le nœud précédent en plus des données habituelles.

2. **Recherche d’un algorithme adapté**  
   Après deux tentatives infructueuses pour concevoir mon propre algorithme, j’ai étudié les algorithmes existants. J’ai opté pour une approche qui cherche à chaque étape **le meilleur coup possible**, jusqu’à ce que :  
   - La stack A soit triée, ou  
   - Sa taille soit réduite à 3 éléments.  
   L’objectif n’était pas d’avoir le programme le plus rapide, mais de générer la **séquence d’instructions la plus courte** pour trier les nombres.

3. **Création d’une structure pour les instructions**  
   J’ai conçu une structure `s_move` pour stocker les informations sur chaque instruction :  
   - Le nom de l’instruction (défini via des macros),  
   - La stack concernée (A, B ou les deux),  
   - Le coût de l’opération,  
   - Un pointeur sur la fonction à exécuter.  
   Cette structure est souvent utilisée dans un tableau : `[0]` pour la source, `[1]` pour la destination, `[2]` pour les deux stacks (cas des instructions combinées comme `rr` ou `rrr`).

4. **Optimisation des mouvements**  
   Pour réduire le nombre d’instructions, j’ai privilégié les opérations combinées comme `rr` ou `rrr` lorsque cela était possible. À chaque étape :  
   - Je calcule le coût de chaque mouvement,  
   - Je choisis le moins coûteux,  
   - J’exécute ce mouvement et passe au nombre suivant.

5. **Gestion de la fin du tri**  
   Une fois que la stack A atteint une taille de 3 éléments, j’applique une stratégie inverse : je transfère les éléments de la stack B vers A en les plaçant dans un **ordre croissant**. Quand la stack B est vide, je cherche la plus petite valeur dans A :  
   - Si son index est supérieur à la moitié de la taille de la stack, j’utilise `reverse_rotate`.  
   - Sinon, j’utilise `rotate`, jusqu’à ce qu’elle soit en première position.


## <a name="explanation-en"></a>🇬🇧 Explanation
