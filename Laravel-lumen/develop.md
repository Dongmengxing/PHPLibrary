```
数据库迁移 及 数据填充
创建迁移    php artisan make:migration create_users_table --create=users
执行数据填充    php artisan db:seed --class=ItemsTableSeeder
执行全量迁移并填充数据 php artisan migrate --seed

system表重置   php artisan migrate:reset --database system_hub --path=database/migrations/system_hub
system表构建    php artisan migrate --database system_hub --path=database/migrations/system_hub
system表重建    php artisan migrate:refresh --database system_hub --path=database/migrations/system_hub
system数据填充  php artisan db:seed --class=SystemHubSeeder
company表重置  php artisan migrate:reset --database company --path=database/migrations/company
company表构建  php artisan migrate --database company --path=database/migrations/company
company表重建  php artisan migrate:refresh --database company --path=database/migrations/company
company数据填充    php artisan db:seed --class=CompanyDatabaseSeeder


单元测试：
vendor/bin/phpunit --filter ApiUsableTest

php apidoc的文档生成功能:
安装:npm install apidoc -g
apidoc -i app/ -o apidoc/ -t mytemplate/
参考:http://apidocjs.com/#param-api

dingo 的api文档生功能:
php artisan api:docs --name Example --use-version v2 --output-file /path/to/documentation.md
参考:https://github.com/liyu001989/dingo-api-wiki-zh/blob/master/API-Blueprint-Documentation.md
```
