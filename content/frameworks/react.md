# Apprendre React 19

## 📘 Sommaire

1. Introduction à React 19
   - Qu'est-ce que React 19 ?
   - Nouveautés majeures de React 19
   - Pourquoi migrer vers React 19 ?
   - Installation et configuration d'un projet avec Create React App ou Vite
   - Vue d'ensemble de l'architecture de React 19

2. Fondamentaux de React 19
   - Structure d'un composant fonctionnel
   - JSX : syntaxe et fonctionnement
   - Props et State : gestion des données
   - Utilisation de `useState` et `useEffect`
   - Introduction aux hooks intégrés : `useReducer`, `useContext`, `useRef`

3. Nouveautés et changements dans React 19
   - Suppression de `useMemo`, `useCallback` et `React.memo` : React gère désormais l'optimisation des performances en arrière-plan
   - Passage des refs comme propriétés ordinaires (plus besoin de `forwardRef`)
   - Introduction du nouveau transformateur JSX : pourquoi il est désormais requis
   - Migration de `ReactDOM.render` vers `ReactDOM.createRoot`
   - Suppression de `propTypes`, `defaultProps` et des refs de type chaîne

4. Gestion de l'état et du contexte
   - Utilisation de `useReducer` pour la gestion d'état complexe
   - Context API : partage de données entre composants
   - Introduction à `useContext` et `useReducer` combinés
   - Remplacement de Redux par des solutions plus modernes

5. Routage avec React Router
   - Installation et configuration de React Router
   - Définition de routes et navigation
   - Paramètres d'URL et liens dynamiques
   - Protection des routes (authentification et autorisation)

6. Tests avec React 19
   - Pourquoi tester avec React ?
   - Introduction à Jest et React Testing Library
   - Tests unitaires et d'intégration
   - Tests de composants avec hooks
   - Bonnes pratiques de tests dans React 19

7. Optimisation des performances
   - Comprendre le rendu concurrent
   - Utilisation de `Suspense` pour le chargement asynchrone
   - Code splitting et lazy loading
   - Analyse des performances avec React DevTools

---

## 1. Introduction à React 19

React 19 est la dernière version majeure de la bibliothèque JavaScript pour la construction d'interfaces utilisateur. Cette version apporte des améliorations significatives en termes de performances, de nouvelles fonctionnalités et une simplification de certaines API existantes.

### Qu'est-ce que React 19 ?

React est une bibliothèque déclarative, efficace et flexible pour créer des interfaces utilisateur interactives. React 19 s'appuie sur les concepts fondamentaux des versions précédentes tout en introduisant des optimisations internes et de nouvelles primitives pour faciliter le développement d'applications modernes et performantes.

### Nouveautés majeures de React 19

React 19 introduit plusieurs changements notables :

*   **Optimisation automatique des performances :** React gère désormais automatiquement la mémorisation des composants et des valeurs, rendant `useMemo`, `useCallback` et `React.memo` obsolètes dans la plupart des cas.
*   **Refs simplifiées :** Les refs peuvent maintenant être passées comme des props ordinaires, éliminant le besoin de `forwardRef`.
*   **Nouveau transformateur JSX :** Un nouveau transformateur JSX est requis pour bénéficier des dernières optimisations et fonctionnalités.
*   **API Root améliorée :** `ReactDOM.createRoot` remplace `ReactDOM.render` pour une meilleure gestion du rendu concurrent et des mises à jour.
*   **Nettoyage d'API :** Plusieurs API plus anciennes comme `propTypes`, `defaultProps` et les refs de type chaîne ont été supprimées.

### Pourquoi migrer vers React 19 ?

Migrer vers React 19 offre plusieurs avantages :

*   **Performances améliorées :** Grâce aux optimisations automatiques, vos applications peuvent devenir plus rapides sans effort supplémentaire.
*   **Code simplifié :** La suppression de certaines API et la simplification des refs rendent le code plus concis et facile à lire.
*   **Nouvelles fonctionnalités :** Accès aux dernières primitives et améliorations pour construire des interfaces utilisateur plus riches.
*   **Préparation pour l'avenir :** Adopter la dernière version vous positionne pour les futures évolutions de React.

