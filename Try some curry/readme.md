# Try some Curry

## Problema

El codigo puede volverse sucio en JSX cuando manejo los eventos. Lo que pasa, es que puedo tener una función que tome como primer argumento un evento, pero uno o más valores como el argumento secundario, esto quiere decir que al momento de llamarlo necesito descomponer una **arrow function** , lo cual puede resultar dificultoso si lo hago en varios lugares.

```
function Page() {

    const handleIt = (e: any, v: number) => {
        console.log(e,v);
    }

    return <>
        <div>

        <input onChange={(e) => handleIt(e, 1)} />
        <input onChange={(e) => handleIt(e, 2)} />
        <input onChange={(e) => handleIt(e, 3)} />

        </>
}
```

## Solución

Un truco bastante ingenioso de Javascript es crear una funcion Curry. Básicamente, una función Curry es aquella que retorna otra función. La función exterior toma los argumentos personalizados, mientras que la función interior maneja el evento que le es pasado por default, esto evita tener que crear una arrow function por cada evento

```
function Page() {

    const handleIt = (v: number) => {
        return (e:any) => console.log(e,v);
    }

    return <>
        <div>

        <input onChange={handleIt(1)} />
        <input onChange={handleIt(2)} />
        <input onChange={handleIt(3)} />


        </>
}
```
