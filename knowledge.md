
 ```
在使用类似如下引用时
foreach($tests as &$test){
    
}

应在foreach 结束的位置释放引用

foreach($tests as &$test){
    
}
unset($test);
```
