##### SQL 判断（检查）字符串中是否包含另一个字符串

```sql
CHARINDEX ( expressionToFind , expressionToSearch [ , start_location ] )
```
> expressionToFind ：目标字符串，就是想要找到的字符串，最大长度为 8000 。  
> expressionToSearch ：用于被查找的字符串。  
> start_location：开始查找的位置，为空时默认从第一位开始查找。  
> 备注：  
> 大小写敏感  
> select charindex('test','this CHARINDEX Test'COLLATE Latin1_General_CS_AS)  
> 大小写不敏感 select charindex('Test','this CHARINDEX Test'COLLATE Latin1_General_CI_AS)  


```sql
replace()
```
> declare @item nvarchar(100)  
> set @item='英语好难';   
> select ID,title,author from Article  
> where LEN(REPLACE(@item,title,''))<len(@item);--根据替换后的长度进行判断>2  


```sql
PATINDEX
```
> 可以用来判断一个字符串中是否包含另一个字符串  
> select PATINDEX('%tes%','PATINDEX tes')  
> FREETEXT 语句所执行的功能又称做自由式全文查询。   
> FREETEXT 语句的语法格式为：FREETEXT({column | * }，‘freetext_string’)   
> column 是被搜索列，使用 “*” 时说明对表中的所有全文索引列进行搜索。  
> Freetext_string 参数指出所搜索的自由文本格式字符串。  


```sql
like
```
> 以通配符开头使用 LIKE 的查询将无法使用索引
