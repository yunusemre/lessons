`useState`

Component içerisinde data tutmaya yarar. Condition içersinde kullanılmaz.

```
const [count, setCount] = useState(1);
const [count, setCount] = useState({count: 4 });


// useState içerisine bir değer gelir.
function changeState(){
  return 4;
}

useState(changeState()) // Bu kullanımda her state değişiminde tekrar çağırılır.
useState(()=> changeState()) // Sadece bir kere çağırılır.
```

"setCount" iki şekilde kullanılabilir.
```
setCount(count + 1) // Bu şekilde kullanırsanız state değişmediği taktir de değeri hemen göremeyebilirsiniz.
setCount((prev)=> prev + 1) // Olarak kullanırsanız önceki değeri aldığı için güncel değeri göreceksinizdir.
// updater function deniyor. Buradaki amaç siz fonsiyon kullandığınız zaman react bir sonraki yani nextState sonuçlanana kadar pending state'de bekliyor.
```
Örnek:
```
setCount(count + 1);
console.log(count)
setCount(count + 1);
console.log(count)
```
```
setCount((prev)=> prev + 1);
console.log(count)
setCount((prev)=> prev + 1);
console.log(count)
```
Sayfanın içerisinde çok fazla useState kullanmak karmaşaya da sebebiyet verebilir, component'in satır sayısını uzatabilir. Bunun çözümleri mevcut ilerleyen derslerde göreceğiz.

İleri düzey useState;

```
const [number, setNumber] = useState<IState>({
    loading: false,
    isReady: false,
});

useEffect(() => {
    setTimeout(() => updateState({ isReady: true }), 2000);
}, []);

const updateState = (object: IState) => {
    setNumber((prevObject: IState) => ({ ...prevObject, ...object }));
};

```

-   Bir değeri değiştirmek için her zaman useState kullanmamıza gerek var mı? Hayır

```
const PER_PRICE = 4;
const [amount, setAmount] = useState(0);
const [totalPrice, setTotalPrice] = useState(0);
// const totalPrice = PER_PRICE * amount; gibi

const handleAmount = () => {
    setAmount(amount + 1);
};

useEffect(() => {
    setTotalPrice(PER_PRICE * amount);
}, [amount]);

return (
    <>
        <button onClick={() => handleAmount()}>Add price {amount}</button>
        <p>totalPrice: {totalPrice}</p>
    </>
);
```
