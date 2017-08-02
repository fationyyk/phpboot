# PhpBoot

[![Build Status](https://travis-ci.org/caoym/phpboot.svg?branch=master)](https://travis-ci.org/caoym/phpboot)
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/caoym/phpboot/master/LICENSE)

> phprs-restful 2.x 版本改名为PhpBoot。当前版本由于改动较大, 与1.x 版本不兼容。下载1.x版本请前往 [phprs-restful v1.x](https://github.com/caoym/phprs-restful/tree/v1.2.4)

**PhpBoot**是专为开发RESTful API 设计的PHP框架。它设计的初衷是尽可能**简化API开发**，包括:
* **更少的重复代码**
    
    如避免为开发API而在文档、接口定义、实现、数据库设计之间不停的重复和同步代码等。
* **更低的学习成本**

    如尽量遵循优秀的惯例, 尽可能扩展PHP原生能力, 避免不必要的抽象等。
* **更实用的功能**

    如Validation、ORM、文档生成、工作流引擎等。同时使用PhpBoot有助于提高代码质量。
* **更易于构建可扩展的应用**

    如它引导面向接口的开发, 提倡强类型的编程方式, 提供依赖注入能力, 低侵入性的集成方式, 提供钩子机制等。
    
## 主要特性
   
   * [基于Annotation的路由定义](https://caoym.gitbooks.io/phpboot/content/ji-ben-te-xing/lu-you.html)
   * [接口参数双向绑定](https://caoym.gitbooks.io/phpboot/content/ji-ben-te-xing/can-shu-bang-ding.html)
   * [Validation](https://caoym.gitbooks.io/phpboot/content/ji-ben-te-xing/can-shu-xiao-yan.html)
   * [依赖注入](https://caoym.gitbooks.io/phpboot/content/ji-ben-te-xing/yi-lai-zhu-ru.html)
   * [DB](https://caoym.gitbooks.io/phpboot/content/ji-ben-te-xing/shu-ju-ku.html)
   * [ORM](https://caoym.gitbooks.io/phpboot/content/ji-ben-te-xing/orm.html)
   * [自动文档和接口工具](https://caoym.gitbooks.io/phpboot/content/ji-ben-te-xing/wen-dang-shu-chu.html)
   * [钩子(Hook)](https://caoym.gitbooks.io/phpboot/content/ji-ben-te-xing/hook.html)
   * [工作流引擎(开发中...)](https://caoym.gitbooks.io/phpboot/content/ji-ben-te-xing/gong-zuo-liu.html)
   * 分布式支持(RPC)
   
## 安装和配置

   1. 安装composer(已安装可忽略)
   
       ```
       curl -s http://getcomposer.org/installer | php
       ```
       
   2. 安装PhpBoot
   
       ```
       composer require "caoym/phpboot"
       ```
       
   3. index.php加载PhpBoot
       
       ```PHP
      <?php
      require __DIR__.'/vendor/autoload.php';
      
      $app = \PhpBoot\Application::createByDefault(__DIR__.'/config/config.php');
      $app->loadRoutesFromPath(__DIR__.'/App/Controllers');
      $app->dispatch();
       ```
    
## 示例

   下面一个最基本的例子, 展示了依赖注入、基于Anntotaion的路由定义、参数绑定、参数校验和ORM, 完整的示例请见[phpboot-example](https://github.com/caoym/phpboot-example)
   
   
```PHP
   /**
    * 图书管理接口示例
    *
    * @path /books
    */
   class Books
   {
       /**
        * 查找图书
        *
        * @route GET /
        *
        * @param string $name  查找书名
        * @param int $offset 结果集偏移 {@v min|0}
        * @param int $limit 返回结果最大条数 {@v max|1000}
        *
        * @throws BadRequestHttpException 参数错误
        * @return Book[] 图书列表 
        */
       public function findBooks($name, $offset=0, $limit=100)
       {
           return \PhpBoot\model($this->db, Book::class)
               ->where(['name'=>['LIKE'=>"%$name%"]])
               ->limit($offset, $limit)
               ->get();
       }
   }
 ```
 
对应请求和响应

```
$ curl http://localhost/books/?name=PHP&offset=0&limit=10
[
   {
       "id": 1,
       "name": "PHP",
          "brief": "PHP 从入门到嫌弃",
       "pictures": []
   }
]
```
   
## 帮助和文档

   * **[在线文档](https://caoym.gitbooks.io/phpboot/content/)**
   * **QQ 交流群:185193529**
   * 本人邮箱 caoyangmin@gmail.com
   



