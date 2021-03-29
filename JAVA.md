# 										JAVA

## 一. mybatis

#### 	1.mapper.xml的写法

```
	mysql中  <  的表示方法：&lt;
```

```sql
# any_value的使用：当存在group by且展示的字段没有聚合函数包裹的时候
# 	使用any_value() 包裹字段即可
select any_value(u.id),
       any_value(u.username),
       any_value(u.sex),
       any_value(u.card_id),
       group_concat(p.phone),
       any_value(u.role),
       any_value(u.forest_id),
       any_value(u.entry_time)
       from ffrms_user u
       left join ffrms_user_phone p on (u.id = p.user_id)
       group by p.user_id;
```



#### 2.Springboot分页

- 引入依赖

```java
<!-- https://mvnrepository.com/artifact/com.github.pagehelper/pagehelper-spring-boot-starter -->
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper-spring-boot-starter</artifactId>
    <version>1.3.0</version>
</dependency>
```

- 在集合查询前使用`PageHelper.startPage(pageNum,pageSize)`,并且*中间不能穿插执行其他SQL*

- 查询代码：

  ```java
  @PostMapping("/users")
      public PageInfo<UserSearchDTO> getSearchUsers(
          @RequestBody UsersSearchCriteria usersSearchCriteria) {
          PageHelper.startPage(Optional.ofNullable(usersSearchCriteria.getPageNum()).orElse(1),
              Optional.ofNullable(usersSearchCriteria.getPageSize()).orElse(10));
          return new PageInfo<>(userService.getUsersSearch(usersSearchCriteria));
      }
  ```

  返回的结果：

  ```json
  {
      "total": 1,
      "list": [],
      "pageNum": 1,
      "pageSize": 10,
      "size": 1,
      "startRow": 1,
      "endRow": 1,
      "pages": 1,
      "prePage": 0,
      "nextPage": 0,
      "isFirstPage": true,
      "isLastPage": true,
      "hasPreviousPage": false,
      "hasNextPage": false,
      "navigatePages": 8,
      "navigatepageNums": [
          1
      ],
      "navigateFirstPage": 1,
      "navigateLastPage": 1
  }
  ```

  