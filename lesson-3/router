```
import Box from '@/components/box';
import Home from '@/views/home';
import { Navigate, Outlet, createBrowserRouter, useRouteError } from 'react-router-dom';

export const router = createBrowserRouter([
    {
        path: '/',
        loader: () => ({ message: 'Hello Data Router!' }),
        element: (
            <Box> // Bu kısmı bir layout olarak düşünebiliriz. Header, Footer, Content alanı gibi bileşenleri ekleyebiliriz.
                <Navigate to="/home" /> // yönlendirme yapabiliriz.
                <Outlet /> // Bu kısım tüm routinglerin çalıştığı alandır. 
            </Box>
        ),
    },
    {
        path: '/home',
        errorElement: <TodosBoundary />,
        loader: () => ({ message: 'Hello Data Router!' }),
        element: <Home />,
    },
]);

export function TodosBoundary() {
    const error = useRouteError() as Error;
    return (
        <>
            <h2>Opppsss!!! 💥</h2>
            <p>{error?.message}</p>
        </>
    );
}
```
