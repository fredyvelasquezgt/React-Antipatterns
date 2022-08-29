# Prop plowing

## Problema

Esta es una situación en la cual le pasamos demasiados props a un componente, esto provoca que el codigo sea vea desordenado y repetitivo.

```
function Page() {

    const data = {
        id: 23,
        name: 'Fredy',
        bio: 'Mi nombre es Fredy',
        age: 19,
        avatar: ' :D '
    }

  return (
      <User id={data.id} name={data.name} bio={data.bio} age={data.age} avatar={data.avatar} />
  );
}
```

## Solución

Usar el operador **spread** para pasar todos los props al mismo tiempo. Esto hace que el codigo sea mas eficiente pero un poco menos explicito, por lo que es recomendado solo usarlo cuando realmente se esté trabajando con un componente el cual reciba demasiados props.

```
function Page() {

    const data = {
        id: 23,
        name: 'Fredy',
        bio: 'Mi nombre es Fredy',
        age: 19,
        avatar: ' :D '
    }

  return (
      <User {...data} />
  );
}
```
