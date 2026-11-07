# Currency Converter

Application web de conversion de devises faite avec Vue.js 3 et Vite.
Elle convertit un montant d'une devise vers une autre à partir de taux fixes
(l'euro sert de devise pivot).

## Fonctionnalités

- Saisie du montant avec un clavier numérique sur la page
- Choix de la devise source et de la devise cible (USD, EUR, TND, GBP, JPY, CAD)
- Bouton pour inverser les deux devises
- Résultat arrondi à 2 décimales
- Message d'erreur si le montant est égal à 0

## Lancer le projet

npm install
npm run dev

Puis ouvrir http://localhost:5173 dans le navigateur.

## Structure

- src/data/taux.js : liste des devises et taux de change
- src/components/CurrencyConverter.vue : composant principal
- src/App.vue : affiche le composant
- screenshots/ : captures d'écran des tests

## Technologies

Vue.js 3 (Composition API, script setup), Vite, CSS (Flexbox et Grid)