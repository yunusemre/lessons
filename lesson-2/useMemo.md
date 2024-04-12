`useMemo`

-   Memorize işlemini yapar. Aynı işlemi tekrar tekrar yapmaktan kurtarır.
-   Ne gibi problemler oluşturabilir?
-   Nerelerde kullanabiliriz? (complex hesaplamalarda, hiç değişmeyen sabit değerlerde)

```
function App(){
    const [number, setNumber] = useState<number>(0);
    const [dark, setDark] = useState<boolean>(false);
    const double: number = slowFunction(number);

    const themeStyle = {
        background: dark ? 'black' : 'white',
        color: dark ? 'white' : 'black',
    };

    return (
        <>
            <input
                type='number'
                value={number}
                onChange={(e) => setNumber(parseInt(e.target.value))}
            />
            <button onClick={() => setDark((prev) => !prev)}>Change Theme</button>
            <h1 style={themeStyle}>{double}</h1>
        </>
    );
}
```

-   Gibi örneklerde de kullanılabilir.

```
const filteredUsers = useMemo(
    () => users.filter(user => user.name.includes(filter)),
    [users, filter]
);
```
