`useContext`

Tüm logic'i kapsamaya yarar.

useContext birazdan HOC' e benzer. useContext ile HOC arasında farklar çok olmamakla birlikte useContextde değişiklik varsa consumerlarda da değiliklik olur. HOC sadece wrapper görevi görür.

```
const ThemeContext = React.createContext()

function App(){
    const [theme, setTheme] = useState("dark")

    return (
        <ThemeContext.Provider value={{ theme, setTheme }}>
            <ChildComponent />
        </ThemeContext.Provider>
    )
}

function ChildComponent() {
  const { theme, setTheme } = useContext(ThemeContext)
  return (
    <>
      <div>The theme is {theme}</div>
      <button onClick={() => setTheme("light")}>Change To Light Theme</button>
    </>
  )
}
// Bu kısım context'in global olarak kullanılmasına imkan sağlıyor. Bir hook gibi kullanabilirsiniz.
export const useTheme = () => {
    const context = useContext(ThemeContext);
    if (context === undefined) {
        throw new Error('message');
    }
    return context;
};

```

```
const { theme, setTheme } = useTheme(); // olarak kullanılabilir.
```
