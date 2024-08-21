# TypeScript

> ❌ A travailler

> ✔️ Auto validation par l'étudiant

## 🎓 J'ai compris et je peux expliquer

- l'intéret de TypeScript dans l'IDE ✔️
- les types de bases ✔️
- comment et pourquoi étendre une interface ❌ / ✔️
- les classes et les decorators ✔️

## 💻 J'utilise

### Un exemple personnel commenté ✔️

```js
declare global {
    interface Window {
        dataLayer2: DataLayerObject[];
    }
}

const getAjaxBody = (pageID: string | undefined, pageStatus: string | undefined, request: Request, searchTerm: string | undefined | null): Record<string, any> => {
    const cookies = request.headers.get('set-cookie') || request.headers.get('cookie');
    let customerCookie: string | undefined = undefined;
    if (cookies) {
        const cookiesArray = cookies.split('; ');
        cookiesArray.forEach(cookie => {
            const [name, value] = cookie.split("=");
            if (name.trim() === "connect.sid") {
                customerCookie = value;
            }
        })
    } (...)
}
```
Ici on a une déclaration de type pour un objet dataLayer2 et une fonction getAjaxBody avec ses arguments typés.

### Utilisation dans un projet ❌ / ✔️

[lien github](...)

Description : <!-- TODO: Lien vers dataLayer -->

### Utilisation en production si applicable❌ / ✔️

[lien du projet](...)

Description : <!-- TODO: Lien vers dataLayer -->

### Utilisation en environement professionnel ❌ / ✔️

Description : Dans le cadre de la refonte du site e-commerce et du datalayer, il nous faut appeler un endpoint magento en précisant un id de page pour recevoir les infos du datalayer telles que demandées par Optimal Ways. Les infos devront ensuite être push dans le datalayer.

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

- J'ai ecrit un [tutoriel](...) ❌ / ✔️ <!-- TODO: Lien vers dataLayer -->
- J'ai fait une [présentation](...) ❌ / ✔️
