title: 使用 Grape 构建 API
date: 2015-06-25 14:17:32
tags: [rails, grape]
---

现在rails界有各种各样的api技术架构

rails + jbuilder
grape + rails
grape + sinatra
grape + ActionController::Metal
grape + goliath, 基于EventMachine的异步框架

今天只讲 ** 使用 Grape 构建 API** , 很多人争执 使用原生rails构建api不是很好么
这里不做争论

感觉  [@42thcoder](https://ruby-china.org/42thcoder) 比较中肯

Grape 的好处:

- built-in params validation, 声明式语法
- 更方便地产出复杂 JSON, Grape Entity + present 很好用
- 不用写 route, 代码即路由, 一目了然
- 做 versioning 代码更少
- 与 Rails 部分松耦合
- Grape Swagger ( 支持 desc )

你提到的问题:
- 代码量没有少: 少了
- 调用栈增加了: I don't see any problem.
- Filter 不通用. 没有通用的需求, Rails 写后台管理( 管理员用 ), Grape 写给客户端( 普通用户 )写接口, 可重用的 Filter 非常少
- Helper 不通用. 多数 Helper 用来 render HTML tag, 产出 JSON 时不需要; 真想通用, include 进来就好.

PS:
纯 jbuilder 生成api 结构, 数据还是很慢的, 而且很麻烦, 我比较懒惰.

---

切入正题, 这个小demo
使用mongodb做数据库, rails + grape少不了, swagger生成 api文档

1 生成文件夹

`mkdir -p app/api/v1`

```ruby /app/api/base.rb
class Base < Grape::API
  mount V1::Root
end

```

```ruby /app/api/v1/root.rb

require 'grape-swagger'

module V1
  class Root < Grape::API

    version 'v1'
    format :json
    content_type :json, "application/json;charset=UTF-8"
    formatter :json, Grape::Formatter::Jbuilder

    before do
      header['Access-Control-Allow-Origin'] = '*'
      header['Access-Control-Request-Method'] = '*'
    end

    add_swagger_documentation base_path: "/api", api_version: 'v1', mount_path: 'doc', markdown: GrapeSwagger::Markdown::KramdownAdapter
  end
end

```

2

``` js /app/assets/javascripts/api.js
//= require jquery
//= require jquery_ujs
//= require swagger-ui

//= require api/doc
//= require_self

```

``` css /app/assets/stylesheets/api.css
/*
 *= require swagger-ui
 *= require_self
 */

```

```coffee /app/assets/javascripts/api/doc.coffee
$ ->
  if $("#swagger-ui-container").length > 0
    swaggerUi = new SwaggerUi
      url: "/api/v1/doc"
      dom_id: "swagger-ui-container"
      supportedSubmitMethods: ['get', 'post', 'put', 'delete']
      onComplete: (swaggerApi, swaggerUi)->
        $('pre code').each (i, e)-> hljs.highlightBlock e
      onFailure: (data)->
      docExpansion: "list"
    swaggerUi.load()
    console.log("v1")

```

访问 http://localhost:3000/doc/v1
