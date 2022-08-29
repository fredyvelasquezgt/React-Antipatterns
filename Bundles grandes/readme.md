# Bundles grandes

## Problema

Uno de los problemas con las apps que son complejas es que también son grandes, con esto nos referimos a que cuentan con un exceso de código de Javascript, esto repercute a que cuando la app sea lanzada a producción, tendrá problemas de velocidad al inicializarse dado que el navegador debe de manejar todo el bundle de Javascript.

## Solucion

Si estamos usando Next.JS o create-react-app los cuales estan construidos con webpack, es sencillo implementar la division de codigo.

Normalmente, para importar algo, usamos el **import**

```
import {hiMom} from './helpers';

function Page() {

}
```

Sin embargo, los navegadores ahora aceptan importanciones dinámicas, las cuales me permiten cargar módulos de forma asíncrona usando la función **import**.

Cuando webpack llega a ese codigo, automaticamente sabe que debe de separar esa parte en un bundle diferente, el cual no será requerido sino hasta después de la inicialización de la página. Esta alternativa funcion bien para Javascript plano, pero no tanto para componentes de React.

```
function Page() {

    const hello = async = () => {
        const {hiMom} = await import('./helpers');
        return hiMom;
    };
}
```

Por otra parte, React cuenta con una feature para soportar una carga **lazy**. Me permite realizar importaciones dinámicas con componentes de React.

```
import React, {Suspense} from 'react';

const Button = React.lazy(() => import('./Button'));ss

function Page() {
    return (
        <Suspense fallback={<div>Loading...</div>}>
            <Button />
        <Suspense>
    );
}
```
