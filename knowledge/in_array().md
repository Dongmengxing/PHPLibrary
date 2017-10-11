
## in_array()
```
bool in_array ( mixed $needle , array $haystack [, bool $strict = FALSE ] )
$needle 针
$haystack 海

在大海中捞针

$strict true开启严格模式 比较值同时比较类型
```

## 注意事项
```
in_array(0, 's')  返回true

因为PHP是弱类型语言, 在 0 与 ‘s’ 比较时, 既number 与 string 进行比较,
string类型会首先转化成number,然后在进行比较操作,'s'转换成number 为0在, 值相同, 所以返回true

建议在使用时开启严格模式,同时比较值和类型
```
