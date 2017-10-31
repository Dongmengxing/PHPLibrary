```
protected $guarded = ['id', 'created_at','updated_at','deleted_at'];

public function getTableColumns()
    {
        return $this->getConnection()->getSchemaBuilder()->getColumnListing($this->getTable());
    }

    //获取guarded之外的参数
    public function getOutsideGuarded()
    {
        return array_values(array_diff($this->getTableColumns(),$this->getGuarded()));
    }
```
