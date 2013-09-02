
情况如下：表中有条六条记录。 其中张三和王五 的记录有重复
TableA
id  customer PhoneNo
001 张三     777777
002 李四     444444
003 王五     555555
004 张三     777777
005 张三     777777
006 王五     555555

如何写一个sql语句将TableA变成如下

001 张三     777777
002 李四     444444
003 王五     555555

---

--假定id为主键

	delete tablea
	from tablea tt
	where  exists(
	select 1
	from tablea 
	where customer=tt.customer
	and phoneno=tt.phoneno
	and id<tt.id)

	delete a from TableA a join 
	TableA b 
	on a.customer  = b.customer and a.PhoneNo = b.PhoneNo where a.id>b.id

--测试环境
create table TableA ( id varchar(3),customer varchar(5),PhoneNo varchar(6))
insert into TableA select '001','张三','777777'
union all select '002','李四','444444'
union all select '003','王五','555555'
union all select '004','张三','777777'
union all select '005','张三','777777'
union all select '006','王五','555555'
--删除语句
delete  from TableA  
where id not  in
(select id=min(id) from TableA
group by customer,PhoneNo
)
--结果 select * from TableA  
id   customer PhoneNo 
---- -------- ------- 
001  张三       777777
002  李四       444444
003  王五       555555

参考网址：
[1](http://www.360doc.com/content/10/0408/13/536925_22087659.shtml)

