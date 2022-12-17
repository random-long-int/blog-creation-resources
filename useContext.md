[retour](./README.md)

# Context

Le hook `useContext` de React vous permet d'accéder à un contexte de l'application depuis n'importe quel composant de votre arbre de composants. Pour utiliser `useContext` de manière à ce que votre contexte soit accessible dans toute l'application, vous devez suivre les étapes suivantes:

1. Créez un contexte en utilisant la fonction `createContext` de React. Cette fonction prend en entrée le type de vos données de contexte et renvoie un objet comprenant deux propriétés: `Provider` et `Consumer`.
2. Enveloppez l'élément racine de votre application (généralement votre composant `App`) dans un `Provider` en utilisant la propriété `value` pour définir les données de votre contexte.
3. Dans les composants où vous souhaitez accéder à votre contexte, importez le contexte créé à l'étape 1 et utilisez `useContext` pour récupérer les données de contexte.

Voici un exemple de contexte qui gère un thème et une fonction de basculement de thème, et qui est accessible dans toute l'application:

Créez un dossier `contexts` a la racine de votre projet et mettez y un fichier `themeContext.tsx`

```tsx
import { createContext } from 'react';

export type Theme = 'light' | 'dark';

interface Context {
  theme: Theme;
  toggleTheme: () => void;
}

export const ThemeContext = createContext<Context>({
  theme: 'light',
  toggleTheme: () => {}
});
```

Mettez un Provider dans votre dossier `_app.tsx` pour que le theme soit accessible dans toute l’application

```tsx
import { useState } from 'react';
import { Theme, ThemeContext } from '../contexts/themeContext';

export default function App({ Component, pageProps }: AppProps) {
  const [theme, setTheme] = useState<Theme>('light');

  const toggleTheme = () => {
    setTheme(theme === 'light' ? 'dark' : 'light');
  }

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      <Component {...pageProps} />
    </ThemeContext.Provider>
  )
}
```

Vous pouvez maintenant l’utiliser comme suit

```tsx
import { useContext } from 'react';
import { ThemeContext } from '../../contexts/themeContext';
import Link from 'next/link';

export default function MyComponent() {
    const { theme, toggleTheme } = useContext(ThemeContext);
  
    return (
      <>
        <p>Thème actuel: {theme}</p>
        <button onClick={toggleTheme}>Basculer le thème</button>
      </>
    );
}
```

## Exemple 2 : User Context

```tsx
// ./contexts/userContext.ts
import { createContext } from 'react';

export type User = {
    id: string;
    username: string;
    loggedIn: boolean;
};

interface Context {
  user: User;
  updateUser: (user: User) => void;
}

export const defaultUser: User = {
    id: '1',
    username: 'default',
    loggedIn: false
};

export const UserContext = createContext<Context>({
  user: defaultUser,
  updateUser: () => {}
});

// ./pages/_app.tsx
import { User, UserContext, defaultUser } from '../contexts/userContext';

export default function App({ Component, pageProps }: AppProps) {
  const [user, setUser] = useState<User>(defaultUser);
  const updateUser = (user: User) => {
    setUser(user);
  }

  return (
    <UserContext.Provider value={{ user, updateUser }}>
       <Component {...pageProps} />
    </UserContext.Provider>
  )
}

// ./pages/userProfile.tsx
import { useContext } from 'react';
import { UserContext } from '../../contexts/userContext';

export default function MyComponent() {
    const { user, updateUser } = useContext(UserContext);
  
    return (
      <div>
        <p>User actuel: {JSON.stringify(user, null, 2)}</p>
        <button onClick={() => updateUser({ id: "uiveui-6666yg-757rf", username: "john doe", loggedIn: true })}>Update user</button>
      </>
    );
}
```
