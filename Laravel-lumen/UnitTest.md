>第一层，测试所有的接口能不能调通
>第二层 
```
<?php

use Laravel\Lumen\Testing\DatabaseMigrations;
use Laravel\Lumen\Testing\DatabaseTransactions;

class ApiUsableTest extends TestCase
{
    // phpunit.xml 删除 bootstrap="bootstrap/app.php", 设置 processIsolation="true" 时,这方法可用
    public function testApis()
    {
        $router = app('Dingo\Api\Routing\Router');
        $dataRoutes = $router->getRoutes();

        $routes = [];
        foreach ($dataRoutes as $collection) {
            foreach ($collection->getRoutes() as $route) {
                $uses = array_key_exists('uses', $route->getAction())
                    ? $route->getAction()['uses']
                    : $route->getActionName();

                $routes[] = [
                    'host' => $route->domain(),
                    'method' => implode('|', $route->methods()),
                    'uri' => $route->uri(),
                    'name' => $route->getName(),
                    'action' => $uses,
                    'middleware' => $route->getMiddleware() ? implode(", ", $route->getMiddleware()) : "No",
                    'protected' => $route->isProtected() ? 'Yes' : 'No',
                    'versions' => implode(', ', $route->versions()),
                    'scopes' => implode(', ', $route->scopes()),
                    'rate' => $this->routeRateLimit($route),
                ];
            }
        }

        foreach ($routes as $route)
        {
            echo explode('|', $route['method'])[0];
            echo '/'.$route['uri'];

            $response = $this->json(explode('|', $route['method'])[0], '/'.$route['uri'], ['name' => 'Sally'], ['Accept'=>'application/vnd.lumen.v1+json']);
            $response->assertResponseStatus(200);

            echo '√';

        }

    }

//    // phpunit.xml 保留 bootstrap="bootstrap/app.php", 设置 processIsolation="false" 时, additionProvider 可用,但是这时候模拟 json 请求,统一都是未找到
//    /**
//     * @dataProvider additionProvider
//     */
//    public function testApisWithProvider($route)
//    {
//
//            echo explode('|', $route['method'])[0];
//            echo '/'.$route['uri'];
//
//            $response = $this->json(explode('|', $route['method'])[0], '/'.$route['uri'], ['name' => 'Sally'], ['Accept'=>'application/vnd.lumen.v1+json']);
//            $response->assertResponseStatus(200);
//
//            echo '√';
//    }
//
//
//
//    public function additionProvider()
//    {
//        $router = app('Dingo\Api\Routing\Router');
//        $dataRoutes = $router->getRoutes();
//
//        $routes = [];
//        foreach ($dataRoutes as $collection) {
//            foreach ($collection->getRoutes() as $route) {
//                $uses = array_key_exists('uses', $route->getAction())
//                    ? $route->getAction()['uses']
//                    : $route->getActionName();
//
//                $routes[] = [
//                    'host' => $route->domain(),
//                    'method' => implode('|', $route->methods()),
//                    'uri' => $route->uri(),
//                    'name' => $route->getName(),
//                    'action' => $uses,
//                    'middleware' => $route->getMiddleware() ? implode(", ", $route->getMiddleware()) : "No",
//                    'protected' => $route->isProtected() ? 'Yes' : 'No',
//                    'versions' => implode(', ', $route->versions()),
//                    'scopes' => implode(', ', $route->scopes()),
//                    'rate' => $this->routeRateLimit($route),
//                ];
//            }
//        }
//
//        return [$routes];
//
//    }

    protected function routeRateLimit($route)
    {
        list($limit, $expires) = [$route->getRateLimit(), $route->getRateLimitExpiration()];
        if ($limit && $expires) {
            return sprintf('%s req/s', round($limit / ($expires * 60), 2));
        }
    }

}

```
