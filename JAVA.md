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

