# Divs inutiles

## Problema

Es común que cuando se esté creando un componente nuevo, existan fallos como el de tratar de retornar dos elementos hermanos juntos, esto es porque cada componenete solo puede tener un elemento raiz.

```
//Esto da error:
function Frag() {

    return (
        <nav> </nav>
        <article></article>
    );
}
```

El problema se puede solucionar colocando todo adentro de un div. Esto funciona perfectamente bien, pero ocasiona otros problemas con el css y la accesibilidad.

## Solucion

Para lidiar con el problema, React cuenta con un componente _Fragment_, el cual le dice a React que no renderice nada como el componente padre.

```
function Frag() {

    return (
        <>
            <nav></nav>
            <article></article>
        </>
    );
}
```
