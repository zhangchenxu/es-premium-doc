---
home: true
heroText: ES Premium
tagline: 🚀一款更简洁、更优雅、更纯粹的ES查询框架。
actionText: 开始使用 →
actionLink: /pages/52d5c3/
bannerBg: none # auto => 网格纹背景(有bodyBgImg时无背景)，默认 | none => 无 | '大图地址' | background: 自定义背景样式       提示：如发现文本颜色不适应你的背景时可以到palette.styl修改$bannerTextColor变量

features: # 可选的
  - title: 简洁
    details: 致力于实现DSL语句的完美转化
    imgUrl: /img/jianjie.png
  - title: 优雅
    details: 一镜到底的函数式编码体验
    imgUrl: /img/youya.png
  - title: 纯粹
    details: 专注于ES查询，将查询做到极致
    imgUrl: /img/chuncui.png

# 文章列表显示方式: detailed 默认，显示详细版文章列表（包括作者、分类、标签、摘要、分页等）| simple => 显示简约版文章列表（仅标题和日期）| none 不显示文章列表
postList: none
---
<!-- <p align="center">
  <a class="become-sponsor" href="/pages/1b12ed/">支持这个项目</a>
</p> -->

<style>
.become-sponsor {
  padding: 8px 20px;
  display: inline-block;
  color: #11a8cd;
  border-radius: 30px;
  box-sizing: border-box;
  border: 1px solid #11a8cd;
}
</style>
<!-- 
<br/>
<p align="center">
  <a href="https://www.npmjs.com/package/vuepress-theme-vdoing" target="_blank"><img src="https://img.shields.io/npm/v/vuepress-theme-vdoing" alt="npm" class="no-zoom"></a>
  <a href="https://www.npmjs.com/package/vuepress-theme-vdoing" target="_blank"><img src="https://img.shields.io/npm/dt/vuepress-theme-vdoing" alt="npm" class="no-zoom"></a>
  <a href="https://github.com/xugaoyi/vuepress-theme-vdoing" target="_blank"><img src='https://img.shields.io/github/stars/xugaoyi/vuepress-theme-vdoing' alt='GitHub stars' class="no-zoom"></a>
  <a href="https://github.com/xugaoyi/vuepress-theme-vdoing" target="_blank"><img src='https://img.shields.io/github/forks/xugaoyi/vuepress-theme-vdoing' alt='GitHub forks' class="no-zoom"></a>
</p> -->

<br/>
<!-- <p align="center" style="color: #999;">
  赞助商 (进入注册为主题作者充电)
</p>
<p align="center">
  <a href="http://apifox.cn/a103xugaoyi" target="_blank"><img src="https://cdn.staticaly.com/gh/xugaoyi/blog-gitalk-comment@master/img/441669861566_.2bedplbm21hc.jpg" alt="npm" class="no-zoom" style="width: 300px;border-radius: 2px;"></a>
</p> -->

<!-- ## 🎖特别用户
::: cardList 3
```yaml
# - name: OpenHarmony
#   desc: 开放原子开源基金会
#   link: https://docs.openharmony.cn/pages/000000/
#   bgColor: '#f1f1f1'
#   textColor: '#2A3344'
- name: MyBatis-Plus官网
  desc: 🚀为简化开发而生
  link: https://baomidou.com/
  bgColor: '#f1f1f1'
  textColor: '#2A3344'
- name: Deepin 社区
  desc: Deepin 应用开发技术分享、DTK开发经验等
  link: https://docs.deepin.org
  bgColor: '#f1f1f1'
  textColor: '#2A3344'
- name: VForm官网
  desc: 低代码表单优选方案，拖拽式设计，一键生成源码
  link: http://www.vform666.com
  bgColor: '#f1f1f1'
  textColor: '#2A3344'
```
:::

<br/> -->

## 🎖 项目介绍
在项目中使用 ElasticSearch 进行查询时，通常会先编写相应的 DSL 查询语句。在确认 DSL 语句后，我们的需求实际上已经完成了大部分。然而，目前 Elasticsearch 的标准 Java API 实现并不是特别友好，这导致在 Java 实现上花费了相当多的时间。

