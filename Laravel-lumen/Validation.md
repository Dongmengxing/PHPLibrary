>unique
```
'name' => 'required|min:1|unique:versions,name,NULL,id,deleted_at,NULL'
 or
'name' => 'required|string|unique:company.skuattributes,name,NULL,deleted_at',

```
>in
```
'sex' => 'integer|in:1,2',

```
