---
title: mybatis-plus 结合 pagehelper 分页查询 total 值错误的情况之一
date: 2022-11-30
tags:
---

mybatis-plus + pagehelper 分页查询 total 值错误的情况之一 (๑•̀ㅂ•́) ✧

<!-- more --> 

在使用 **mybatis-plus** 进行数据库操作，**pagehelper** 进行相关查询的分页操作，遇到 **total** 和预期不符合的情况之一

## 错误用法

数据库查询出来的数据并不是最后 **service** 层返回的数据，要进行转换后返回

```java
@Service
public class OrderServiceImpl implements OrderService{

    @Resource
    private OrderMapper orderMapper;


    @Override
    public PageInfo<OrderResponse> page(OrderManagePageRequest request) {
        PageHelper.startPage(request.getPageNum(), request.getPageSize());
        List<Order> orders = orderMapper.selectList(null);
        List<OrderResponse> response = orders.stream().map(order -> {
            OrderResponse orderResponse = new OrderResponse();
            BeanUtils.copyProperties(order, orderResponse);
            return orderResponse;
        }).collect(Collectors.toList());
        return new PageInfo<>(response);
    }
}

```

## 正确用法

在转换时，要创建一个新的 **PageInfo** 对象的实例，并把之前 **PageInfo** 实例的属性拷贝过去

```java
@Service
public class OrderServiceImpl implements OrderService{

    @Resource
    private OrderMapper orderMapper;

    @Override
    public PageInfo<OrderResponse> page(OrderManagePageRequest request) {
        PageHelper.startPage(request.getPageNum(), request.getPageSize());
        List<Order> orders = orderMapper.selectList(null);
        PageInfo<Order> page = new PageInfo<>(orders);
        List<OrderResponse> response = orders.stream().map(order -> {
            OrderResponse orderResponse = new OrderResponse();
            BeanUtils.copyProperties(order, orderResponse);
            return orderResponse;
        }).collect(Collectors.toList());
        PageInfo pageResponse = new PageInfo(response);
        BeanUtils.copyProperties(page,pageResponse);
        return pageResponse;
    }
}

```

## 介绍

情况举例:

- 数据库框架: mybatis-plus
- 查询分页插件: pagehelper

mybatis-plus 是一个对 **mybatis** 进行封装后的一个框架，兼容基础的 **mybatis**，并进行简单的扩展 - 提供了一些方便、已用的特性。

[pagehelper](https://github.com/pagehelper/Mybatis-PageHelper) 是一个针对 **mybatis** 的分页插件。

> mybatis-plus 默认提供一个分页功能，这里并没有使用