es-premium 插件就是为了简化这个过程并提供更直观、更易于使用的方式来构建和执行 Elasticsearch 查询。es-premium 是一款能够无缝衔接 DSL 语句的查询插件，它为构建和执行 Elasticsearch 查询提供了简洁而强大的接口。

通过 es-premium 插件，你可以使用链式调用的方式构建查询，并且它提供了丰富的方法来支持各种查询类型、过滤条件和聚合操作。它的设计目标是让 Elasticsearch 查询在 Java 中更加容易和灵活，减少开发者在编写查询时的工作量和复杂性。

使用 es-premium 插件，你可以更专注于业务逻辑的实现，而无需过多关注底层的 Elasticsearch Java API 的使用细节。它能够大大简化查询的编写过程，提高开发效率，并且提供了对 Elasticsearch 高级功能的支持。

## 🎉 项目优势
> * 简化查询过程：简洁强大的接口，只需要调用相关接口就可以实现相关功能；
> * 原生ES查询：接口定义遵循原生的ES查询方法，不采用SQL语言转化，避免实现过程中产生歧义；
> * 执行效率高：采用树形结构的存储方式，支持更高的递归深度，执行效率也更快；

### 💎 查询场景描述
现在我们有一个既有的DSL语句，实现一个不太复杂的查询：
这个查询的逻辑是：查询 “`位于Phoenix，价格小于100000，房间数大于3，卫生间数大于3，ElementarySchool、MiddleSchool、HighSchool有任意两个`”的房子，按照“`价格升序排列`”，并且`聚合出这些房子的agent名字`

`上述场景对应的DSL语句`
::: details
```json
GET listing/_search
{
  "from": 0,
  "size": 10,
  "query": {
    "bool": {
      "filter": [
        {
          "match": {
            "city": {
              "query": "Phoenix"
            }
          }
        },
        {
          "range": {
            "price": {
              "from": null,
              "to": 100000
            }
          }
        },
        {
          "range": {
            "bedrooms": {
              "from": 3,
              "to": null
            }
          }
        },
        {
          "range": {
            "baths": {
              "from": 3,
              "to": null
            }
          }
        },
        {
          "bool": {
            "minimum_should_match": 2,
            "should": [
              {
                "match": {
                  "hasMiddleSchool": true
                }
              },
              {
                "match": {
                  "hasHighSchool": true
                }
              },
              {
                "match": {
                  "hasElementarySchool": true
                }
              }
            ]
          }
        }
      ]
    }
  },
  "sort": [
    {
      "price": {
        "order": "asc"
      }
    }
  ],
  "aggregations": {
    "cardinality_agg": {
      "cardinality": {
        "field": "agentName"
      }
    }
  }
}
```
:::

### 💎 ES Java API标准实现
```java
// 位于Phoenix，价格小于100000，bedrooms > 3, baths > 3
BoolQueryBuilder filter = QueryBuilders.boolQuery()
    .filter(QueryBuilders.matchQuery("city", "Phoenix"))
    .filter(QueryBuilders.rangeQuery("price").lt(100000))
    .filter(QueryBuilders.rangeQuery("bedrooms").gt(3))
    .filter(QueryBuilders.rangeQuery("baths").gt(3));
// ElementarySchool,MiddleSchool,HighSchool任意有两个
BoolQueryBuilder should = QueryBuilders.boolQuery()
    .should(QueryBuilders.matchQuery("hasElementarySchool", true))
    .should(QueryBuilders.matchQuery("hasMiddleSchool", true))
    .should(QueryBuilders.matchQuery("hasHighSchool", true))
    .minimumShouldMatch(2);
filter.filter(should);
// 聚合条件
TermsAggregationBuilder agentNameAgg = AggregationBuilders.terms("agent_name_agg")
    .field(EsFieldEnum.AGENT_NAME.getCode()).size(10);
// 开始查询
SearchSourceBuilder queryBuilder = new SearchSourceBuilder();
queryBuilder.query(filter)
    .aggregation(agentNameAgg)
    .from(1)
    .size(10);

SearchRequest searchRequest = new SearchRequest();
String[] indices = {"listing"};
searchRequest.indices(indices);
searchRequest.source(queryBuilder);
```

