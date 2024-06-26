# Maximiser les Rendements Agricoles avec l'Optimisation Mathématique (_[ici](/pages/BioFerme/Bioferme_stochastique.pdf)_)

Dans le monde complexe de l'agriculture moderne, les agriculteurs font face à de nombreux défis, de la gestion des cultures à la maximisation des rendements tout en minimisant les coûts. Pour relever ces défis, de nombreuses fermes se tournent vers l'optimisation [mathématique](/pages/BioFerme/Bioferme_stochastique.pdf)., une approche qui utilise des modèles mathématiques pour prendre des décisions éclairées sur la gestion des cultures et des ressources.

## Le Défi de la Gestion Agricole

La gestion d'une ferme agricole implique la prise en compte de divers facteurs, tels que les conditions météorologiques, les coûts des intrants agricoles, la demande du marché pour les produits cultivés, et bien d'autres. Pour maximiser les profits et optimiser les rendements, les agriculteurs doivent prendre des décisions éclairées sur la manière d'allouer leurs ressources limitées, telles que la terre, l'eau et la main-d'œuvre.

## Mise en situation : Cas de **_Birge & Louveaux, Introduction to Stochastic Programming, Springer, 1997_** 
### _[Resolution sous Excel](/pages/BioFerme/Biocarburants.xlsx)_
Un agriculteur européen se spécialise dans la culture du blé, du maïs et de la betterave sucrière sur ses 500 acres de terre. Au cours de l’hiver, il souhaite décider de la superficie à consacrer à chaque culture. Il faut au moins 200 t de blé et 240 t de maïs pour nourrir son bétail. Ces quantités peuvent être produites sur la ferme ou achetées auprès d’un négociant. Toute production excédentaire (par rapport aux besoins alimentaires) serait vendue (pour la production d'éthanol). Les prix de vente sont respectivement de 170 et 150 dollars par tonne de blé et de maïs. Les prix d’achat sont supérieurs de 40% (au prix de vente). Une autre culture pour la production d’éthanol est la betterave sucrière, qui se vend à 36 \$/t. Cependant, la Commission européenne impose un quota sur la production de betteraves sucrières. Toute quantité dépassant le quota ne peut être vendue qu’à 10 \$/t. Le quota de l’agriculteur pour l’année prochaine est de 6 000 t. Le coût de plantation (par acre) est de 150 \$ pour le blé, 230 \$ pour le maïs et 260 \$ pour la betterave sucrière. Sur la base de son expérience passée, l’agriculteur sait que le rendement moyen de ses terres est d'environ 2,5 t, 3 t et 20 t par acre pour le blé, le maïs et les betteraves sucrières, respectivement. Proposer un modèle mathématique pour aider cet agriculteur. 

| Culture          | Superficie (acres) | Besoins alimentaires (t) | Prix de vente ($/t) | Prix d'achat ($/t) | Prix de vente excédentaire ($/t) | Coût de plantation ($/acre) | Rendement moyen (t/acre) |
|------------------|---------------------|--------------------------|----------------------|---------------------|----------------------------------|------------------------------|--------------------------|
| Blé              | ?                   | 200                      | 170                  | 238                 | 170                              | 150                          | 2.5                      |
| Maïs             | ?                   | 240                      | 150                  | 210                 | 150                              | 230                          | 3                        |
| Betterave sucrière | ?                 | -                        | 36                   | 50.4                | 36 (quota), 10 (dépassement)     | 260                          | 20                       |


## Modèle Mathématique pour la Gestion Agricole : Etape 1 - Approche deterministique

Soit notre agriculteur européen qui cultive du blé, du maïs et de la betterave sucrière sur ses 500 acres de terre. Son objectif est de décider de la superficie à consacrer à chaque culture afin de maximiser ses profits. Pour cela, il doit tenir compte des besoins alimentaires de son bétail, des prix de vente et d'achat des différentes cultures, ainsi que des quotas imposés par les autorités.


Un modèle mathématique peut aider les agriculteurs à prendre ces décisions en formulant le problème de gestion agricole comme un problème d'optimisation. 

Ainsi, il est claire que les leviers de **decision** de l'agriculteur seront les **surface** allouees a la culture des differents cereales. On modelise le probleme comme suit:

**Variables de decisions :**

- $$ \mathcal{I} = \{ \text{Ble} , \text{Mais} , \text{Betterave}  \}$$ 
- $$ \mathcal{J} = \mathcal{I} \text{ - } \text{Betterave}$$ 
- $$ i \in \mathcal{I} $$ : les differentes cultures plantees par l'agriculteur
- $$X_i$$ : les superficies allouees pour les differentes cultures i ($$\forall i \in \mathcal{I}$$ )
- $$B_j$$ : Quantites achetee pour les differents produits j (Buy) ($$\forall j \in \mathcal{J}$$ )

**Variables de consequence :**

- $$S_i$$ : Quantites vendue pour les differents produits i (Sales) -- ou $$Ecarts_i$$ -- ($$\forall i \in \mathcal{I}$$ )
- $$P_i$$ : Quantites cultivees pour les differents produits i (Production) ($$\forall i \in \mathcal{I}$$ )
- $$TS_i$$ : Total des vente pour les differents produits i (Total sales) ($$\forall i \in \mathcal{I}$$ )
- $$QS_i$$ : Quantite disponibles des differents produits i (Quantity in stock) ($$\forall i \in \mathcal{I}$$ )
- $$K_1$$ et $$K_2$$ : Quantite de betterave produite, respectivement la quantite en dessous du quota et celle au dessus. 


**Parametres :**

- $$r_i$$ : Rendements de production pour les differents produits i ($$\forall i \in \mathcal{I}$$ )
- $$PS_i$$ : Prix de vente pour les differents produits i (Price of sale) ($$\forall i \in \mathcal{I}$$ )
- $$PB_j$$ : Prix d'achat pour les differents produits j (Price of buy) ($$\forall j \in \mathcal{J}$$ )
- $$C_i$$ : Couts de production des differents produits i par Acre (Cost of production) ($$\forall i \in \mathcal{I}$$ )
- $$N_i$$ : Besoins de la ferme en produits j (Needs of products) ($$\forall j \in \mathcal{J}$$ )
- $$Quota$$ : Quota defini par le commission europenne sur le produit _Betterave_



À partir des informations recueillies, nous écrivons les équations qui décrivent le problème. Cela inclut les contraintes d'équilibre des superficies cultivées, les contraintes de vente, d'achat et de production, ainsi que les contraintes spécifiques à la culture de la betterave. Nous formulons également la fonction objectif pour maximiser les profits. Voici les équations de contraintes de base qui définissent ce modèle :

1. **Équilibre de la Superficie Cultivée** :

   $$\sum_{i \in \mathcal{I}} X_i = \text{Superficie Totale Disponible} \leq 500 \textit{ Acres}$$

2. **Contraintes de Vente-Achat-Production de Produits** :

   - Contrainte 1 : Productions 
   
   $$ P_i = r_{\text{i}} . X_{\text{i}}$$
   
   - Contrainte 2 : Ventes 
   
   $$ S_i = P_i + B_i - N_i $$
   
   - Contrainte 3 : Total des ventes    

   $$ TS_j = PS_j.S_j $$ 
   
   et 
   
   $$ TS_{\text{betterave}} = 36K_1 + 10K_2$$
   
   - Contrainte 4 : Total de produits disponibles    
   
   $$ QS_j = P_i +  B_i$$ 
  
   

3. **Satisfaction de la Demande Minimale** :

   $$\sum_{i \in \mathcal{I}} (\ r_j.X_j  + B_j \ ) \geq \text{Demande Minimale Mensuelle} = N_j$$

4. **Contraintes Spécifiques à la Culture de la Betterave** :

   - Contrainte 1 : 
   
   $$r_{\text{betterave}} . X_{\text{betterave}} = K_1 + K_2 = P_{\text{betterave}}$$

   - Contrainte 2 : 
   
   $$ 0 \leq K_1 \leq Quota$$ 

   $$ 0 \leq K_2 \leq M$$ 
   
   ou plus simplement :   
   
   $$36.r_{\text{betterave}} . X_{\text{betterave}} \leq 36K_1 + 10K_2$$  
   
   et 
   
   $$ 0 \leq K_1 \leq Quota$$

   - Contrainte 3 : $$ N_{\text{Betterave}} = 0$$ 

L'objectif ici etant de maximiser le **profit**, on eccrit la fonction objective suivante:

5. **Objectif de Maximisation des Profits** :
   
   $$\text{Maximiser } \textbf{   Profit = Ventes - Cout} $$ 


Le modele final s'eccrit donc :


$$ \text{Maximiser Profit} = \sum_{i \in \mathcal{I}} TS_i  - \left(\sum_{i \in \mathcal{I}} C_i \cdot X_i + \sum_{j \in \mathcal{J}} PB_j \cdot B_j\right) $$

$$\sum_{i \in \mathcal{I}} X_i \leq 500$$

$$P_i = r_i \cdot X_i \quad (\forall i \in \mathcal{I})$$

$$S_i = P_i + B_i - N_i \quad (\forall i \in \mathcal{I}) $$

$$TS_i = PS_i \cdot S_i \quad (\forall i \in \mathcal{I})$$

$$QS_i = P_i + B_i \quad (\forall i \in \mathcal{I})$$

$$\sum_{i \in \mathcal{I}} (r_j \cdot X_j + B_j)  \geq N_j$$

$$ TS_{\text{betterave}} = 36K_1 + 10K_2$$

$$P_{\text{betterave}} = K_1 + K_2 $$

$$ 0 \leq K_1 \leq Quota$$

$$ X_i, B_i, K_1, K_2 \ \geq \ 0 \text{ pour tout } i \in \mathcal{I} $$

Nous utilisons des outils d'optimisation pour résoudre le modèle mathématique que nous avons développé. Cela nous permet d'obtenir les valeurs optimales des variables de décision et de conséquence, ainsi que le profit total réalisé par l'agriculteur. Nous analysons les résultats obtenus pour comprendre les décisions optimales recommandées par le modèle. Cela peut inclure l'allocation optimale des superficies, les quantités à acheter et à produire, ainsi que le profit total réalisé par l'agriculteur.



## Résultats et Commentaires

Après avoir résolu ce modèle mathématique, nous avons obtenu les résultats suivants (Pour les fichiers de solution, cliquez ici..) :

|               | Ble   | Maïs  | Betterave | Variable associée |
|---------------|-------|-------|-----------|-------------------|
| Surface       | 120   | 80    | 300       | $$X_i$$                 |
| Qte Achat     | 0     | 0     | 0         | $$B_i$$             |
| Rendement     | 2.5   | 3     | 20        | $$r_i$$                 |
| Total ventes  | $17,000 | $-   | $-        | $$TS_i$$            |
| Achat  (40% de plus du Prix vente)       | $238  | $210  | -         | $$B_i$$ 
| Production    | 300   | 240   | 6000      | $$P_i$$                 |
| Écart P-D     | 100   | 0     | 6000      | $$S_i$$             |
| Quantité disponible | 300 | 240 | 6000    | $$QS_i$$            |


- **Profit Total** : 118 600 $

Ces résultats montrent une allocation optimale des ressources agricoles pour maximiser les profits, tout en respectant les contraintes de demande minimale et de superficie disponible. Par exemple, la betterave est cultivée sur 100 hectares comme spécifié dans la contrainte, tandis que ni la betterave ni aucun autre produit n'est acheté, ce qui indique une gestion efficace des ressources financières.

![Modele Resolu sous Excel](/images/biofferme/Bioferme_deterministe.png)



```GAMS

Sets
    I       /Ble, Mais, Betterave/
    J       /Ble, Mais/;

Parameters
    r(I)    Rendements de production pour les differents produits
    PS(I)   Prix de vente pour les differents produits
    PB(J)   Prix achat pour les differents produits
    C(I)    Coûts de production des différents produits par acre
    N(J)    Besoins de la ferme en produits
    Quota   Quota défini par le commission européen sur le produit Betterave;

Variables
    X(I)    Superficies allouées pour les différentes cultures
    B(J)    Quantités achetées pour les différents produits
    S(I)    Quantités vendues pour les différents produits
    P(I)    Quantités cultivées pour les différents produits
    TS(I)   Total des ventes pour les différents produits
    QS(I)   Quantité disponibles des différents produits
    K1      Quantité de betterave produite en dessous du quota
    K2      Quantité de betterave produite au-dessus du quota
    Profit  Profit total;

Positive Variables X, B, K1, K2;

Equations
    Eq1     Equilibre de la superficie cultivée
    Eq2(I)  Contrainte de production et de vente pour les différents produits
    Eq3(J)  Satisfaction de la demande minimale pour les différents produits
    Eq4     Contrainte spécifique à la culture de la Betterave;

Eq1..   sum(I, X(I)) =l= 500;

Eq2(I).. P(I) =e= r(I) * X(I);

Eq3(J).. sum((I), r(I) * X(I) + B(I)) =g= N(I);

Eq4..   r("Betterave") * X("Betterave") =g= 36 * K1 + 10 * K2;

Profit =e= sum(I, PS(I) * S(I)) - (sum(I, C(I) * X(I)) + sum(J, PB(J) * B(J)));

Model agriculture /all/;
Solve agriculture using lp maximizing Profit;

Display X.l, B.l, S.l, P.l, TS.l, QS.l, K1.l, K2.l, Profit.l;


```

En utilisant ce modèle, les agriculteurs peuvent prendre des décisions éclairées sur la manière d'allouer leurs ressources pour obtenir les meilleurs rendements possibles, contribuant ainsi à une agriculture plus durable et rentable.

L'optimisation mathématique offre une approche puissante pour résoudre les problèmes de gestion agricole et maximiser les rendements. En suivant les étapes décrites dans ce tutoriel, les agriculteurs peuvent prendre des décisions éclairées qui les aident à tirer le meilleur parti de leurs ressources limitées.



## Modèle Mathématique pour la Gestion Agricole : Etape 2 - Decision sous incertitude (Concept de Matrice des gains, Prise de decision - Minimax, Maximax, ... Equivalent certain)

On introduit maintenant une incertitude sur la **meteo** (le temps qu'il fait) qui a pour consequence **majeure** le rendement des parcelles de culture. On fera l'hypothese qu'aucun changement n'est fait sur le marche (prix d'achat et de vente).

On a donc potentiellement un climat **Mauvais**, **Moyen** (le cas deterministe etudie precedemment), une meteo **Bonne**. Pour chaque temps, qu'il fait on associe une variation sur le rendement habituelle observe (le rendement moyen ou le **Moyen** qui est celui donnee par le modele deterministe de base prcedemment etudie). Ainisi en temps **Mauvais**, les rendement vont **diminuer** de 20 % : soit **80 %** du rendement moyen generalement observe; en temps **Bon** ou favorable, les rendement vont **augmenter** de 20 % : soit **120 %** du rendement moyen generalement observe.

Des lors, on peut donc calculer les nouveaux rendements dans chaque cas en notant toutefois, que aucune information n'est diponible sur le temps qu'il fera; on s'adaptera selon l'intuition du fermier (**selon l'aversion au risque du decideur**) ou au jour le jour. 

| Scenario | Ble   | Mais  | Betterave | Rendements |
|----------|-------|-------|-----------|------------|
| Mauvais  | 2.00  | 2.40  | 16.00     | 80%        |
| Moyenne  | 2.50  | 3.00  | 20.00     | 100%       |
| Bonne    | 3.00  | 3.60  | 24.00     | 120%       |

![Modele Resolu sous Excel](/images/biofferme/Bioferme_Rendements.png)


Avant de poursuivre , je tiens a preciser 02 concepts qui seront observes par la suite.

**Stratégie** caracterise souvent des **Choix** (un ensemble de valeurs defini par le decideur pour les differentes variables de decision, des portefeuilles d'actions ou de projet surlequel investir...NOte: il faut noter que a la fin, **_une seule decision sera prise_**): Ensemble de décisions prises par un décideur pour atteindre un objectif donné dans un environnement incertain. Cette stratégie peut viser à maximiser les bénéfices, minimiser les coûts, ou atteindre tout autre objectif défini par le problème.

**Scénario** souvent appele **Etats** dans lequel l'environnement du decideur evolue: Représente une configuration ou une réalisation possible de l'incertitude dans le modèle d'optimisation. Il peut y avoir plusieurs scénarios possibles, chacun étant associé à une probabilité ou à une pondération spécifique. Ces scénarios reflètent généralement des variations dans les données d'entrée telles que les conditions météorologiques, les demandes du marché, les coûts des ressources, etc.

L'objectif de l'optimisation sous incertitude est souvent de déterminer la meilleure stratégie à adopter, en tenant compte de tous les scénarios possibles et de leurs probabilités associées, afin de maximiser ou de minimiser une fonction objectif donnée.

1. **Resolution de chaque scenario :**

Afin de resourdre ce probleme sous-incertitude, on va resourdre le **probleme deterministe associe a chaque scenario**, pris individuellement.

| **Scenario** | Mauvais    | Moyenne   | Bonne     |
|------------|------------|-----------|-----------|
| **Rendement** | 80%        | 100%      | 120%      |
|            |            |   **Stratégie**         |           |
|  | Pessimiste         | Equilibre        | Optimiste        |
|   | L1         | L2        | L3        |
|    |            |     **Surface**      |           |
| Ble        | 100        | 120       | 183.333   |
| Mais       | 25         | 80        | 66.6667   |
| Betterave  | 375        | 300       | 250       |
| **Profit**    | $59,950.00 | $118,600.00 | $167,666.67 |

Le fichier Excel ci-dessous presente les resultats obtenu, ce qui va nous permettre de construitre la **Matrice de gains** associee a chaque **strategie**.

![Modele Resolu sous Excel](/images/biofferme/Bioferme_Strategies.png)

Ceci revient a resoudre le modele deterministe avec des valeurs fixes de : _les valeurs des coefficients de rendement_

- Resolution du modele : M1 - Mauvais 

![Modele Resolu sous Excel](/images/biofferme/Bioferme_det_mauvaise.png)

- Resolution du modele : M2 - Moyenne 

![Modele Resolu sous Excel](/images/biofferme/Bioferme_deterministe.png)

- Resolution du modele : M3 - Bonne 

![Modele Resolu sous Excel](/images/biofferme/Bioferme_det_bonne.png)

2. **Conception de la amatrice de gains :**

On peut des lors concevoir (definir) les strategies associees a ce probleme (3 etats ou scenario possibles) comme suit :

|          | Ble            | Mais           | Betterave      | Scénarios |
|----------|----------------|----------------|----------------|-----------|
| Pessimiste| 100 acres       | 25 acres        | 375 acres       |       Mauvaise    |
| Équilibré   | 120 acres       | 80 acres        | 300 acres       |      Moyenne     |
| Optimiste | 183.3 acres     | 66.7 acres      | 250 acres       |       Bonne    |

A partir de la, on construit tla matrice de gain comme suit:

**Step 1 :** Le remplassage de la matrice de gain commence par la diagonale qui correspond aux profits optimaux obtenu pour chaque scenario

![Modele Resolu sous Excel](/images/biofferme/Matricegainsstrategiebase.png)

**Step 2 :** On cherche a remplir le tableau de la matrice de gain avec les valeurs fixes de : 1) _les valeurs des coefficients de rendement_, 2) _les valeurs des superficies definies par chaque strategie_; la seule variable de decision dans ce cas devient la quantite a acheter Bj (la quantite de j a acheter)


![Modele Resolu sous Excel](/images/biofferme/Matricedegainscomplet.png)

Voici une explication detaillee du remplissage de la matrice des gains.

![Modele Resolu sous Excel](/images/biofferme/InceritudeExolication.png)


3. **Prise de decision :**

Plusieurs approches existent pour la prise de decision une fois que l'on a defini la matrice de gain. On presentera les plus populaires et leurs avantages mais aussi leur limites. (Pour une appication en finance que j'ai vraiment aimee je vous recommande ce [blog](https://madamefinance.wordpress.com/2014/06/09/173/).

**Approche 1 : Laplace Bayes - La moyenne** 


Ici, le produit ou la strategie qui retiendra notre attention elle qui sera le plus proche ou egal a la moyenne. L'inconvenient, est que:

- il peut souvent etre difficile d'avoir un produit dont le gain est strictement egal a la moyenne: on parle d'un risque de representation fausse de la realite

Dans notre cas, illustrons ce qui est enonce ci-dessus:

![Modele Resolu sous Excel](/images/biofferme/Laplace.png)

Ici, on calcule la moyenne des gains de chaque strategie (protefeuille, ou produit) pour l'ensemble des etats tel que : 

$$\text{Moy}_i =  \frac{1}{N} \sum_{j \in \text{Etats} } G_{i,j}$$

Ensuite, la strategie ayant la plus grande moyenne est la strategie **Optimiste avec une moyenne de G = $ 107 683.33** car elle est la plus grande. En effet, du fait, qu'aucune strategie ne donne exactement cette valeur, on evolue dans une incertitude encore plus importante puisque que une cette valeur ne _reflete pas la realite_: Savage (2008) compare cette approche à avoir 1 enfant et demi par femme.

![Modele Resolu sous Excel](/images/biofferme/Laplace1.png)


**Approche 2 : Wald - Maximin** 

Ici, le produit ou la strategie qui retiendra notre attention sera celle qui aura le meilleur resulat dans le pire scenario possible. L'inconvenient, est que:

- il occulte parfois les opportunites possible parcequ'il ne se focalise que sur les pertes probables: la consequence de cette approche en economie serait de freiner l'innovation afin de garantir une stabilite certaine (comportement systematiquement pessimiste).

Dans notre cas, illustrons ce qui est enonce ci-dessus:

![Modele Resolu sous Excel](/images/biofferme/Maximin.png)

Ici, on calcule la valeur minimale des gains de chaque strategie (protefeuille, ou produit) sur l'ensemble des etats tel que : 

$$\text{Min}_i =  \text{Min} \{ G_{i,j} \ | \ \forall \ j \in \mathcal{J} \} $$

Ensuite, la strategie ayant la plus grande valeur **minimale** est la strategie **Pessimiste avec une valeur de G = $ 59 950** car elle est la plus grande. Cependant, on constate qu'il est possible d'avoir de meilleur gain avec une strategie : comportement systematique frileux.

![Modele Resolu sous Excel](/images/biofferme/Maximin2.png)

**Approche 3 : Maximax** 

Ici, le produit ou la strategie qui retiendra notre attention sera celle qui aura le meilleur resulat dans le meilleur scenario possible. L'inconvenient, est que:

- il surestime l'ooportunite ce qui expose le decideur a un tres grand risque: risque eleve en cas de de mauvaise prediction.

Dans notre cas, illustrons ce qui est enonce ci-dessus:

![Modele Resolu sous Excel](/images/biofferme/Maximax.png)

Ici, on calcule la valeur maximale des gains de chaque strategie (protefeuille, ou produit) sur l'ensemble des etats tel que : 

$$\text{Min}_i =  \text{Max} \{ G_{i,j} \ | \ \forall \ j \in \mathcal{J} \} $$

Ensuite, la strategie ayant la plus grande valeur **minimale** est la strategie **Optimiste avec une valeur de G = $ 167 666.7** car elle est la plus grande. Cependant, le decideur est expose a un grand risque en cas de mauvaise prevision.

![Modele Resolu sous Excel](/images/biofferme/maximax2.png)

**Approche 4 : Minimax Regret - Leonard Savage (1954) , von Neumann (1926) et Landsheere, Gilbert (1979)** 

Ici, le produit ou la strategie qui retiendra notre attention sera celle qui aura le meilleur (le plus petit) regret parmi les regrets extremes. Dans un premier temps, on va calculer les regrets max de chaque gain i-j.

Il s'agit de la difference entre un gain et la plus grande valeur possible de gain associee a l'etat j de ce gain:

$$ \text{Regret}_{i,j} = \text{ Max } \{ G_{i,j} \} \ - \ G_{i,j} \ (\forall \ i \in \mathcal{I} )     $$

![Modele Resolu sous Excel](/images/biofferme/Minimax.png)

Ici, on calcule pour chaque strategie le regret maximal : 

$$ \text{Regret Max}_{i} = \text{ Max } \{ Regret_{i,j} \ (\forall \ i \in \mathcal{I}) \}    $$

Ensuite, la strategie ayant la plus grande valeur **minimale** du regret maximal est la strategie **Optimiste avec une valeur de Regret max = $ 12 250** (la plus petite). Elle est tres appreciee en theorie de la decision.

![Modele Resolu sous Excel](/images/biofferme/Minimax2.png)

**Approche 5 : Hurwicz - Appreciation du decideur** 

Cette approche se base sur l'expertise + ou - biaisee du decideur, de par son aversion au risque ou pas. 

Apres avoir identifier les Max et et les Min de chaque strategie, on trouve la somme ponderee de ceux-ci a partir de la preference du decideur:

$$ \text{Profit pour une Decision} = a \cdot Min_i \ + \ (a - 1) \cdot Max_i   $$

- a = 0.8 : Averse au risque
- a = 0.3 : Aime le risque 

![Modele Resolu sous Excel](/images/biofferme/risque.png)

## Modèle Mathématique pour la Gestion Agricole : Etape 3 - Decision selon une probabilite d'apparution des etats/scenarios (Modele stochastique)

Nous terminons ce projet en introduisant le concept de modele stochastique a proprement parler. Toutefois, il est important de montrer le caractere imperatif de suivre la demarche suivie tout au long de ce projet:

 1. Modeliser et resoudre le probleme selon une approche deterministique s'il y'a lieu.
 2. Identifier les differents scenarios, les resourdre et concevoir la matrice de gains
 3. Proposer le modele stochastique final global et le resoudre
 4. Identifier la VEIP (Valeur Esperee d'une Information parfaite) qui permet d'apprecier une offre exterieur (consultant, logiciel prestataire, ... ) 


 Afin de mener a bien l'etape 3 et 4, il est vital de rappeler le contexte de la prise de decision stochatique:
 - un choix (ou ensemble de choix) prealable a ete fait par le decideur sans etre affecte par l'incertitude: en occurence, la surperficie de culture pour chaque cereale
 - selon l'etat observe au court du temps, le decideur, peut s'ajuster (variables de recours : Quantite a vendre et Quantite a acheter par produit)

 Pour des raisons de simplification, nous ecrivons un modele stochatique allege (identique) de celui presente jusqu'ici (suppression des variables de consequence) :

 $$ \text{Maximiser Profit} = \frac{1}{3} \cdot \left(\sum_{i \in \mathcal{I}} PS_{i} \cdot S_{i,k} - \sum_{j \in \mathcal{J}} PB_j \cdot B_{j,k}\right)  - \sum_{i \in \mathcal{I}} C_i \cdot X_i  $$

$$\sum_{i \in \mathcal{I}} X_i \leq 500$$

$$S_{i,k} = r_{i,k} \cdot X_i + B_{i,k} - N_i \quad (\forall i \in \mathcal{I}) $$

$$\sum_{i \in \mathcal{I}} (r_{i,k} \cdot X_j + B_{i,k})  \geq N_j$$

$$ 36.S_{\text{betterave}} \leq 36K_1 + 10K_2$$

$$S_{\text{betterave}} = K_1 + K_2 $$

$$ 0 \leq K_1 \leq Quota$$

$$ X_i, B_i, K_1, K_2 \ \geq \ 0 \text{ pour tout } i \in \mathcal{I} $$

On peut ainsi modifier notre matrice de gain en rajoutant une nouvelle colonne : **Equivalent Certain** qui represnte la valeur esperee pour chaque strategie. On ecrit les equations associee:


$$ \text{Equivalent Certain}_1 = EC_{Pessimiste} = Prob_{Mauvais}.\text{Gain}_{Pessimiste,Mauvais} + Prob_{Moyen}.\text{Gain}_{Pessimiste,Moyen} + Prob_{Bon}.\text{Gain}_{Pessimiste,Bon}  $$
$$ \text{Equivalent Certain}_2 = EC_{Equilibre} = Prob_{Equilibre}.\text{Gain}_{Equilibre,Mauvais} + Prob_{Moyen}.\text{Gain}_{Equilibre,Moyen} + Prob_{Bon}.\text{Gain}_{Equilibre,Bon}  $$
$$ \text{Equivalent Certain}_3 = EC_{Optimiste} = Prob_{Mauvais}.\text{Gain}_{Optimiste,Mauvais} + Prob_{Moyen}.\text{Gain}_{Optimiste,Moyen} + Prob_{Bon}.\text{Gain}_{Optimiste,Bon}  $$

Les **profits esperes pour chaque strategie** correspondent a :

$$EC_{Pessimiste} = \frac{1}{3} \cdot \left( \$ \ 59,950 + \$ \ 86,600 + \ \$ \ 113,250 
 \right) = \ \$ \ 86,600 $$

$$EC_{Equilibre} = \frac{1}{3} \cdot \left( \$ \ 55,120 + \$ \ 118,600 + \ \$ \ 148,000 
 \right) = \ \$ \ 107,240 $$

$$EC_{Optimiste} = \frac{1}{3} \cdot \left( \$ \ 47,700 + \$ \ 107,683 + \ \$ \ 167,666.67 
 \right) = \ \$ \ 107,683.33 $$

On peut decider de faire le choix plutot sur la base du profit general espere (la solution du modele stochatique) :

On optient le profit espere :

$$Profit(E)  = \$ \ 108,390$$

A partir de ca, on peut trouver le **profit espere pour chaque etat (scenario)** :

$$ Profit(E)  = \frac{1}{3} \cdot \$ \ 108,390 =  \$ \ 36,130$$

On obtient toujours le meme resultat peu importe le scenario (etat) parceque les etats sont equi-probables. Tandis que le **profit sous information parfaite** est le profit que le decideur obtiendrait s'il maitrisait l'etat en avance multiplie par la probabilite d'occurence du scenario; ce qui reviendrait a prendre la meilleure decision pour un scenariio donne. On ecrit donc :

$$\text{Profit sous information parfaite } = \frac{1}{3} \cdot \$ \ 59,950 \ + \frac{1}{3} \cdot  \$ \ 118,600 \ + \frac{1}{3} \cdot \ \$ \ 167,666.67 = \ \$ \ 115,405.56 $$

On calcule donc le **VEIP** :

$$ \text{VEIP } =  \ \$ \ 115,405.56 \ - \$ \ 108,390 \ = \$ \ 7,015.56  $$



![Modele Resolu sous Excel](/images/biofferme/StochastiqueBioferme.png)