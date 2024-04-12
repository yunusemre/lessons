`useEffect`

Useeffect sayfa ilk yüklendiği zaman çalışır. componentDidMount olarak düşünebilirsiniz.
Genellikle apileri call etmek için kullanılır. Aşağıda bir kullanım şekli var.

```
const [resourceType, setResouceType] = useState('post');
useEffect(() => {
    console.log('render');
});
return (
    <div>
        <button onClick={() => setResouceType('posts')}>Posts</button>
        <button onClick={() => setResouceType('users')}>Posts</button>
        <button onClick={() => setResouceType('comments')}>Posts</button>

        <h1>{resourceType}</h1>
    </div>
);
```

Bu şekilde kullanıldığı zaman herhangi bir değişiklik olduğunda useeffect değişir. bunu da componentDidUpdate olarak düşünebilirsiniz.

Doğru kullanımı da aşağıdakideki gibidir. Sebebi ise array dediğim kısım dependency olarak kullanılır ve değişiklik olduğu zaman çalışsın anlamına gelir.

```
useEffect(() => {
    console.log('mount');
}, []);
```

```
const [resourceType, setResouceType] = useState('post');
console.log('render');

useEffect(() => {
    console.log('render resourceType');
}, [resourceType]);

```

Herhangi bir state değişikliği olmadığı zaman componentde render işlemi gerçekleşmez.

Farklı kullanım alanları var mı?
Takip etmek istediğiniz her şey için kullanabilirsiniz. Mesela "window size"

```
const [windowWidth, setWindowWidth] = useState(window.innerWidth);

const handleResize = () => {
    setWindowWidth(window.innerHeight);
};
useEffect(() => {
    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
    // kullanılırsa event işlemleri artık aktif olmaz. Diğer koşullarda kaynak tüketir.
}, []);
```
