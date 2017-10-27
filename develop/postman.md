## postman使用技巧

> 域名或者公用部分可以创建环境变量

> postman 在 Pre-request Script 中提供使用JavaScript设置全局变量等

```
// 设置全局变量
pm.globals.set("token", "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOjEsImF1ZCI6InVzZXIiLCJpc3MiOiJodHRwOi8vMTI3LjAuMC4xOjgzMzMvYXBpL2FjY291bnRzL2JpbmRfdXNlciIsImlhdCI6MTUwNDc3ODg1MiwiZXhwIjoxNTY1MjU4ODUyLCJuYmYiOjE1MDQ3Nzg4NTIsImp0aSI6IkFXV3hvc0plTGduRUQ0cGcifQ.EKr6KVckTXHtVN2Txy-LvDi8a8B3eKbQfIcPaUtZVSo");

// 使用全局变量
Authorization:{{token}}
```
