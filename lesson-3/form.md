`React form`

Kütüphane olarak react-hook-form, redux-form, formik var. Ben react-hook-form kullanıyorum genel olarak.

```
const {
register,
handleSubmit,
watch,
formState: { errors },
} = useForm({
  defaultValues: {
    firstName: "",
    lastName: "",
  },
});

const onSubmit = (data) => console.log(data);
```

Form validasyonu içinde yup kütüphanesi
Hata mesajları için @hookform/error-message

```
const schema = yup
.object({
    firstName: yup.string().required("warning text"),
    age: yup.number().positive("Girdiğiniz değer pozitif olmalıdır.").integer().required(),
}).required()
```
