= Starter

image:https://img.shields.io/badge/vert.x-3.8.1-purple.svg[link="https://vertx.io"]

This application was generated using http://start.vertx.io

== 用vertx做spring boot项目的 router ， 摒弃掉servlet

重用 spring web 的 controller, requestMapping 和 requestParam等， 减少移植的代码量
```
@RestController ， @Controller ， @RequestMapping  ， @RequestParam， @RequestBody
```
== 开始

```
    <dependency>
			<groupId>com.zzy</groupId>
			<artifactId>vertx-spring-boot-starter</artifactId>
			<version>1.0.3-SNAPSHOT</version>
		</dependency>
```

Controller demo
```
@RestController
@RequestMapping("/test")
public class Tes1tController {
}
```

param demo
```
    @RequestMapping(value = "/test3/:id", method = RequestMethod.PUT)
    public Map post(@RequestParam(value = "id") int id,
                    @RequestParam(value = "qq", required = false, defaultValue = "333") int qq,
                    @RequestBody() Map map) {
                    }
```
```
 @RequestMapping(value = "/test4", method = RequestMethod.GET)
    public Map post4(RoutingContext context) {
    }
```
Interceptor demo
```
@Component
public class Interceptor implements VertxHandlerInterceptor {
  @Override
  public boolean preHandle(RoutingContext context, Object handler) throws Exception {
    HandlerMethod handlerMethod = (HandlerMethod) handler;
    if(handlerMethod.getMethod().isAnnotationPresent(ResponseBody.class)){
      context.response().end("not support responsebody");
      return false;
    }
    return true;
  }
}

```

== Help

* https://vertx.io/docs/[Vert.x Documentation]
* https://stackoverflow.com/questions/tagged/vert.x?sort=newest&pageSize=15[Vert.x Stack Overflow]
* https://groups.google.com/forum/?fromgroups#!forum/vertx[Vert.x User Group]
* https://gitter.im/eclipse-vertx/vertx-users[Vert.x Gitter]


