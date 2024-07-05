# Titre de la compétence

> ❌ A travailler

> ✔️ Auto validation par l'étudiant

## 🎓 J'ai compris et je peux expliquer

- l'état (_state_) pour contrôler l'affichage d'un composant ✔️
- les composants enfants et les _props_ qu'on leur passe ✔️
- le déclenchement d'instructions en fonction des actions de l'utilisateur ❌ / ✔️
- le déclenchement d'instructions en fonction de l'étape du cycle de vie du composant ou du changement de valeur de ses props ❌ / ✔️
- l'usage d'un reducer (_useReducer_) pour gérer un état composé dans un composant
- l'état stocké dans un composant avec un _context provider_ et accessible dans ses descendants via `useContext` ✔️

## 💻 J'utilise

### Un exemple personnel commenté ❌ / ✔️

```js
import { Outlet } from 'react-router-dom'
import './App.scss'
import Nav from './components/Nav/Nav'
import SecondaryNav from './components/SecondaryNav/SecondaryNav'
import { useState, useEffect, useContext } from 'react';

function App() {
  const [productsArray, setProductsArray] = useState([]);
  const [notification, setNotification] = useState(0);

  const fetchProducts = async () => {
    try {
      const response = await fetch(`${import.meta.env.VITE_BACKEND_URL}src/productRoutes/getAllProducts.php`);
      const products = await response.json();
      setProductsArray(products);
    } catch (error) {
      console.error('Error fetching products:', error);
    }
  };

  const sessionStart = async () => {
    try {
      await fetch(`${import.meta.env.VITE_BACKEND_URL}src/userRoutes/sessionStart.php`, {
        credentials: 'include'
      });
    } catch (error) {
      console.error('Error while creating session: ', error)
    }
  };

  useEffect(() => {
    fetchProducts();
    sessionStart();
  }, []);

  return (
    <>
      <Nav
        notification={notification}
        setNotification={setNotification}
      />
      <SecondaryNav />
      <button style={{ color: 'white' }} type='button' onClick={handleDisconnect}>x</button>
      <Outlet
        context={{ productsArray, notification, setNotification }}
      />
    </>
  )
}

export default App;
```

### Utilisation dans un projet ❌ / ✔️

[lien github](https://github.com/FlorenceBuchelet/decitrephpbackend)

Description :

### Utilisation en production si applicable❌ / ✔️

[lien du projet](...)

Description :

### Utilisation en environement professionnel ❌ / ✔️

Description :

## 🌐 J'utilise des ressources

### Titre

- lien
- description

## 🚧 Je franchis les obstacles

### Point de blocage ❌ / ✔️

Description:

Plan d'action : (à valider par le formateur)

- action 1 ❌ / ✔️
- action 2 ❌ / ✔️
- ...

Résolution :

## 📽️ J'en fais la démonstration

- J'ai ecrit un [tutoriel](...) ❌ / ✔️
- J'ai fait une [présentation](...) ❌ / ✔️
