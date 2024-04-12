`axios`

Axios en çok kullanılan data çekme kütüphanesidir.

https://npmtrends.com/axios-vs-fetch-vs-request-vs-superagent

-   Neden çok kullanılıyor?
-   Interceptor nedir? : You can intercept requests or responses before they are handled by then or catch.

```
axios.interceptors.request.use(function (config) {
    // config includes headers!
    return config;
  }, function (error) {
    return Promise.reject(error);
  });

// Add a response interceptor
axios.interceptors.response.use(function (response) {
    return response.data;
  }, function (error) {
    return Promise.reject(error);
  });
```

axios hangi konularda yardımcı olur?

-   Cancellation
-   URL-Encoding Bodies
-   Community
