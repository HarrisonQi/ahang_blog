---
title: "MyBatis-Plus 读写 Mysql的Json类型字段数据"
date: "2020-06-05"
categories: 
  - "java"
  - "mybatis-plus"
tags: 
  - "java"
  - "json"
  - "kotlin"
  - "mybatis-plus"
  - "mysql"
coverImage: "MyBatis-Plus-分页查询返回的-数据总数total为0-的解决方案-banner.jpg"
---

Mybatis-Plus是一款相当优秀的开源框架, 为单表操作提供了极大的便利. 这次阿航在写服务端时, 需要对MySQL的json类型字段进行操作, 忙活了一阵, 终于找到了解决方案, 并在本篇文章进行记录.

## 需具备的条件

本篇文章环境:

| 环境 | 版本号 |
| --- | --- |
| Mybatis-Plus | 3.3.2 |

本篇文章假定:

1. 你掌握Java/Kotlin基础(注解)
2. 你掌握Mybatis以及Mybatis-Plus的基本使用
3. 你了解FastJSON或Gson

\[epcl\_box type="notice"\]如果还不具备以上的条件, 阅读本篇文章可能会有阻碍! 建议先满足条件后再尝试阅读!\[/epcl\_box\]

\[epcl\_box type="information"\]老规矩, 速度快的同学直接向下拉. 看核心代码.\[/epcl\_box\]

## 场景

我们拥有一个json类型的数据库字段, 我们在进行写操作时, 不希望将对象转为json字符串再存数据库. 读数据也是一样. 我们希望这一切自动完成.

## 准备工作

我们先来创建一个数据库表:

```
CREATE TABLE `mybatis_json_test`  (
  `id` int(10) NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `extra_object` json NULL,
  `extra_list` json NULL,
  `extra_array` json NULL
);

INSERT INTO `mybatis_json_test`
VALUES
	( 1, '{\"id\": 1, \"name\": \"2\"}', '[{\"id\": 1, \"name\": \"2\"}]', '[{\"id\": 1, \"name\": \"2\"}]' );
```

## 实战开始

### 创建表对应实体类

首先创建实体类`MybatisJsonTest`:

\[epcl\_tabs\] \[epcl\_tab title="Java"\]

```
import com.baomidou.mybatisplus.annotation.IdType;
import com.baomidou.mybatisplus.annotation.TableField;
import com.baomidou.mybatisplus.annotation.TableId;
import com.baomidou.mybatisplus.annotation.TableName;
import com.baomidou.mybatisplus.extension.handlers.FastjsonTypeHandler;

import java.io.Serializable;
import java.util.List;

@TableName(autoResultMap = true)
public class MybatisJsonTest implements Serializable {

    @TableId(type = IdType.AUTO)
    private Integer id;

    @TableField(typeHandler = FastjsonTypeHandler.class)
    private ExtraNode extraObject;

    @TableField(typeHandler = FastjsonTypeHandler.class)
    private List extraList;

    @TableField(typeHandler = FastjsonTypeHandler.class)
    private ExtraNode[] extraArray;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public ExtraNode getExtraObject() {
        return extraObject;
    }

    public void setExtraObject(ExtraNode extraObject) {
        this.extraObject = extraObject;
    }

    public List getExtraList() {
        return extraList;
    }

    public void setExtraList(List extraList) {
        this.extraList = extraList;
    }

    public ExtraNode[] getExtraArray() {
        return extraArray;
    }

    public void setExtraArray(ExtraNode[] extraArray) {
        this.extraArray = extraArray;
    }

    class ExtraNode implements Serializable {

    private Integer id;
    private String name;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
}
```

\[/epcl\_tab\]

\[epcl\_tab title="Kotlin"\]

```
@TableName(autoResultMap = true)
class MybatisJsonTest : Serializable {
    @TableId(type = IdType.AUTO)
    var id: Int? = null

    @TableField(typeHandler = FastjsonTypeHandler::class)
    var extraObject: ExtraNode? = null

    @TableField(typeHandler = FastjsonTypeHandler::class)
    var extraList: List? = null

    @TableField(typeHandler = FastjsonTypeHandler::class)
    var extraArray: Array? = null

    inner class ExtraNode : Serializable {
        var id: Int? = null
        var name: String? = null
    }
}
```

