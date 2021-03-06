### Mybatis使用sql方式分页

***

##### Mapper

Mapper之中的代码如下：

```sql
/*
 * 查询收藏的商品，使用分页
 */
@Select("SELECT id, user_id, item_id, add_price, add_time, created, updated FROM user_collection_info"
        + " where user_id = #{userId} ORDER BY created DESC LIMIT #{offset},#{limit}")
List<WishList> getWishListByLimit(@Param("userId") long userId, @Param("limit") int limit, @Param("offset") int offset);
```



##### Service

Service之中的代码如下：

```java
//查询收藏的商品，使用分页
public List<WishList> getWishListByLimit(Long userId, Integer limit, Integer offset)
{
    return wishListMapper.getWishListByLimit(userId, limit, offset);
}
```



##### Controller

Controller之中的代码如下：

```javascript
//查询收藏的商品，使用分页
@RequestMapping(value = "getMarkList", method = RequestMethod.GET)
public @ResponseBody
JsonResult getMarkList(Long userId, Integer pageSize,Integer pageStart)
{

    List<WishList> list2=wishListService.getWishListByLimit(userId,pageSize,pageStart);
    return JsonResult.builder().code(ResultCode.SUCCESS.val()).message(ResultCode.SUCCESS.msg()).result(list2).build();
}
```

主要的问题其实是在sql语句之中，加入了控制的参数limit和offset，分别在上述对应的是pageSize和pageStart，也就是说，**每页的数据量和数据的开始的位置**。**limit和offset的位置是定好了的**，如果不使用Map来将key和value对应起来，而是用`(int limit, int offset)`这种方式的时候，只能直接按照`offset, limit`的顺序来，也就是先定义每页的初始位置，然后在定义每页的数量，参数的位置是`(int offset， int limit)`，这样定义的offset和limit也没用，只能是`(0,1)`。

ref:

1.[mybatis框架的两种分页](https://blog.csdn.net/leozhou13/article/details/50394242),   2.[mybatis框架的两种分页](https://blog.csdn.net/leozhou13/article/details/50394242)