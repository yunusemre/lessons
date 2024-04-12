`useCallback`

```
function useToggle(initialValue) {
  const [value, setValue] = useState<boolean>(false);
  const toggle = useCallback(() => {
    setValue(v => !v);
  }, []);
  return [value, toggle];
}

function App() {
  const [isDarkMode, toggleDarkMode] = useToggle(false);
  return (
    <button onClick={toggleDarkMode}>
      Toggle color theme
    </button>
  );
}
```

useMemo ile useCallback arasında fark var mıdır?

- function olarak dönebiliyor.
- useMemo arguments (parametre almaz) ama useCallback alır.
