# AntiPattern
개발하면서 나오는 안티패턴과 권장되는 코드로 변경한 것을 정리. 알고 있는 것보다 습관이 되어야 하는 것들.


## Type 또는 Category를 변수로 가지고 있을 때
안티패턴 : 현재는 한 클래스 안에서 Product Type에 따라 서로 다른 메서드를 호출하는 경우를 표현함. 좀 더 복잡한 참조관계에서는 swtich 문이 Product를 참조하는 곳에 존재할 수도 있고 case 문 안에서의 메서드 호출 역시 Product가 참조하는 것을 이용하는 경우 더 좋지 않은 코드가 됨.

```cs
class Product
{
    public string Category { get; }

    public void SomeMethod()
    {
        switch(Category)
        {
            case "book" :
                this.SomeMethod1();
                break;
            
            case "drink" :
                this.SomeMethod2();
                break;
        }
    }
}
```

권장
```cs
class Product
{
    protected string Cateogry { get; }
    public abstract string SomeMethod();
}

class Book : Product
{
    public override void SomeMethod()
    {
        
    }
}

class Drink : Product
{
    public override void SomeMethod()
    {
        //...
    }
}
```