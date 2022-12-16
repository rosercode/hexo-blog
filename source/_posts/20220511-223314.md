---
title: Java | 反射应用
date: 2022-05-11 22:33:15
tag:
---

(๑•̀ㅂ•́) ✧ Java 反射应用 -- 判断一个 JavaBean 的属性是否为 null

<!-- more -->

在正常的业务逻辑中，我们会存在下面的需求：

在前端发送数据到后端，需要对数据进行校验，其中一项为判断是否为空，我们可以通过下面的方式来判断是否有参数是否为空

```java
@GetMapping(value = "/expressRemark")
@NeedLoginAuth
public CommonResponse insertRemark(RemarkEntity remark){
    response.setCode(-1);
    // 数据校验
    if (remark.getRemarkInfo() == null || remark.equals("")){
        response.setMessage("评论内容不能为空");
    }
    remark.setRemarkId(Integer.parseInt(CommonUtils.uuid()));
    remark.setUserId(this.user.getUserId());
    remark.setRemarkStatue(0);
    log.info("客户端插入评论信息，用户名为 {}，评论的内容为 {}",user.getUserNum(),remark.getRemarkInfo());
    response.setMessage("评论发布完成，等待管理员审核");
    remarkServiceImp.insertRemark(remark);
    return response;
}

```

上面的方法不够灵活，而当我们添加属性、或者修改一个属性名称后，需要对重新对这部分代码进行修改。那我们应该如何实现对一个灵活的、动态的实现上面的功能。

我们可以通过 **反射** 的机制来对一个类的属性进行检查：

```java
/**
 * @author wangsh
 * @date 2022/5/9 23:27
 */
public class MainClass {

    public static void main(String[] args) throws ClassNotFoundException, IllegalAccessException {
        RemarkEntity remark = new RemarkEntity();
        if(isNullObj(remark)){
            System.out.println("对象中的所有属性都为空......");
        }
    }
    /**
     * @date 2022-05-09 23:53:37
     * @param object
     * @return
     */
    public static boolean isNullObj(Object object){
        Class clazz = (Class)object.getClass(); // 得到类对象
        Field fields[] = clazz.getDeclaredFields(); // 得到所有属性
        boolean flag = true; //定义返回结果，默认为true
        for(Field field : fields){
            field.setAccessible(true);
            Object fieldValue = null;
            try {
                fieldValue = field.get(object); //得到属性值
                Type fieldType =field.getGenericType();//得到属性类型
                String fieldName = field.getName(); // 得到属性名
                System.out.println("属性类型："+fieldType+",属性名："+fieldName+",属性值："+fieldValue);
            } catch (IllegalArgumentException e) {
                e.printStackTrace();
            } catch (IllegalAccessException e) {
                e.printStackTrace();
            }
            if(fieldValue != null){  //只要有一个属性值不为null 就返回false 表示对象不为null
                flag = false;
                break;
            }
        }
        return flag;
    }
}
```

上面的依旧不够灵活，因为有些属性我们可以允许为 null 的。

那我们如何动态的指定某些属性，可以为空，或者不能为空？

这需要用到 Java **注解** ，使用 **注解** 给一个类的属性打一个 **标记** ，在使用反射获取属性时，检查属性的 **标记** ，动态的判断。

下面是我修改后的一个函数：

```java

```

