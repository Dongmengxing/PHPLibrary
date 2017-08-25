> require dingo api

>
```
use App\Transformers\GetTransformer;
use Illuminate\Support\Collection;
use League\Fractal;

//处理单个模型
    public function transformItemData($item, $transformerName, $include = '')
    {
        $get_transformer = new GetTransformer();
        $transformer = $get_transformer->getByName($transformerName);
        $resource = new Fractal\Resource\Item($item, $transformer);
        $fractal = new Fractal\Manager();
        return $fractal->parseIncludes($include)->createData($resource)->toArray();
    }
    //处理列表模型
    public function transformCollectionData($collection, $transformerName, $include = '')
    {
        $get_transformer = new GetTransformer();
        $transformer = $get_transformer->getByName($transformerName);
        $resource = new Fractal\Resource\Collection($collection, $transformer);
        $fractal = new Fractal\Manager();
        return $fractal->parseIncludes($include)->createData($resource)->toArray();
    }
    //自动判断使用单个或列表模型,判断存在误差
    public function transformData($data, $transformerName, $include = '')
    {
        $get_transformer = new GetTransformer();
        $transformer = $get_transformer->getByName($transformerName);
        if ($data instanceof Collection) {
            $resource = new Fractal\Resource\Collection($data, $transformer);
        } else {
            $resource = new Fractal\Resource\Item($data, $transformer);
        }
        $fractal = new Fractal\Manager();
        return $fractal->parseIncludes($include)->createData($resource)->toArray();
    }

```
