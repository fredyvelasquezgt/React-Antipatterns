# Nesting Gotcha

En este ejemplo definimos un componente **Child** el cual se encuentra dentro del componente padre. El **Child** usa una función que esta definida en el padre, lo cual me evita definir un prop para esa función. A simple vista, esto funciona y se ve bien, pero hay un problema grande.

```
function Parent () {
    const [count, setCount] = useState(0);

    const handleClick = () => setCount(count + 1);

    const Child = () => {
        return <button onClick={handleClick}>+</button>
    }

    return (
        <div>
            <Child />
        </div>
    );
}
```

## Problema

- Cada vez que el componente padre es renderizado, también re define el componente **Child**, lo que significa que recibe una nueva dirección en memoria, lo cual puede causar problemas de rendimiento en el futuro.

## Solución

- No definir completamente un componente **Child**
- Mover al componente **Child** afuera del componente padre y pasarle la funcion como un prop.

```
const Child = ({onClick}) => {
    return <button onClick={onClick}>+</button>
}

function Parent() {

    const [count, setCount] = useState(0);

    const handleClick = () => setCount(count + 1);

    return (
        <div>
            <Child onClick={handleClick} />
        </div>
    )
}
```
