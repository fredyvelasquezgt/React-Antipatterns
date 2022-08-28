# Nesting Gotcha

En este ejemplo definimos un componente **Child** el cual se encuentra dentro del componente padre. El **Child** usa una funcion que esta definida en el padre, lo cual me evita definir un prop para esa funcion. A simple vista, esto funciona y se ve bien, pero hay un problema grande.

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

- Cada vez que el componente padre es renderizado, tambien re define el componente **Child**, lo que significa que recibe una nueva direccion en memoria, lo cual puede causar problemas de rendimiento en el futuro.

## Solucion
