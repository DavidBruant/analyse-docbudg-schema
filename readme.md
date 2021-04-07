# Analyse schema document budgetaire

Ce repo analyse en détail la version 95 du schéma de données `<DocumentBudgetaire>`


## Source

Source des données : http://odm-budgetaire.org/composants/schemas/schema_doc_budg_V95.zip

http://odm-budgetaire.org/pagesIndex/outil-totem.html


## Respect de l'Article L311-6 du Code des relations entre le public et l'administration

Le premier objectif est de trouver tous les endroits où il pourrait y avoir des données faisant obstacle à la communication de fichiers `<DocumentBudgetaire>`

https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000037269056/


## Méthode

Partir du fichier [DocumentBudgetaire.xsd](SchemaDocBudg/DocumentBudgetaire.xsd) et commenter tous les morceaux du schema qui ne posent aucun risque jusqu'à ce qu'il ne reste que les parties avec un risque


## Analyse et discussion

### Éléments nécessitants une occultation par défaut

Ici, on liste les éléments et attributs (décrit par un sélecteur CSS) qui nécessitent une occultation de manière certaine ou par prudence

- `Budget > BlocBudget > PJRef > NomPJ[V]` 
    - type `Base_Texte100` (`TPJReference` de [SchemaDocBudg/Class_PJReference.xsd](SchemaDocBudg/Class_PJReference.xsd))
    - pourrait contenir un nom de personne physique, peut-être
- `Champ_Editeur[V]`
    - il y en a 36. Type `Base_Texte100`
    - Ce champ n'est pas documenté au-delà de "Commentaire", ce qu'il contient n'est donc pas clair 
- `Budget > Annexes > DATA_CONCOURS > CONCOURS > LibOrgaBenef[V]` quand `CodNatJurBenefCA` vaut `P3` ou est absent
    - `LibOrgaBenef[V]` est de le nom de l'organisme bénéficiaire de la subvention
    - `P3` signifie "personne physique"
    - quand `CodNatJurBenefCA` est absent, on ne sait pas, donc occulter par défaut
- `Budget > Annexes > DATA_PRET > PRET > NomBenefPret[V]`
    - la nature juridique du bénéficiaire d'un prêt n'est pas précisée, donc occuter le nom dans tous les cas par prudence
- `Budget > Annexes > DATA_MEMBRESASA > MEMBREASA > Proprietaire[V]`
    - l'élément `Proprietaire` peut contenir les noms et prénoms d'une personne physique


### Cas ne nécessitant pas occultation, mais à garder en tête en cas d'évolution du format de données

- `Budget > Annexes > DATA_FORMATION > FORMATION > NomElu[V]`
    - Défini dans [Class_Formation.xsd](SchemaDocBudg/Class_Formation.xsd). La documentation dit "Nom Prénom de l'élu". L'élément `FORMATION` ne contient que l'"Action de formation financée". Le nom et le prénom de l'élu.e de la collectivité sont déjà des informations publiques. Aussi, le fait que les élus se forment dans l'exercice de leur mandat est de notoriété publique. Les données comme le prix de la formation, son lieu, ses dates précises (au-delà du fait qu'elle a eu lieu pendant l'exercice comptable du document budgétaire) ne sont pas disponibles. Aussi, la décision de formation fait sûrement déjà l'objet d'une décision du conseil délibérant, il ne s'agit donc pas d'une donnée personnelle.
- `Budget > Annexes > DATA_PERSONNEL > PERSONNEL`
    - Il n'y a dans les éléments `PERSONNEL` aucune donnée permettant l'identification de personnes physiques