### Installation et configuration d'un projet avec Create React App ou Vite

Pour démarrer un nouveau projet React 19, vous pouvez utiliser des outils modernes comme Vite ou Create React App (bien que Vite soit généralement recommandé pour sa rapidité).

**Avec Vite :**

```bash
npm create vite@latest my-react19-app --template react
cd my-react19-app
npm install
npm run dev
```

Vite configurera automatiquement un projet avec le nouveau transformateur JSX et les dépendances nécessaires.

**Avec Create React App (si vous préférez) :**

```bash
npx create-react-app my-react19-app --template cra-template-react-18 # Utilisez le template React 18 et mettez à jour ensuite
cd my-react19-app
npm install react@latest react-dom@latest
```

Notez que vous devrez peut-être configurer manuellement le nouveau transformateur JSX et `createRoot` si vous partez d'un ancien template CRA. Il est recommandé d'utiliser Vite pour un nouveau projet React 19.

### Vue d'ensemble de l'architecture de React 19

React 19 conserve l'architecture basée sur les composants. Votre application est construite comme une arborescence de composants, chacun gérant son propre état et ses propres props. Le moteur de rendu concurrent de React 19 permet des mises à jour plus fluides et une meilleure réactivité de l'interface utilisateur, même lors de tâches complexes. Les hooks restent la manière recommandée de gérer l'état et les effets secondaires dans les composants fonctionnels.

---

## 2. Fondamentaux de React 19

Cette section couvre les concepts de base nécessaires pour commencer à construire des applications avec React 19.

### Structure d'un composant fonctionnel

Les composants fonctionnels sont la manière moderne d'écrire des composants React. Ce sont de simples fonctions JavaScript qui retournent des éléments React (décrivant ce qui doit apparaître à l'écran).

```jsx
import React from 'react';

function MonComposant(props) {
  // Logique du composant
  return (
    <div>
      <h1>Bonjour, {props.nom}</h1>
      <p>Ceci est un composant fonctionnel.</p>
    </div>
  );
}

export default MonComposant;
```

*   Un composant fonctionnel reçoit un objet `props` en argument, contenant les données passées par le parent.
*   Il retourne du JSX, qui est ensuite rendu par React.

### JSX : syntaxe et fonctionnement

JSX (JavaScript XML) est une extension de syntaxe pour JavaScript. Il ressemble à du HTML mais permet d'écrire des structures d'interface utilisateur directement dans votre code JavaScript.

```jsx
const element = <h1>Bonjour, monde !</h1>;
```

*   JSX n'est pas du HTML ou une chaîne de caractères. C'est une extension de syntaxe qui est transformée en appels à `React.createElement` par un processus de compilation (comme Babel ou le transformateur JSX de React 19).
*   Vous pouvez intégrer des expressions JavaScript dans JSX en utilisant des accolades `{}`.

```jsx
const nom = 'Roo';
const element = <h1>Bonjour, {nom}</h1>;
```

### Props et State : gestion des données

*   **Props (Propriétés) :** Les props sont des données passées d'un composant parent à un composant enfant. Elles sont en lecture seule pour le composant enfant.

```jsx
// Composant Parent
function App() {
  return <MonComposant nom="Roo" />;
}

// Composant Enfant (voir exemple ci-dessus)
function MonComposant(props) {
  return <h1>Bonjour, {props.nom}</h1>; // Accès à la prop 'nom'
}
```

*   **State (État) :** Le state est un ensemble de données gérées par un composant lui-même. Lorsque le state change, le composant se re-rend automatiquement.

### Utilisation de `useState` et `useEffect`

*   **`useState` :** Un hook qui permet d'ajouter une variable d'état à un composant fonctionnel. Il retourne une paire : la valeur actuelle de l'état et une fonction pour la mettre à jour.

```jsx
import React, { useState } from 'react';

function Compteur() {
  const [count, setCount] = useState(0); // Initialise l'état 'count' à 0

  return (
    <div>
      <p>Le compteur est à : {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Incrémenter
      </button>
    </div>
  );
}
```

*   **`useEffect` :** Un hook qui permet d'effectuer des effets secondaires dans les composants fonctionnels (comme des appels API, des souscriptions, des manipulations du DOM). Il s'exécute après chaque rendu du composant par défaut.

