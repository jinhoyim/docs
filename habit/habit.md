# Habit
좋은 개발 습관을 위해 정리.

## Type 또는 Category를 변수로 가지지 않기
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

## 추상화 하는 과정
추상화를 할 때 상위 개체를 식별하고 하위 개체를 알게 되었다면 상위에서 하위로 내리는 방법보다 우선 하위 개체로 모두 내린 후에 상위 개체로 올려가는 방법을 사용하면 잘못된 추상화를 만드는 경우가 줄어들 수 있음.

