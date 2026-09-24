# Marelleo, micrologiciels

Ce dépôt ne contient pas de code : seulement l'image compilée du micrologiciel
de Marelleo, une boîte à histoires, et le manifeste que les boîtes viennent
lire pour savoir s'il existe quelque chose de plus récent.

Le code source vit ailleurs, dans un dépôt privé. Seul le binaire est publié,
pour que les boîtes n'aient aucun identifiant à porter : un objet qui va
chercher son propre micrologiciel ne doit pas transporter de secret.

## Le manifeste

`marelleo.json` est la seule chose qu'une boîte interroge. Elle le compare à sa
propre version, et ne télécharge que s'il annonce autre chose.

```json
{
  "version": "0.6.1",
  "url": "https://marelleo.zebra.rodeo/firmware.bin",
  "taille": 2666000,
  "md5": "l'empreinte de firmware.bin",
  "notes": "ce qui change"
}
```

`taille` et `md5` ne sont pas décoratifs. L'image est gravée dans l'emplacement
de programme inactif, et la boîte ne bascule dessus qu'une fois l'empreinte
vérifiée : une image tronquée ou abîmée en chemin est refusée, et la boîte
redémarre sur la version précédente, intacte.

## Publier une version

Depuis le dépôt du code :

```
tools/publier-firmware.sh ../marelleo-firmware https://marelleo.zebra.rodeo "ce qui change"
```

Le script compile, calcule l'empreinte, écrit les deux fichiers ici et les
commite. Il reste à pousser.
