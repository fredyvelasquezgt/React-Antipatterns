# Programar más inteligente

## Problema

Cuando trabajamos usando el **useState**, puede ser tentador almacenar toda la informacion en un solo objeto, esto hace que el codigo se vea mas limpio y que al momento de llamarlo sea mas facil. Sin embargo, **React 18**, hace _automatic batching_ cada vez que se actualiza el estado, esto quiere decir que llamar al **setState** multiples veces en la misma funcion no disparar multiples re renderizaciones.

Lo anterior hace que mi informacion sea dificil de extraer en un **Custom Hook**. Anteriormente (cuando se usaban los componentes con clases) era comun organizar el codigo de la siguiente forma:

```
<Smart> //Manejar informacion aqui
    <Dumb data={val} > //Mostrar informacion aqui
</Smart>
```

## Solucion

Realmente no existe nada de malo con el patron anterior, sin embargo, existen formas mas sencillas de extraer la logica en un **Custom Hook** .

A continuacion construyo un componente con mucha informacion para los estados.

```
function Feature() {

    const [state, setState] = useState({...});
    const [count. setCount] = useState(0);
    const [coords, setCoords] = useState({x:0, y:0});
    const [title, setTitle] = useState('hey');
    const [theme, setTheme] = useState('dark');
    const [ts, setTs] = useState(Date.now());

}
```

A medida que las cosas se pongan mas complejas, o quiera usar esa informacion en otro componente, extraigo la informacion en mi **Custom Hook**, el cual al final de cuentas, es solo una funcion de Javascript, esto me permite tratar virtualmente mis componentes como componentes _dumb_ , mientras que mis **Custom Hooks** son los encargados de manejar la logica mas compleja

```
function Feature() {

    const [count, setCount] = useState(0);
    const [coords, setCoords] = useState({x:0 , y:0 });

    const {title, theme, ts} = useMetadata();
}

function useMetadata() {
    const [title, setTitle] = useState('hey');
    const [theme, setTheme] = useState('dark');
}
```
