#### 查询出广东省所有的市、县语句的思路总结

- - -

首先，第一个查询语句：

 - 我们查询用s_provinces表，用递归的原理跟自己进行关联，然后查询条件cityName=广东的
```
select p.id,p.cityName,s.cityName,x.cityName from s_provinces p    
	join s_provinces s on s.parentId=p.id 
	join s_provinces x on x.parentId=s.id 
where p.cityName='广东省'
```

第二查询语句：

 - 查询的是没有县区的地方
```
    select s.id,p.cityName,s.cityName,null from s_provinces s
    	join s_provinces p on s.parentId=p.id
    where p.cityName='广东省';
 ```

最后：

 - 用union all进行联合查询，union all会列举所有符合条件的查询结果
```
    select p.id,p.cityName,s.cityName,x.cityName from s_provinces p 
	join s_provinces s on s.parentId=p.id 
	join s_provinces x on x.parentId=s.id where p.cityName='广东省'
	
    union all
    
    select s.id,p.cityName,s.cityName,null from s_provinces s
    	join s_provinces p on s.parentId=p.id
    	where p.cityName='广东省';
```