\[/epcl\_tab\] \[/epcl\_tabs\]

> 💡 代码解析: 实际上我们只是创建了`mybatis_json_test`表的实体类. 这里的重点为两个注解: `@TableName(autoResultMap = _true_)`以及`@TableField(typeHandler = FastjsonTypeHandler_.class_)`

\[epcl\_box type="information"\]FastjsonTypeHandler可以替换为你想要的TypeHandler! 比如GsonTypeHandler!\[/epcl\_box\]

增加这两个注解后, 我们实际上已经实现了我们的效果.

### 验证效果

创建类文件`MybatisJsonTestMapper`, 定义Mapper:

\[epcl\_tabs\] \[epcl\_tab title="Java"\]

```
import com.baomidou.mybatisplus.core.mapper.BaseMapper;
import org.springframework.stereotype.Repository;

@Repository
public interface MybatisJsonTestMapper extends BaseMapper {
}
```

\[/epcl\_tab\] \[epcl\_tab title="kotlin"\]

```
import com.baomidou.mybatisplus.core.mapper.BaseMapper
import org.springframework.stereotype.Repository

@Repository
interface MybatisJsonTestMapper : BaseMapper
```

\[/epcl\_tab\] \[/epcl\_tabs\]

创建类文件`TestController`, 定义Controller:

\[epcl\_tabs\] \[epcl\_tab title="Java"\]

```
import com.baomidou.mybatisplus.core.conditions.query.LambdaQueryWrapper;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;

@RestController
@RequestMapping("/test")
public class TestController {

    @Autowired
    private MybatisJsonTestMapper mybatisJsonTestMapper;

    @GetMapping
    public List listAll() {
        return this.mybatisJsonTestMapper.selectList(new LambdaQueryWrapper<>());
    }
}
```

\[/epcl\_tab\] \[epcl\_tab title="kotlin"\]

```
import com.baomidou.mybatisplus.core.conditions.query.LambdaQueryWrapper
import org.springframework.web.bind.annotation.GetMapping
import org.springframework.web.bind.annotation.RequestMapping
import org.springframework.web.bind.annotation.RestController

@RestController
@RequestMapping("/test")
class TestController(private val mybatisJsonTestMapper: MybatisJsonTestMapper) {
    @GetMapping
    fun listAll(): List {
        return mybatisJsonTestMapper.selectList(LambdaQueryWrapper())
    }
}
```

\[/epcl\_tab\] \[/epcl\_tabs\]

如果上述步骤没有问题, 访问`/test`本地接口, 应该会返回:

```
[
  {
    "id": 1,
    "extraObject": { "id": 1, "name": "2" },
    "extraList": [
      { "name": "2", "id": 1 }
    ],
    "extraArray": [
      { "id": 1, "name": "2" }
    ]
  }
]
```

\[epcl\_box type="success"\]至此, 成功完成!\[/epcl\_box\]

## 核心代码

实体类文件上方需要增加注解:

```
@TableName(autoResultMap = true)
```

json字段对应的实例变量需要增加注解:

\[epcl\_tabs\] \[epcl\_tab title="Java"\]

```
@TableField(typeHandler = FastjsonTypeHandler.class)
```

\[/epcl\_tab\] \[epcl\_tab title="Kotlin"\]

```
@TableField(typeHandler = FastjsonTypeHandler::class)
```

\[/epcl\_tab\] \[/epcl\_tabs\]

`FastjsonTypeHandler`可更换为`GsonTypeHandler`等.

## 感谢

[mybatis-plus读取JSON类型](https://www.cnblogs.com/liangweiping/p/12835377.html)

## 结语

不得不再次感叹Mybatis-Plus的强大. 在使用原生Mybatis的时候, 需要在`mapper.xml`文件中添加N个`<resultMap>`! 现在一行搞定. 比起从前, 不知节省了多少寿命😭😭😭😭
