>unique
```
'name' => 'required|min:1|unique:versions,name,NULL,id,deleted_at,NULL'
```
>in
```
'sex' => 'integer|in:1,2',
```

>自定义验证模式
```
AppServiceProvider boot

Validator::extend('phone_number', function($attribute, $value, $parameters)
{
    return substr($value, 0, 2) == '01';
});

'phone' => 'required|numeric|phone_number|size:11'

正则表达式
'phone' => 'required|regex:/(01)[0-9]{9}/'
```
