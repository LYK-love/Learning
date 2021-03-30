VgahnJ_Sg9I6



presion：结果的数字位数（包括小数点后）

scale：精度。如果是负数，就代表对小数点前的n位四舍五入。 如果不输入，则缺省值为0.

e.g.

```
7,456,123.89    NUMBER(*,1)  7456123.9
7,456,123.89	NUMBER(9)	7456124

```



GET /数据库第三章课件

Host: 饭皇.com

User--Agent: Mozilla/5.0 xxx

Origin: http:// lyk.com



`ASC`升序排列 ， `AESC`降序排列

`distinct`关键字：确保得到的键值对不会重复

```
SELECT *
FROM agents
WHERE city IN ( Duluth,  Dallas )
```

```
select cid from customers where  discnt <= all( select discnt from customers where city = Duluth )
```