```jsx
import React, { useState, useEffect } from 'react';

function TitreDynamique() {
  const [titre, setTitre] = useState('Chargement...');

  useEffect(() => {
    // Cet effet s'exécute après le rendu initial et après chaque mise à jour
    document.title = `Titre : ${titre}`;

    // Fonction de nettoyage (optionnel)
    return () => {
      // S'exécute avant le prochain effet ou lors du démontage du composant
      console.log('Nettoyage de l\'effet');
    };
  }, [titre]); // Le tableau de dépendances : l'effet se ré-exécute si 'titre' change

  return (
    <div>
      <input
        type="text"
        value={titre}
        onChange={(e) => setTitre(e.target.value)}
      />
      <p>Le titre de la page est mis à jour.</p>
    </div>
  );
}
```

### Introduction aux hooks intégrés : `useReducer`, `useContext`, `useRef`

React fournit d'autres hooks pour gérer des scénarios plus avancés :

*   **`useReducer` :** Alternative à `useState` pour la gestion d'état plus complexe, impliquant une logique de transition d'état basée sur des actions (souvent utilisé avec `useContext`).
*   **`useContext` :** Permet d'accéder à la valeur d'un contexte React, facilitant le partage de données entre composants sans passer les props manuellement à chaque niveau.
*   **`useRef` :** Permet de créer une référence mutable qui persiste pendant toute la durée de vie du composant. Utile pour accéder à des éléments DOM ou stocker des valeurs qui ne déclenchent pas de re-rendu lorsqu'elles changent.

---

## 3. Nouveautés et changements dans React 19

React 19 apporte des changements significatifs qui simplifient le développement et améliorent les performances.

### Suppression de `useMemo`, `useCallback` et `React.memo`

Dans React 19, le compilateur React gère désormais automatiquement la mémorisation des composants et des valeurs. Cela signifie que vous n'avez plus besoin d'utiliser explicitement `useMemo`, `useCallback` ou `React.memo` dans la plupart des cas. Le compilateur analyse votre code et applique les optimisations nécessaires en coulisses.

**Avant React 19 :**

```jsx
import React, { useMemo } from 'react';

function ListeElements({ items }) {
  const listeOptimisee = useMemo(() => {
    return items.map(item => <li key={item.id}>{item.nom}</li>);
  }, [items]); // Dépendance à 'items'

  return <ul>{listeOptimisee}</ul>;
}
```

**Avec React 19 :**

```jsx
import React from 'react';

function ListeElements({ items }) {
  // React 19 gère automatiquement la mémorisation si nécessaire
  const listeElements = items.map(item => <li key={item.id}>{item.nom}</li>);

  return <ul>{listeElements}</ul>;
}
```

Cette automatisation réduit la quantité de code boilerplate et le risque d'oublier une dépendance dans les tableaux de dépendances des hooks de mémorisation.

### Passage des refs comme propriétés ordinaires

React 19 simplifie la manière de passer des refs aux composants. Vous pouvez maintenant passer une ref comme une prop ordinaire, éliminant le besoin de `forwardRef`.

**Avant React 19 (avec `forwardRef`) :**

```jsx
import React, { useRef, forwardRef } from 'react';

const MonInput = forwardRef((props, ref) => {
  return <input ref={ref} type="text" {...props} />;
});

function App() {
  const inputRef = useRef();

  return (
    <div>
      <MonInput ref={inputRef} placeholder="Tapez ici" />
      <button onClick={() => inputRef.current.focus()}>Focus Input</button>
    </div>
  );
}
```

**Avec React 19 :**

```jsx
import React, { useRef } from 'react';

// La ref est passée comme une prop normale
function MonInput({ inputRef, ...props }) {
  return <input ref={inputRef} type="text" {...props} />;
}

function App() {
  const inputRef = useRef();

  return (
    <div>
      <MonInput inputRef={inputRef} placeholder="Tapez ici" />
      <button onClick={() => inputRef.current.focus()}>Focus Input</button>
    </div>
  );
}
```

Cette approche rend le passage des refs plus intuitif et cohérent avec le passage d'autres props.

### Introduction du nouveau transformateur JSX