### 🔥 ES Premium实现
```java
EsQueryWrapper<SearchResultInfo> queryWrapper = new EsQueryWrapper<>();
queryWrapper.lt("price", 10000)
   .match("city", "Phoenix")
   .gt("bedrooms", 3)
   .gt("baths", 3)
   .shouldMinimum(2,
      eSchool -> eSchool.match("hasElementarySchool", true),
      mSchool -> mSchool.match("hasMiddleSchool", true),
      hSchool -> hSchool.match("hasHighSchool", true)
    ).order(List.of(new QueryOrderInfo("price", SearchOrderEnum.ASC)))
    .page(1, 10)
    .aggregate(new AggregationInfo("agentName", AggregationTypeEnum.CARDINALITY))
    .indices("listing");
```

这个🌰可以比较直观的说明，我们的ES Premium具体是什么东西了。详细操作可参见API文档：[**API文档**](/pages/a2f161/)

### 🚀 效率对比
关于es-premium执行的效率，可以参考对比图，该对比基于上述的查询场景进行查询，每种实现方式执行10次，取平均值。
平均值分别为：
> * es-premium 815ms
> * es原生API  899ms
<div style="text-align:center">
  <img src="https://github.com/WaitingMan/file-warehouse/raw/main/img/es-premium-speed.jpeg" alt="Image" width="400" height="300">
</div>


<br/>

<style>
  pre code {
    white-space: pre-wrap;
    font-family: inherit;
    text-align: left;
  }
</style>

<!-- ## ⚡️未来...

::: tip
期待 [VuePress v2.0](https://github.com/vuepress/vuepress-next) 以及 [VitePress](https://github.com/vuejs/vitepress) 的正式发布...

届时，VuePress 1.x 编译慢的缺点将得到极大的改善。我将会视情况把主题升级至 VuePress v2.0 或 VitePress。还希望大家多多 [:sparkling_heart:支持](/pages/1b12ed/) 哟，持续关注吧~
::: -->

<br/>

<!-- ## 💎 公众号
`有趣研究社`是本人对各种有趣的、好玩的、沙雕的创意和想法以在线小网站或者文章的形式表达出来，比如：
- [小霸王游戏机](https://game.xugaoyi.com)
- [爱国头像生成器](https://avatar.xugaoyi.com/)
- [到账语音生成器](https://zfb.xugaoyi.com/)

还有更多好玩的等你去探索吧~

::: center
<img src="https://fastly.jsdelivr.net/gh/xugaoyi/image_store@master/blog/qrcode.zdqv9mlfc0g.jpg"  style="width:190px;" />
:::

<br/> -->

<!-- ## ⚡ 反馈与交流

在使用过程中有任何问题和想法，请给我提 [Issue](https://github.com/xugaoyi/vuepress-theme-vdoing/issues)。
你也可以在Issue查看别人提的问题和给出解决方案。

或者加入我们的交流群：

<table>
  <tbody>
    <tr>
      <td align="center" valign="middle">
        <img src="https://cdn.staticaly.com/gh/xugaoyi/blog-gitalk-comment@master/img/0.4pp7r95mdai0.jpeg" class="no-zoom" style="width:120px;margin: 10px;">
        <p>vdoing微信群(添加我微信备注"进群")</p>
      </td>
      <td align="center" valign="middle">
        <img :src="$withBase('/img/qrcode/qqq.webp')" alt="群号: 694387113" class="no-zoom" style="width:120px;margin: 10px;">
        <p>vdoing QQ群: 694387113</p>
      </td>
    </tr>
  </tbody>
</table> -->

<style>
  .page-wwads{
    width:100%!important;
    min-height: 0;
    margin: 0;
  }
  .page-wwads .wwads-img img{
    width:80px!important;
  }
  .page-wwads .wwads-poweredby{
    width: 40px;
    position: absolute;
    right: 25px;
    bottom: 3px;
  }
  .wwads-content .wwads-text, .page-wwads .wwads-text{
    height: 100%;
    padding-top: 5px;
    display: block;
  }
</style>
