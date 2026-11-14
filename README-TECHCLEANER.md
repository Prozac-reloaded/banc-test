# Tech-Cleaner – Banc de test manettes

Version adaptée de [DualShock Calibration GUI](https://github.com/dualshock-tools/dualshock-tools.github.io) (licence MIT, © the_al)
pour produire des **rapports de bon fonctionnement** après tests et calibrage des manettes PS4 / PS5 / DualSense Edge.

## Ce qui a été ajouté

- Bouton vert **« Rapport Tech-Cleaner »** sur l'écran principal, une fois la manette connectée.
- Fenêtre de rapport en 4 étapes :
  1. **Manette détectée** : modèle, n° de série, couleur, carte mère, firmware, authenticité (détection des clones).
  2. **Tests fonctionnels** : reprend automatiquement les résultats du Quick Test (bouton pour le lancer directement).
  3. **Mesure des joysticks** :
     - *Centre au repos* : 3 s sans toucher les sticks, mesure le décalage maximal (tolérance 6 %).
     - *Circularité* : faire plusieurs tours en butée, mesure l'écart au cercle (tolérance 15 %, référence usine Sony ≈ 10 %).
     - Les calibrages faits pendant la session (centre, amplitude, enregistrement permanent) sont repris automatiquement.
  4. **Intervention** : client, référence commande, technicien, travaux réalisés, garantie (3 mois par défaut, 6 mois proposé automatiquement si « Upgrade TMR » est coché), observations, éléments non d'origine constatés, verdict (automatique ou forcé).
- **Générer le rapport** : ouvre un rapport A4 aux couleurs Tech-Cleaner → bouton *Imprimer / Enregistrer en PDF*.
- Onglet **Historique** : tous les rapports sont conservés dans le navigateur, réimprimables, avec export (sauvegarde JSON + tableau CSV pour Excel) et import.
- Statistiques/traceurs de l'outil d'origine désactivés : aucune donnée client ne quitte le PC.

## Réglages

Tout est en haut du fichier `js/techcleaner/report.js` (objet `TC_CONFIG`) : coordonnées, seuils de tolérance, durées de garantie.
La liste des travaux proposés est juste en dessous (`INTERVENTIONS`).

**Logo** : déposer votre logo sous le nom `images/techcleaner-logo.png` ; il remplacera automatiquement le logo texte sur les rapports.

## Mise en ligne (le plus simple : GitHub Pages)

1. Créer un dépôt GitHub (ex. `banc-test`) et y envoyer ce dossier.
2. Dans le dépôt : *Settings → Pages → Source : GitHub Actions*.
3. À chaque envoi, le site est construit et publié automatiquement (workflow déjà inclus) sur `https://<votre-compte>.github.io/banc-test/`.

## Utilisation en local (sur le PC de l'atelier)

Prérequis : Node.js 20+ et Google Chrome ou Microsoft Edge (WebHID obligatoire).

```bash
npm install
npm run start
```

Puis ouvrir `http://localhost:8080` dans Chrome/Edge et brancher la manette **en USB**.

## Fichiers modifiés / ajoutés

- `js/techcleaner/session.js` – mémorise les constats de la session (nouveau)
- `js/techcleaner/report.js` – mesures, formulaire, rapport, historique (nouveau)
- `templates/techcleaner-report-modal.html` – fenêtre du rapport (nouveau)
- `js/core.js`, `js/modals/quick-test-modal.js`, `js/template-loader.js` – branchements (quelques lignes, repérées « Tech-Cleaner »)
- `js/utils.js`, `index.html` – statistiques désactivées, nom et pied de page Tech-Cleaner

Les modifications du code d'origine sont volontairement minimes pour pouvoir récupérer facilement les mises à jour du projet d'origine.