React 19 nécessite l'utilisation du nouveau transformateur JSX. Ce transformateur est plus performant et permet les optimisations automatiques mentionnées précédemment. Si vous utilisez des outils de build modernes comme Vite ou une version récente de Create React App, le nouveau transformateur est généralement configuré par défaut. Si vous configurez Babel manuellement, assurez-vous d'utiliser `@babel/plugin-transform-react-jsx` avec l'option `runtime: 'automatic'`.

### Migration de `ReactDOM.render` vers `ReactDOM.createRoot`

L'API `ReactDOM.render` est obsolète dans React 19 et a été remplacée par `ReactDOM.createRoot`. `createRoot` est la nouvelle API recommandée pour le rendu des applications React et est nécessaire pour bénéficier des fonctionnalités du rendu concurrent.

**Avant React 19 :**

```javascript
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

**Avec React 19 :**

```javascript
import ReactDOM from 'react-dom/client'; // Notez le '/client'
import App from './App';

const container = document.getElementById('root');
const root = ReactDOM.createRoot(container); // Crée une racine
root.render(<App />); // Rend l'application dans la racine
```

L'utilisation de `createRoot` permet à React de gérer plus efficacement les mises à jour et de préparer le terrain pour les fonctionnalités de rendu côté serveur et de streaming.

### Suppression de `propTypes`, `defaultProps` et des refs de type chaîne

React 19 supprime plusieurs API plus anciennes :

*   **`propTypes` et `defaultProps` :** Bien qu'utiles pour la validation de type et les valeurs par défaut, ces fonctionnalités sont mieux gérées par TypeScript ou des outils similaires au niveau de la compilation.
*   **Refs de type chaîne :** L'utilisation de chaînes de caractères pour les refs (`<input ref="monInput" />`) est une ancienne méthode qui a été remplacée par l'API `useRef` et les refs de rappel.

Assurez-vous de mettre à jour votre code pour utiliser les alternatives modernes avant de migrer vers React 19.

---

## 4. Gestion de l'état et du contexte

La gestion de l'état est un aspect crucial du développement d'applications React. React offre plusieurs outils pour gérer l'état, des hooks locaux comme `useState` aux solutions plus avancées comme l'API Context et `useReducer`.

### Utilisation de `useReducer` pour la gestion d'état complexe

Le hook `useReducer` est une alternative à `useState` qui est particulièrement utile pour gérer une logique d'état complexe impliquant plusieurs sous-valeurs ou lorsque le prochain état dépend de l'état précédent. Il est souvent préféré à `useState` lorsque les mises à jour d'état sont complexes ou lorsque l'état est partagé entre plusieurs composants via `useContext`.

`useReducer` prend une fonction `reducer` et un état initial comme arguments et retourne l'état actuel et une fonction `dispatch`.

```javascript
import React, { useReducer } from 'react';

// Le reducer : une fonction pure qui prend l'état actuel et une action, et retourne le nouvel état
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    case 'reset':
      return { count: 0 };
    default:
      throw new Error();
  }
}

