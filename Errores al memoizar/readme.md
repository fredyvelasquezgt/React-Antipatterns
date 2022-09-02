# Errores al memoizar

## Problema

Componente que hace mucho trabajo:

1. Maneja dos piezas de estado.
2. Necesitamos correr una operación costosa cada vez que el valor cambia

```
function WorkHard() {

    const [count, setCount] = useState(0);
    const [other, setOther] = useState(0);

    const total = expensiveCalculation(count)'\;

    return (
        <>
        </>
    );
}
```

El problema con la implementación actual es que cada vez que el estado cambie en el componente, va a correr otra vez el calculo costoso, inclusive si solo depende del valor _count_. Es bastante obvio que existen dificultades de rendimiento.

## Solución

Esta es una oportunidad perfecta para usar el hook **useMemo**. Lo que hará es recordar el último valor, y ejecutará la funcion actual cuando la información en la dependencia cambie.

`const total = useMemo(() => expensiveCalculation(count), [count]);`

Existe el mismo escenario para las funciones, el cual es manejado con el hook **useCallback**
