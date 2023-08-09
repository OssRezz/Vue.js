# Vet Project

## Install TailWindCss in vue

1. Ejecutamos el comando `npm install -D tailwindcss postcss autoprefixer` para instalar las dependencias
2. Ejecutamos el comando `npx tailwindcss init -p` Este comando nos va a generar dos archivos tailwind.config.cjs y postcss.config.cjs
3. En el archivo tailwind.config.cjs vamos agregar los archivos donde tenemos las clases de tailwind para generar los estilos al final de la hoja, solo se agregaran los estilos de las clases que hemos utilizado, esto funciona con algo llamado JIT (just in time). La intención de esto es optimizar el código y no cargar toda la hoja de estilos de tailwind

Los archivos los debemos agregar en el array de content:

```
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    './src/**/*.{vue,js,ts,jsx,tsx}'
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

4. En nuestra hoja de estilos, debemos agregar las siguientes lineas de código:

```
@tailwind base;
@tailwind components;
@tailwind utilities;

```

5. Documentación tailwind: https://tailwindcss.com/
6. Headless ui: https://headlessui.com/
