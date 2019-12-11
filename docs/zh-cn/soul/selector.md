---
title: 选择器规则详解
keywords: soul
description: 选择器规则详解
---

## 说明

* 本篇主要详解soul网关中，选择器与规则的概念，以及如何使用。


## 大体理解

* 首先明白:选择器与规则是一对多的关系，而插件对选择器又是一对多的关系。

* 我们想在插件里面做事情的时候，我们是不是希望根据我们的配置，达到满足条件的，我们插件才去执行它？

* 选择器和规则就是为了让插件在满足特定的条件下，才去执行我们想要的，这个你首先头脑要点数。

* 数据结构可以参考之前的 [数据库设计](db.md)


## 选择器 

![](https://yu199195.github.io/images/soul/selector.png)

 * 选择器详解：
 
     * 名称：为你的选择器起一个容易分辨的名字
     * 类型：custom flow 是自定义流量。full flow 是全流量。自定义流量就是请求会走你下面的匹配方式与条件。全流量则不走。
     * 匹配方式：and 或者or 是指下面多个条件是按照and 还是or。
     * 条件：
        * header：请求头，里面的module字段以match的值是什么。举个列子：你在header请求头加了个module字段值是order，那么就填写module字段match匹配order。
        * 可以添加多个条件，按照匹配类型这多个条件是and 还是or去匹配。
     * 是否开启：打开才会生效
     * 打印日志：打开的时候，当匹配上的时候，会打印匹配日志。
     * 执行顺序：当多个选择器的时候，执行顺序小的优先执行。 

 * 选择器建议 : 可以uri来匹配，根据前缀 （/contextPath） ,来进行匹配。
 
## 规则
 ![](https://yu199195.github.io/images/soul/rule.png)

 * 规则详解：
     * 名称：为你的规则起一个容易分辨的名字
     * 匹配方式：and 或者or 是指下面多个条件是按照and 还是or。
     * 条件：
        * header：请求头，里面的method字段以match的值是什么。举个列子：你在header请求头加了个method字段值是findById，那么就填写method字段match匹配findById。
        * 可以添加多个条件，按照匹配类型这多个条件是and 还是or去匹配。
     * 是否开启：打开才会生效
     * 打印日志：打开的时候，当匹配上的时候，会打印匹配日志。
     * 执行顺序：当多个选择器的时候，执行顺序小的优先执行。 
     * 处理：每个插件的规则处理不一样，具体的差有具体的处理，具体请查看每个对应插件的处理。

*  规则建议：选可以uri来匹配，根据具体的url路径,来进行匹配。  
    
    
## 条件详解

* uri 匹配 （推荐）

  * uri匹配是根据你请求路径中的uri来进行匹配，在接入网关的时候，前端几乎不用做任何更改。
  
  * 在选择器中，推荐使用uri中的前缀来进行匹配，而在规则中，则使用具体路径来进行匹配。
  
  * 该匹配方式的时候，在匹配字段名称可以任意填写，匹配字段值需要正确填写。
  
* header 匹配

  *   header是根据你的http头中的设置来进行匹配。这个应该明白把？
  
*  query 匹配

  * 这个是根据你的uri中的查询参数来进行匹配，比如 /test?a=1&&b=2 ，那么可以选择该匹配方式。
   
  * 上述就可以新增一个条件 query  a   =  1  

*  ip匹配

  * 这个是根据 http调用方的 ip来进行匹配。
  
  * 尤其是在waf插件里面，如果发现一个ip地址有攻击，可以新增一条匹配条件，填上该ip，拒绝该ip的访问。
  
  * 如果在soul前面使用了nginx代理，为了获取正确的ip，你可能要参考 [dev-iphost](dev-iphost.md)
 
* host匹配

  * 这个是根据 http调用方的host来进行匹配。
    
  * 尤其是在waf插件里面，如果发现一个host地址有攻击，可以新增一条匹配条件，填上该host，拒绝该host的访问。
    
  * 如果在soul前面使用了nginx代理，为了获取正确的host，你可能要参考 [dev-iphost](dev-iphost.md)  
    
*  post匹配

  * 这个是使用 `requestDTO`中的字段名称与值来进行匹配，使用了反射技术，不推荐使用。

          