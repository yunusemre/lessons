-   Neden ihtiyaç duyarız (http stateless bir protocoldur, TCP statefuldur.)
-   Hangi sorunun çözümü
-   redux ile redux toolkit (redux'ın bir workflow'u, immer js içeriyor, daha basite indirgenmiş hali) arasında nasıl bir fark var?
-   Datayı kaybetmemek için state manager yanında kullanılabilecek bir şey var mı? (redux-persist)
    `redux toolkit`

```
const initialState = {
    isLogin: false,
    username: null
};

const appSlice = createSlice({
    name: 'apps',
    initialState,
    reducers: {
        resetState: () => initialState,
        isLogin: (state, { payload }) => state.isLogin = payload;
        setUserName: (state, { payload }) => state.username = payload;
    },
    extraReducer: (builder) => {
        .addCase(getById, (state, action) => {
            <!-- examples -->
            <!-- https://redux-toolkit.js.org/api/createAsyncThunk -->
        })
    },
    selectors: {
        selectSlice: (state) => state,
    },
});

export const { setUserName, isLogin } = appSlice.actions;
export const { selectSlice } = counterSlice.selectors // reselect
export default appSlice.reducer;
```

```
import { combineReducers } from '@reduxjs/toolkit';

const rootReducer = combineReducers({
    apps: appReducer,
});

export default rootReducer;
```

```
import rootReducer from './root-reducer';
import storage from 'redux-persist/lib/storage' // defaults to localStorage for web
import { type Action, type ThunkAction, configureStore } from '@reduxjs/toolkit';
import { persistReducer, persistStore } from 'redux-persist';

const persistConfig = {
    key: 'project',
    storage,
    whitelist: ['apps'],
};
const persistedReducer = persistReducer(persistConfig, rootReducer);
export const store = configureStore({
    reducer: persistedReducer,
    devTools: true,
    middleware: (getDefaultMiddleware) =>
        getDefaultMiddleware({
            serializableCheck: false,
        }).concat(),
});

export const persistor = persistStore(store);
export type AppDispatch = typeof store.dispatch;
export type RootState = ReturnType<typeof store.getState>;
export type AppThunk<ReturnType> = ThunkAction<ReturnType, RootState, unknown, Action<string>>;
```
```
import { AppDispatch, RootState } from '@/store';
import { type TypedUseSelectorHook, useDispatch, useSelector } from 'react-redux';


// hook kısmına bunu ekleyebiliriz. Bununla birlikte app'in state kısmına daha kolay erişebiliriz.
export const useAppDispatch = () => useDispatch<AppDispatch>();
export const useAppSelector: TypedUseSelectorHook<RootState> = useSelector;
```
```
<Provider store={store}>
    <PersistGate persistor={persistor}>
        {...}
    </PersistGate>
</Provider>
```

State managerda performans arttırıcı neler olabilir?

selectors dediğimiz özellikle almak istediğimiz bir değer varsa redux'dan bunu almamıza yardımıcı olur.
Bunun yerine farklı kütüphanelerde kullanılabilir. reselect, immutable js gibi. redux selectorlar reselect kütüphanesini kullanılarak oluşturulmuştur.