function CompteurComplexe() {
  const [state, dispatch] = useReducer(reducer, { count: 0 }); // Initialise l'état

  return (
    <div>
      <p>Compteur : {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
      <button onClick={() => dispatch({ type: 'reset' })}>Réinitialiser</button>
    </div>
  );
}
```

*   La fonction `reducer` contient la logique de mise à jour de l'état.
*   La fonction `dispatch` est utilisée pour envoyer des "actions" au reducer, déclenchant ainsi les mises à jour d'état.

### Context API : partage de données entre composants

L'API Context de React permet de partager des données (comme l'état global, les paramètres de thème, les informations d'authentification) entre les composants sans avoir à passer manuellement les props à chaque niveau de l'arborescence des composants (prop drilling).

1.  **Créer un Contexte :** Utilisez `React.createContext` pour créer un objet Context.

    ```javascript
    import React from 'react';

    const ThemeContext = React.createContext('light'); // Valeur par défaut
    ```

2.  **Fournir la valeur du Contexte :** Utilisez le `Provider` du Context pour envelopper la partie de votre arborescence de composants qui a besoin d'accéder à la valeur.

    ```jsx
    import React from 'react';
    import ThemeContext from './ThemeContext';
    import MonComposantQuiUtiliseLeTheme from './MonComposantQuiUtiliseLeTheme';

    function App() {
      return (
        <ThemeContext.Provider value="dark">
          <MonComposantQuiUtiliseLeTheme />
        </ThemeContext.Provider>
      );
    }
    ```

3.  **Consommer la valeur du Contexte :** Utilisez le hook `useContext` dans un composant fonctionnel pour lire la valeur du contexte.

    ```javascript
    import React, { useContext } from 'react';
    import ThemeContext from './ThemeContext';

    function MonComposantQuiUtiliseLeTheme() {
      const theme = useContext(ThemeContext); // Accède à la valeur du contexte

      return (
        <div style={{ background: theme === 'dark' ? '#333' : '#FFF', color: theme === 'dark' ? '#FFF' : '#000' }}>
          Le thème actuel est : {theme}
        </div>
      );
    }
    ```

### Introduction à `useContext` et `useReducer` combinés

Combiner `useContext` et `useReducer` est un modèle puissant pour gérer l'état global dans les applications React sans dépendre de bibliothèques externes comme Redux. `useReducer` gère la logique de mise à jour de l'état, et `useContext` permet de partager cet état et la fonction `dispatch` à travers l'arborescence des composants.

```javascript
import React, { createContext, useReducer, useContext } from 'react';

// 1. Créer le Contexte
const StateContext = createContext();
const DispatchContext = createContext();

// Le reducer
function appReducer(state, action) {
  switch (action.type) {
    case 'set_user':
      return { ...state, user: action.payload };
    case 'logout':
      return { ...state, user: null };
    default:
      throw new Error(`Unhandled action type: ${action.type}`);
  }
}

// 2. Créer le Provider
export function AppProvider({ children }) {
  const [state, dispatch] = useReducer(appReducer, { user: null }); // État initial

  return (
    <StateContext.Provider value={state}>
      <DispatchContext.Provider value={dispatch}>
        {children}
      </DispatchContext.Provider>
    </StateContext.Provider>
  );
}

// 3. Créer des hooks personnalisés pour consommer le Contexte
export function useAppState() {
  const context = useContext(StateContext);
  if (context === undefined) {
    throw new Error('useAppState must be used within an AppProvider');
  }
  return context;
}

export function useAppDispatch() {
  const context = useContext(DispatchContext);
  if (context === undefined) {
    throw new Error('useAppDispatch must be used within an AppProvider');
  }
  return context;
}

// Utilisation dans un composant :
// function UserInfo() {
//   const { user } = useAppState();
//   const dispatch = useAppDispatch();

//   if (!user) {
//     return <button onClick={() => dispatch({ type: 'set_user', payload: { name: 'Roo' } })}>Login</button>;
//   }

//   return (
//     <div>
//       <p>Bienvenue, {user.name}</p>
//       <button onClick={() => dispatch({ type: 'logout' })}>Logout</button>
//     </div>
//   );
// }

// Envelopper l'application avec le Provider :
// function App() {
//   return (
//     <AppProvider>
//       <UserInfo />
//     </AppProvider>
//   );
// }
```

Ce modèle permet une gestion d'état centralisée et prévisible, similaire à Redux, mais avec moins de boilerplate et une intégration native avec React.

### Remplacement de Redux par des solutions plus modernes

Avec les améliorations de l'API Context et l'introduction de `useReducer`, de nombreuses applications n'ont plus besoin de bibliothèques de gestion d'état externes comme Redux pour gérer l'état global. Le modèle `useContext` + `useReducer` est souvent suffisant pour la plupart des besoins.

Cependant, pour les applications très vastes et complexes avec des besoins avancés (middleware, devtools sophistiqués, etc.), Redux Toolkit reste une option viable et simplifiée par rapport à Redux classique. D'autres alternatives modernes comme Zustand, Jotai, ou Recoil offrent également des approches différentes et souvent plus simples pour la gestion d'état. Le choix dépendra de la taille et de la complexité de votre application, ainsi que de vos préférences.

---

## 5. Routage avec React Router

Le routage est essentiel pour les applications web monopages (SPA) afin de permettre la navigation entre différentes vues sans rechargement complet de la page. React Router est la bibliothèque de routage standard de facto pour React.

### Installation et configuration de React Router

Pour utiliser React Router dans votre projet React 19, vous devez l'installer via npm ou yarn :

```bash
npm install react-router-dom
# ou
yarn add react-router-dom
```

Ensuite, vous devez configurer votre application pour utiliser le routeur. Le plus souvent, vous envelopperez votre composant racine (par exemple, `App`) avec un routeur, comme `BrowserRouter` (pour les applications web modernes avec l'API History du navigateur).

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import { BrowserRouter as Router } from 'react-router-dom';
import App from './App';

const container = document.getElementById('root');
const root = ReactDOM.createRoot(container);

root.render(
  <React.StrictMode>
    <Router>
      <App />
    </Router>
  </React.StrictMode>
);
```

### Définition de routes et navigation

React Router utilise des composants pour définir les routes et gérer la navigation.

*   **`Routes` et `Route` :** Le composant `Routes` est utilisé pour regrouper un ensemble de `Route`s. Le composant `Route` associe un chemin d'URL à un composant à rendre.

    ```jsx
    import React from 'react';
    import { Routes, Route } from 'react-router-dom';
    import Accueil from './pages/Accueil';
    import APropos from './pages/APropos';
    import Contact from './pages/Contact';

    function App() {
      return (
        <div>
          {/* Votre barre de navigation ou d'autres éléments communs */}
          <Routes>
            <Route path="/" element={<Accueil />} />
            <Route path="/a-propos" element={<APropos />} />
            <Route path="/contact" element={<Contact />} />
          </Routes>
        </div>
      );
    }
    ```

*   **`Link` :** Le composant `Link` est utilisé pour créer des liens de navigation. Il empêche le rechargement complet de la page et utilise l'API History pour changer l'URL.

    ```jsx
    import React from 'react';
    import { Link } from 'react-router-dom';

    function Navigation() {
      return (
        <nav>
          <ul>
            <li><Link to="/">Accueil</Link></li>
            <li><Link to="/a-propos">À Propos</Link></li>
            <li><Link to="/contact">Contact</Link></li>
          </ul>
        </nav>
      );
    }
    ```

### Paramètres d'URL et liens dynamiques

Vous pouvez définir des routes avec des paramètres pour afficher des contenus dynamiques (par exemple, les détails d'un produit en utilisant son ID dans l'URL).

*   **Définir une route avec paramètre :** Utilisez le signe deux-points (`:`) suivi du nom du paramètre dans le chemin de la route.

    ```jsx
    <Route path="/produits/:produitId" element={<DetailProduit />} />
    ```

*   **Accéder aux paramètres dans le composant :** Utilisez le hook `useParams` pour accéder aux paramètres d'URL dans le composant rendu par la route.

    ```javascript
    import React from 'react';
    import { useParams } from 'react-router-dom';

    function DetailProduit() {
      const { produitId } = useParams(); // Récupère le paramètre 'produitId' de l'URL

      return (
        <div>
          <h1>Détails du Produit {produitId}</h1>
          {/* Afficher les détails du produit en utilisant produitId */}
        </div>
      );
    }
    ```

### Protection des routes (authentification et autorisation)

Pour protéger certaines routes et n'autoriser l'accès qu'aux utilisateurs authentifiés ou autorisés, vous pouvez créer un composant de route privée.

```jsx
import React from 'react';
import { Route, Navigate } from 'react-router-dom';
import useAuth from './useAuth'; // Hook personnalisé pour vérifier l'authentification

function PrivateRoute({ element, ...rest }) {
  const isAuthenticated = useAuth(); // Vérifie si l'utilisateur est authentifié

  return (
    <Route
      {...rest}
      element={isAuthenticated ? element : <Navigate to="/login" replace />}
    />
  );
}

// Utilisation dans votre Routes :
// <Routes>
//   <Route path="/login" element={<Login />} />
//   <PrivateRoute path="/dashboard" element={<Dashboard />} />
//   {/* ... autres routes */}
// </Routes>
```

Ce composant `PrivateRoute` vérifie si l'utilisateur est authentifié. Si c'est le cas, il rend le composant spécifié (`element`). Sinon, il redirige l'utilisateur vers la page de connexion (`/login`) en utilisant le composant `Navigate`.

---

## 6. Tests avec React 19

Tester vos composants React est essentiel pour garantir la fiabilité et la maintenabilité de votre application. Cette section couvre les bases des tests avec React 19 en utilisant les outils les plus courants : Jest et React Testing Library.

### Pourquoi tester avec React ?

Les tests vous aident à :

*   **Détecter les bugs tôt :** Identifier les problèmes avant qu'ils n'atteignent les utilisateurs.
*   **Améliorer la confiance :** Avoir l'assurance que vos modifications n'introduisent pas de régressions.
*   **Faciliter le refactoring :** Modifier le code existant en sachant que les tests vous alerteront si quelque chose se casse.
*   **Comprendre le comportement des composants :** Les tests servent de documentation vivante sur la manière dont vos composants sont censés fonctionner.

### Introduction à Jest et React Testing Library

*   **Jest :** Un framework de test JavaScript populaire développé par Facebook. Il est souvent utilisé avec React et fournit un environnement de test complet, y compris un runner de test, une bibliothèque d'assertions et un support pour les mocks.
*   **React Testing Library (RTL) :** Une bibliothèque qui se concentre sur le test du comportement de vos composants d'une manière qui ressemble à la façon dont un utilisateur interagirait avec eux. Plutôt que de tester les détails d'implémentation (comme l'état interne d'un composant), RTL encourage à tester l'interface utilisateur telle qu'elle est rendue dans le DOM.

Pour commencer, installez les dépendances nécessaires :

```bash
npm install --save-dev @testing-library/react @testing-library/jest-dom jest
# ou
yarn add --dev @testing-library/react @testing-library/jest-dom jest
```

Si vous utilisez Create React App ou Vite, Jest et RTL sont souvent déjà configurés.

### Tests unitaires et d'intégration

*   **Tests unitaires :** Testent de petites unités de code isolément (par exemple, une seule fonction ou un petit composant sans dépendances externes).
*   **Tests d'intégration :** Testent l'interaction entre plusieurs unités de code (par exemple, comment un composant parent interagit avec ses composants enfants, ou comment un composant interagit avec une API).

React Testing Library est particulièrement bien adaptée aux tests d'intégration, car elle se concentre sur l'interaction avec le DOM rendu.

### Tests de composants avec hooks

Tester des composants qui utilisent des hooks comme `useState` ou `useEffect` avec React Testing Library est assez simple. Vous rendez le composant et interagissez avec lui via le DOM, tout comme un utilisateur le ferait. RTL s'assure que les hooks fonctionnent correctement en arrière-plan.

```javascript
import React from 'react';
import { render, screen, fireEvent } from '@testing-library/react';
import Compteur from './Compteur'; // Votre composant Compteur utilisant useState

test('incrémente le compteur lorsque le bouton est cliqué', () => {
  render(<Compteur />);

  const compteurElement = screen.getByText(/Le compteur est à :/i);
  const boutonIncrementer = screen.getByText(/Incrémenter/i);

  expect(compteurElement).toHaveTextContent('Le compteur est à : 0');

  fireEvent.click(boutonIncrementer);

  expect(compteurElement).toHaveTextContent('Le compteur est à : 1');
});
```

Dans cet exemple, nous rendons le composant `Compteur`, trouvons les éléments pertinents par leur texte, vérifions l'état initial, simulons un clic sur le bouton, puis vérifions que l'état a été mis à jour correctement dans le DOM.

Pour tester des hooks personnalisés ou des logiques complexes liées aux hooks en dehors d'un composant, vous pourriez envisager d'utiliser la bibliothèque `@testing-library/react-hooks` (maintenant intégrée dans `@testing-library/react` sous le nom `renderHook`).

### Bonnes pratiques de tests dans React 19

*   **Tester le comportement, pas l'implémentation :** Concentrez-vous sur ce que l'utilisateur voit et avec quoi il interagit, plutôt que sur les détails internes du composant.
*   **Utiliser les requêtes de RTL dans l'ordre de priorité :** Préférez les requêtes qui ressemblent le plus à la façon dont un utilisateur trouverait des éléments (par exemple, `getByRole`, `getByLabelText`, `getByPlaceholderText`, `getByText`, `getByDisplayValue`, `getByAltText`, `getByTitle`, `getByTestId`).
*   **Tester les interactions utilisateur :** Simulez les clics, les saisies de texte, etc., pour vérifier que votre interface utilisateur réagit comme prévu.
*   **Mocker les dépendances externes :** Pour les tests unitaires, moquez les appels API, les modules externes ou les contextes pour isoler le composant testé.
*   **Maintenir les tests à jour :** Assurez-vous que vos tests reflètent les changements dans votre code.

---

## 7. Optimisation des performances

L'optimisation des performances est cruciale pour offrir une expérience utilisateur fluide, en particulier dans les applications React complexes. React 19 introduit des fonctionnalités et des améliorations pour faciliter l'optimisation.

### Comprendre le rendu concurrent

Le rendu concurrent est une fonctionnalité majeure de React qui permet à React de travailler sur plusieurs mises à jour d'état en même temps et de donner la priorité aux mises à jour les plus importantes (comme les interactions utilisateur). Cela rend l'application plus réactive en évitant de bloquer le thread principal pendant les rendus coûteux. `ReactDOM.createRoot` est nécessaire pour activer le rendu concurrent.

### Utilisation de `Suspense` pour le chargement asynchrone

`Suspense` est un composant React qui vous permet de "suspendre" le rendu d'une partie de votre arborescence de composants jusqu'à ce qu'une condition soit remplie (par exemple, le chargement de données ou de code). Il vous permet de gérer facilement les états de chargement sans logique conditionnelle complexe dans vos composants.

```jsx
import React, { Suspense } from 'react';

// Composant chargé paresseusement
const ComposantChargeLentement = React.lazy(() => import('./ComposantChargeLentement'));

function App() {
  return (
    <div>
      <h1>Bienvenue</h1>
      <Suspense fallback={<div>Chargement...</div>}>
        {/* Le contenu de Suspense ne sera rendu qu'une fois que ComposantChargeLentement est chargé */}
        <ComposantChargeLentement />
      </Suspense>
    </div>
  );
}
```

*   `React.lazy` permet de charger un composant dynamiquement (code splitting).
*   `Suspense` prend une prop `fallback` qui affiche un indicateur de chargement pendant que les composants enfants sont en cours de chargement.

### Code splitting et lazy loading

Le code splitting est une technique qui consiste à diviser votre bundle JavaScript en morceaux plus petits qui peuvent être chargés à la demande. Cela réduit la quantité de code que l'utilisateur doit télécharger initialement, améliorant ainsi le temps de chargement de la page. `React.lazy` et `Suspense` sont les outils intégrés de React pour le lazy loading au niveau des composants.

Pour le code splitting au niveau des routes, vous pouvez combiner `React.lazy`, `Suspense` et React Router :

```jsx
import React, { Suspense, lazy } from 'react';
import { Routes, Route } from 'react-router-dom';

const Accueil = lazy(() => import('./pages/Accueil'));
const APropos = lazy(() => import('./pages/APropos'));

function App() {
  return (
    <div>
      <Suspense fallback={<div>Chargement des pages...</div>}>
        <Routes>
          <Route path="/" element={<Accueil />} />
          <Route path="/a-propos" element={<APropos />} />
        </Routes>
      </Suspense>
    </div>
  );
}
```

### Analyse des performances avec React DevTools

React DevTools est une extension de navigateur (disponible pour Chrome, Firefox et Edge) qui vous permet d'inspecter l'arborescence des composants React, de visualiser les props et l'état, et d'analyser les performances de rendu.

Fonctionnalités clés pour l'optimisation :

*   **Profiler :** Enregistrez les interactions utilisateur pour voir quels composants se rendent et pourquoi, identifiant ainsi les goulots d'étranglement.
*   **Highlight Updates :** Mettez en évidence les composants qui se re-rendent pour visualiser les mises à jour inutiles.
*   **Component Tree :** Inspectez l'arborescence des composants pour comprendre la structure de votre application.

Utiliser régulièrement React DevTools pendant le développement vous aidera à identifier et à résoudre les problèmes de performance.