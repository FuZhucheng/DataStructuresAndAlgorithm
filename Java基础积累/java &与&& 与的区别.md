### java &��&& |��||������
#### �Ӽ򵥳���ȥ��ʶ��
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
#### **���ڣ�&&**
```
if(str != null && !"".equals(str))

```
##### ���� str != null ��ʱ�򣬽������Ż�ȥִ�У� !"".equals(str)
##### ����� str != nullΪfalse����ô���ʱ�򣬳����Ǵ��ڶ�·���������!"".equals(str) �ǲ���ִ�еġ�
#### **���ڣ�&**
```
if(str != null & !"".equals(str))
```
##### ���ܣ� str != null �Ľ�����(��true��false)�����򶼻�ִ�У� !"".equal(str)
### �ܽ᣺
#### ��һ�������ܽ᣺
#### ���ڣ�&   -- >  ��������������ִ��"&"�����������ߵĳ���
#### ���ڣ�&& -- >  ֻ�е�����"&&"��߳���Ϊ��(true)�󣬲Ż�ִ�з���"&&"�ұߵĳ���
#### (��)�������
##### ���ڣ�&  -- >  ֻҪ����������һ��Ϊfalse����Ϊfalse��ֻ��ȫ����Ϊtrue��ʱ�򣬽��Ϊtrue
##### ���ڣ�&& -- > ֻҪ�������Ϊfalse������Ϊfalse�������Ϊtrue��ͬʱ�ұ�ҲΪtrue������Ϊtrue

