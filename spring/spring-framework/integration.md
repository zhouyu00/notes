#### 可用的SpEL评价上下文
每个SpEL表达式依据于专用的context来评价。对于内置的参数，framework提供专用的缓存相关的元数据，例如参数名称。下面表格描述了上下文可用的项目，你可以用作key和条件计算。
| Name |Location|Description|Example|
|-----|-----|-----|-----|
|methodName|Root object|调用的方法名|#root.methodName|
|method|Root object|调用的方法|#root.method.name|
|target|Root object|调用的目标对象|#root.target|
|targetClass|Root object|调用的目标类|#root.targetClass|
|args|Root object|用于调用目标的参数（作为数组）|#root.args[0]|
|caches|Root object|当前方法调用的缓存集合|#root.caches[0].name|
|Argument name|Evaluation context|任意方法参数的名称，如果名称是不可用的（可能因为没有debug信息），参数名也可以在#a<#arg>下取得#arg代表参数索引|#iban或者#a0（你可以使用#p0或者#p<#arg>符号作为别名）|
|result|Evaluation context|方法调用的结果（缓存的值），只在unless表达式中，cache put表达式（计算key），或者cache evict 表达式（当 beforeInvocation是false）。对于支持的wrappers（例如Optional），#result引用实际的结果，而不是wrapper|#result|

### 8.2.2 @CachePut 注解
当缓存需要不在方法执行的介入下进行更新时，你可以使用@CachePut注解。这意味着方法总是被调用，它的结果总是被放入缓存（根据@CachePut选项）。它支持和@Cacheable相同的选项并且应当被用于缓存增长，而不是方法流优化。下面的例子使用了@CachePut annotation:
```java
@CachePut(cacheNames="book",key="#isbn")
public Book updateBook(ISBN isbn,BookDescriptor descriptor)
```
> 在相同的方法上使用@CachePut和@Cacheable注解强烈不推荐，因为它们具有不同的行为。当后者会导致方法调用跳过通过使用缓存，前者强制调用方法为了进行缓存更新。这会导致不受期待的行为，以及特殊边界情况的异常（例如，注解拥有互相排斥的条件），这样的声明应当被避免。需要强调的是，这样的条件不应当依赖于结果对象（即，#result变量），正如这些条件被验证有效提前到证实互斥


### 8.2.3 @CacheEvict注解
缓存抽象允许不仅是缓存存储的增长也包括清理。这个对于从缓存中移除脏的或者未使用的数据非常有用。与@Cacheable相反,@CacheEvict装饰的方法会执行缓存清理（即，方法的调用触发从缓存中移除数据）。类似于它的兄弟，@CacheEvict