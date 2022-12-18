[retour](../README.md)

# Nextjs OAuth with github

## Initialisation

### Create a new project

Go on [supabase](https://app.supabase.com) and create a new project.

Get the url of your project: `Setting > API > URL`

### Enable OAuth

Go on your [Github](https://github.com/) profile.

Go on: `Settings > Developper mode > OAuth Apps > Register a new application`

You need to feel these informations:

- Application name: (Supabase OAuth)
- Homepage URL: (http://localhost:3000/)
- Authorization callback URL: (SUPABASE_URL/auth/v1/callback)

Now you're redirect on the __Supabase OAuth__ Authorization

Click on __Generate a new client secret__

### Configure Supabase

On your project page go on: `Authentication > Providers > Github`

Enable Github and copy paste your __Client ID__ and __Client Secret__ from Github

You're now ready to go!

## Build Nextjs app

```bash
npx create-next-app@latest my-project --typescript --eslint
cd my-project

npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

Add the following lines in `tailwind.config.js`:

```js
content: [
    "./pages/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}",
],
```

Replace the content of `styles/globals.css` with:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

* { box-sizing: border-box; }
```

Execute the folliwing commands to clean up your project:

```bash
rm -rf styles/Home.modules.css public/*.svg pages/api
```

Replace the content of `pages/index.tsx` with:

```js
export default function Home() {
  return (
    <div>
      <h1>Hello World!</h1>
    </div>
  )
}
```

(Optional) Commit that you've just set up tailwindcss

```bash
git add .
git commit -m "feat: 🔛 setup tailwindcss 🔛"
```

Start your build process

```bash
npm run dev
```

## Supabase js library

```bash
npm i @supabase/supabase-js
```

To communicate with supabase we are going to set ENV variables withyour API_KEY and API_URL. We will store these data in `.env.local`

```bash
touch .env.local
```

Content of `.env.local`

```bash
# You can find your values in supabase: `Settings > API`
NEXT_PUBLIC_SUPABASE_URL=YOUR_SUPABASE_URL
NEXT_PUBLIC_SUPABASE_ANON_KEY=YOUR_SUPABASE_ANON_KEY
```

A the root of your project create a file `client.tsx` in a folder `utils`

```js
import { createClient } from '@supabase/supabase-js';

const supabaseUrl:string = process.env.NEXT_PUBLIC_SUPABASE_URL ?? '';
const supabaseKey:string = process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY ?? '';

export const supabase = createClient(supabaseUrl, supabaseKey);
```

You're now ready to go! Commit your change and continue.

```bash
git add .
git commit -m "feat: 🔌 add client side supabase connection 🔌"
```

## Login Page

To make it simple we are going to do it in the index page. A more conventionnal way to do it is to put it in `pages/api/auth/` or `pages/auth/`

First of all, lets define the function `checkUser signIn signOut` and add a __useEffect__ to set the user variable

```js
// Needed imports
import { supabase } from '../utils/client'
import { useEffect, useState } from 'react'
```

```ts
//...
export default function Home() {
  const [user, setUser] = useState<any>(null);

  useEffect(() => {
    checkUser();
    window.addEventListener('hashchange', () => {
      checkUser();
    });
  }, []);

  const checkUser = async () => {
    const { data: { user } } = await supabase.auth.getUser();
    setUser(user);
  }

  const signInWithGithub = async () => {
    await supabase.auth.signInWithOAuth({
      provider: 'github'
    });
  }

  const signOut = async () => {
    await supabase.auth.signOut();
    setUser(null);
  }

  //...
}
```

Now, lets create a really simple UI to signIn/Out

```js
return (
    <>
      <section className='w-full h-screen flex flex-col justify-center items-center'>
        {/* DISPLAY CONNECTION STATUS */}
        <h1>
          {user ? (
            <span className='text-green-500'>You are logged in with {user.email}</span>
          ) : (
            <span className='text-red-500'>You are not logged in</span>
          )}
        </h1>
        
        {/* CONNECTION BUTTON */}
        <div className='mt-4'>
          {user ? (
            <button 
                onClick={signOut} 
                className='bg-red-500 text-white px-4 py-2 rounded'
            >
                Sign Out
            </button>
          ) : (
            <button 
                onClick={signInWithGithub} 
                className='bg-blue-500 text-white px-4 py-2 rounded'
            >
                Sign In with Github
            </button>
          )}
        </div>
      
      </section>
    </>
  )
```

You con now provide OAuth with Github on your nextjs app!

Commit your last changes!

```bash
git add .
git commit -m "feat: 💫 add OAuth with Github 💫"
```
