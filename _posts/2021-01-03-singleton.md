---
layout: post
title: 싱글톤 패턴(Sigleton Pattern)
subtitle: 안드로이드 싱글톤 패턴에 대하여
tags: [개발, JAVA, Android, 디자인패턴]
---

이번에 다니는 회사에서 싱글톤 패턴(Sigleton Pattern) 사용에 대한 회의를 하게 되었다. 회의 준비를
위해 미리 싱글톤 패턴에 대해 공부할 필요가 있었고, 공부한 내용을 정리하여 블로그에 작성하려고 한다.

## 싱글톤 패턴(Singleton Pattern)이란?

싱글톤 패턴(Singleton Pattern)이란 애플리케이션이 실행될 때 어떤 클래스가 최초 한번만 메모리를 할당(**static**)하고,
그 메모리에 인스턴스를 만들어 사용하는 패턴이다. 한번 생성한 인스턴스를 계속해서 재사용하는 패턴으로 자바의 경우 생성자를
`private`으로 선언하고, `getInstance()` 메서드로 인스턴스를 반환하는 식으로 만든다.  

안드로이드의 경우 SharedPreferences 사용 클래스, Application 클래스 등에 사용한다.

## 사용하는 이유  

1. 인스턴스를 매번 새로 생성하지 않아 **메모리 낭비를 방지**할 수 있다. 
2. 전역으로 만들어진 인스턴스이기 때문에 모든 애플리케이션 영역에서 같은 **데이터를 공유**할 수 있다. 
3. 싱글톤 클래스는 한번 만들고 나면 재사용하기 때문에 첫 생성 이후에는 성능이 좋아진다는 장점도 있다.  

안드로이드의 경우 액티비티나 클래스 사이에 클래스 전달이 번거롭기 때문에 클래스를 어디서든 사용할 수 있도록 하기 위해 싱글톤
패턴을 적용한다.

## 유의할 점  

1. 싱글톤 인스턴스가 너무 많은 일을 하거나 너무 많은 데이터를 공유하게 되면 각 클래스 간에 **결합도**가 높아져 ['개방-폐쇄 원칙'](https://ko.wikipedia.org/wiki/%EA%B0%9C%EB%B0%A9-%ED%8F%90%EC%87%84_%EC%9B%90%EC%B9%99)을 위배하게 된다.    
2. **멀티쓰레드 환경**에서는 동기화처리를 하지 않으면 여러 객체가 생성될 수 있고, 그에 따라 공유된 데이터 값이 달라지는 문제가
발생할 수 있다.  

안드로이드의 경우 싱글톤 클래스가 **액티비티의 Context**를 가지는 경우가 생기는데 이 경우 액티비티가 종료되어도 싱글톤 클래스가 
Context를 계속 가지고 있어 메모리 누수가 발생하게 된다.

## 예제

### 안드로이드 예제

{% highlight javascript linenos %}
public class DataManager {

  private static DataManager instance = null;
  private Activity activity;
   

  private DataManager(){
    //생성자앞에 private으로 선언하면서, 
    //다른 클래스에서 new 키워드를 사용하여 인스턴스를 만들 수 있는 여지를 막음.
  }

  public static DataManager getInstance(){
      if(instance == null){
          instance = new DataManager();
      }
      return instance;
  }

  public Activity getActivity() {
      return activity;
  }

  public void setActivity(Activity activity) {
      this.activity = activity;
  }
  
}
{% endhighlight %}

위와 같이 작성해 싱글톤 클래스가 가지게 된 activity를 onDestroy에서 null을 할당하는식으로 메모리 누수를 막을 수 있다.
또, 만약 액티비티 라이프사이클에 영향받지 않는 싱글톤 클래스를 만들고 싶다면 activity 대신 Application의 Context를 넘겨주면 된다.

### 멀티스레드에서 안전한 싱글톤 예제 

1.Lazy initialization

{% highlight javascript linenos %}
public class ThreadSafeLazyInitialization{
 
    private static ThreadSafeLazyInitialization instance;
 
    private ThreadSafeLazyInitialization(){}
     
    public static synchronized ThreadSafeLazyInitialization getInstance(){
        if(instance == null){
            instance = new ThreadSafeLazyInitialization();
        }
        return instance;
    }
    
}
{% endhighlight %}

private static으로 인스턴스 변수를 만들고 private 생성자로 외부에서의 생성을 막는다. 그리고 `synchronized` 키워드를 사용해서 thread-safe하게 만든다.
하지만 synchronized 특성상 비교적 큰 성능저하가 발생하므로 권장하지 않는 방법이다.

2.Lazy initialization + Double-checked locking

{% highlight javascript linenos %}
public class ThreadSafeLazyInitialization {
 
    private volatile static ThreadSafeLazyInitialization instance;
 
    private ThreadSafeLazyInitialization(){}
     
    public static ThreadSafeLazyInitialization getInstance(){
        
        if(instance == null){
            synchronized (ThreadSafeLazyInitialization.class) {
                if(instance == null)
                    instance = new ThreadSafeLazyInitialization();
            }
 
        }
        return instance;
    }
}
{% endhighlight %}

getInstance()에 synchronized를 사용하는 것이 아니라 첫 번째 if문으로 인스턴스의 존재여부를 체크하고 두 번째 if문에서 다시 한번 체크할 때 동기화 시켜서 인스턴스를 생성한다.  
따라서 thread-safe하면서도 처음 생성 이후에 synchonized 블럭을 타지 않아 성능저하가 완화된다.  

그러나 여전히 완벽한 방법은 아니다.

3.Initialization on demand holder idiom (holder에 의한 초기화)

클래스안에 클래스(Holder)를 두어 JVM의 Class loader 매커니즘과 Class가 로드되는 시점을 이용한 방법이다.

{% highlight javascript linenos %}
public class Something {

    private Something() {
    }
 
    private static class LazyHolder {
        public static final Something INSTANCE = new Something();
    }
 
    public static Something getInstance() {
        return LazyHolder.INSTANCE;
    }
}
{% endhighlight %}

개발자가 직접 동기화 문제에 대해 코드를 작성하고 문제를 회피하려 한다면 프로그램 구조가 복잡해지며, 비용 문제가 생길 수 있고, 특히 정확하지 못한 경우가 많다.  
그런데 이 방법은 JVM의 클래스 초기화 과정에서 보장되는 원자적 특성을 이용하여 싱글톤의 초기화 문제에 대한 책임을 JVM에 떠넘긴다.  
holder안에 선언된 instance가 static이기 때문에 클래스 로딩시점에 한번만 호출될 것이며 final을 사용해 다시 값이 할당되지 않도록 만든 방법이다. 

가장 많이 사용하고 일반적인 Singleton 클래스 사용 방법이다.

## 마치며

지금까지는 싱글톤 패턴이 정확히 어떤 것인지 잘 알지 못하고 그냥 써왔다. 회사 일로 공부하게 된 것이지만 이번 기회에 싱글톤 패턴에
대해 많은 공부를 할 수 있었고, 앞으로 더 정확하고 적절하게 싱글톤 패턴을 사용할 수 있을 것 같다.

{: .box-note}
**참고**  
https://limkydev.tistory.com/37  
https://fsd-jinss.tistory.com/140  
https://jeong-pro.tistory.com/86
