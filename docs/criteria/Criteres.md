---
tags: [Criteria, Criterion Options]
---

# Critères

Les critères sont des objets permettant de classifier des articles sous différents types de catégories. Ces derniers peuvent être assignés à des articles lors de la création de celui-ci.

<h2>Comment faire un formulaire de critères ?</h2>

Avant de créer une annonce, l'utilisateur doit passer à travers une série d'étape dont le remplissage des critères, ceci est un tutoriel permettant de comprendre comment créer ce formulaire de remplissage de critères.

<h3>Récupération des critères</h3>

La première chose à faire est d'obtenir la liste de tous les critères existant sur la plateforme:

> GET /criteria?sort=priority

-   Le retour est paginé par 50 éléments
-   Le paramètre **sort** permet de trier le résultat par priorité

<h3>Premier critère</h3>

Une fois cette liste des critères récupérée, il faut parcourir chaque critère (par ordre de priorité) et récupérer ses options. Voici ci-dessous un exemple pour le critère d'id 1:

> GET /criteria/1/relationships/options

-   Le résultat est paginé par 50

Une fois cette liste récupérée, affichez là afin de demander à l'utilisateur dans quelle option correspond le mieux à son article.

Par exemple, pour le critère **Marque**, les options y découlant pourront être **Apple** ou **Samsung**. L'utilisateur devra choisir un critère pour passer à l'étape suivante.

<h3>Critères suivants</h3>

Lorsque la première option a été choisie, il faut sauvegarder l'id de l'option qui a été choisie. Ensuite, récupérez la liste des options correspondant au critère suivant:

> GET /criteria/2/relationships/options?filter\[parents]=4

-   Le résultat est paginé par 50
-   Le paramètre **filter** permet de filtrer la liste des éléments retournés

Ici, on filtre les résultats retournés en fonction du premier critère choisi. La valeur 4 correspond à l'ID de la première option choisie, cela aura pour effet de retourner uniquement les nouvelles options découlant de ce critère.

A partir de maintenant, vous pouvez répéter cette étape pour chaque critère suivant dans la liste en ajoutant à chaque fois le critère choisi, la requête suivante pourra ressembler à:

> GET /criteria/3/relationships/options?filter\[parents]=4,6

<h3>Assignement des critères à une option</h3>

Une fois que vous avez terminé le formulaire des critères, vous pouvez passez la liste des options choisies lors de la création d'un article

<h3>Astuces</h3>

-   Si un critère ne retourne qu'une option, il est préférable de choisir cette option implicitement sans demander à l'utilisateur.
-   Les résultats sont paginés, bien que ne dépassant rarement voir jamais 50 éléments, il faut en tenir compte.
