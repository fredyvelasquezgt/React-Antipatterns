# Prop drilling

## Problema

Un problema común al momento de construir grandes aplicaciones es que exista un componente en el top el cual contenga el **state**, pero después tenga un componente anidado el cual necesite usar ese **state** también, esto me lleva a que tenga que pasar el **state** como un prop a un montón de componentes child los cuales no requieran obligatoriamente de este **state**, esto se conoce como _prop drilling_, porque te hace querer barrenarte un agujero en la cabeza.

## Solución

1. Usar una librería de manejo de state como Redux, pero esta herramienta se puede quedar un poco grande para nuestros requerimientos.

2. Cuando tengo información global la cual se puede usar en muchas partes, como un formulario de autenticación, puedo compartir todo usando Context API.

```
<Provider> //Proveer informacion aqui
    <Child/> //Consumir informacion aqui
</Provider>
```

Veamos el ejemplo mejor implementado

1. Primero se necesita proveer la informacion en cierto punto del arbol de componentes.

2. Cualquier componente dentro del que tiene la data puede acceder a la misma desde cualquier nivel.

```
function PropDrilling() {

    const [count] = useState(0);

    return (
        <CountContext.Provider value={count}>
            <Child />
        </CountContext.Provider>
    )
}

function Child() {
    return <GrandChild />
}

function GrandChild() {

    const count = useContext(CountContext);

    return <div> {count} </div>
}
```

A simple vista se ve como la solucion definitiva, sin embargo, esto tiene un costo. El Context API es algo que se debe de usar con cuidado porque hace que mis componentes sean imposibles de reuitlizar si no cuentan con un Provider como un padre.

> La mayoria de aplicaciones solo cuentan con algunos valores a usar de forma global, esto puede ir dentro del Context, mientras que todo lo demás podría manejarse de forma más local.
