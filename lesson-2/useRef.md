`useRef`

-   Basit bir obje oluşturuyor. özelliği ise hafızada aynı obje üzerinde işlem yaparak, aynı referansla size obje veriyor. Ama değiştiği zaman size değiştim bilgisini vermiyor. usestate ya da useeffect gibi değil.
-   useState gibi aldığı datayı sürekli update etmez.
-   html içersinde kullanılır ve dom'a ulaşmamızı sağlar. focus, blur gibi.
-   en önemli özelliklerinden birisi de eski datayı tutabilecek bir özelliğe sahip. (Tracking State Changes)
    component içerisinde geçmiş dataya ihtiyaç olursa kullanılabilir. Buna shouldComponentUpdate, didComponentUpdate ya da bu gibi eski ve yeni datayı karşılaştırdığımız methodlardaki ihtiyacı karşılayabilir.

```
function App(){
    const [name, setName] = useState('');
    const prevRef = useRef('');

    useEffect(() => {
        prevRef.current = name;
    }, [name]);

    return (
        <>
            <div className='p-4'>
                <input
                    value={name}
                    onChange={(e) => setName(e.target.value)}
                />
                <h1>
                    Benim adım <span style={{ color: 'red' }}>{name}</span> ve daha önceden
                    <span style={{ color: 'blue' }}> {prevRef.current}</span> adını kullanıyordum.
                </h1>
            </div>
        </>
    );

    // ------------ //
    const inputElement = useRef();
    const focusInput = () => {
      inputElement.current.focus();
    };

    return (
      <>
        <input type="text" ref={inputElement} />
        <button onClick={focusInput}>Focus Input</button>
      </>
    );
}
```

Sizce component'i hiç render etmeden form datasını alabilir miyim?

```
const nameRef = useRef(null);
console.log('render');

const submitForm = (event: any) => {
    event.preventDefault();
    const formData = new FormData(event.target);
    console.log(formData.get('name'));
    event.target.reset();
};
return (
    <>
        <form onSubmit={(e) => submitForm(e)}>
            <input type='text' name='name' ref={nameRef} />
            <button type='submit'>submit</button>
        </form>
    </>
);

```
