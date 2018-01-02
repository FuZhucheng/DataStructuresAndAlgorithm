### java &与&& |与||的区别
#### 从简单程序去认识：
```
public class Test {

    public static void main(String[] args) {
        String str = null;
        if(str != null && !"".equals(str)){
            //do something
        }
        if(str != null & !"".equals(str)){
            //do something
        }
    }
}
```
#### **对于：&&**
```
if(str != null && !"".equals(str))

```
##### 当： str != null 的时候，接下来才会去执行： !"".equals(str)
##### 如果： str != null为false，那么这个时候，程序是处于短路的情况，则，!"".equals(str) 是不会执行的。
#### **对于：&**
```
if(str != null & !"".equals(str))
```
##### 不管： str != null 的结果如何(即true，false)，程序都会执行： !"".equal(str)
### 总结：
#### （一）问题总结：
#### 对于：&   -- >  不管怎样，都会执行"&"符号左右两边的程序
#### 对于：&& -- >  只有当符号"&&"左边程序为真(true)后，才会执行符号"&&"右边的程序。
#### (二)运算规则：
##### 对于：&  -- >  只要左右两边有一个为false，则为false；只有全部都为true的时候，结果为true
##### 对于：&& -- > 只要符号左边为false，则结果为false；当左边为true，同时右边也为true，则结果为true

