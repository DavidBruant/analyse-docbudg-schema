# Analyse schema document budgetaire

Ce repo analyse en détail la version 95 du schéma de données `<DocumentBudgetaire>`


## Source

Source des données : http://odm-budgetaire.org/composants/schemas/schema_doc_budg_V95.zip

http://odm-budgetaire.org/pagesIndex/outil-totem.html


## Respect de l'Article L311-6 du Code des relations entre le public et l'administration

Le premier objectif est de trouver tous les endroits où il pourrait y avoir des données faisant obstacle à la communication de fichiers `<DocumentBudgetaire>`

https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000037269056/


## Méthode

Partir du fichier [Class_DocumentBudgetaire.xsd](SchemaDocBudg/Class_DocumentBudgetaire.xsd) et commenter tous les morceaux du schema qui ne posent aucun risque jusqu'à ce qu'il ne reste que les parties avec un risque


## Analyse et discussion

### Cas suspicieux

- élément `NomPJ` du type `TPJReference` de [SchemaDocBudg/Class_PJReference.xsd](SchemaDocBudg/Class_PJReference.xsd)
- 





