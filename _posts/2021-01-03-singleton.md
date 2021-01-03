---
layout: post
title: 싱글톤 패턴(Sigleton Pattern)
subtitle: 안드로이드 싱글톤 패턴에 대하여
tags: [개발, JAVA, Android]
---

이번에 다니는 회사에서 싱글톤 패턴(Sigleton Pattern) 사용에 대한 회의를 하게 되었습니다. 회의 준비를
위해 미리 싱글톤 패턴에 대해 공부할 필요가 있었고, 공부한 내용을 정리하여 블로그에 작성하려고 합니다.

## 싱글톤 패턴(Singleton Pattern)이란?

싱글톤 패턴(Singleton Pattern)이란 애플리케이션이 실행될 때 어떤 클래스가 최초 한번만 메모리를 할당(**static**)하고,
그 메모리에 인스턴스를 만들어 사용하는 패턴입니다. 한번 생성한 인스턴스를 계속해서 재사용하는 패턴으로 자바의 경우 생성자를
private으로 선언하고, getInstance() 메서드로 객체를 반환하는 식으로 만듭니다.  

안드로이드의 경우 SharedPreferences 사용 클래스, Application 클래스 등에 사용합니다.

## 사용하는 이유

우선 인스턴스를 매번 새로 생성하지 않아 메모리 낭비를 방지할 수 있습니다. 그리고 전역으로 만들어진 인스턴스이기 때문에 모든
애플리케이션 영역에서 같은 데이터를 공유할 수 있습니다. 또, 싱글톤 클래스를 한번 만들고 나면 재사용하기 때문에 첫 생성 이후에는
성능이 좋아진다는 장점도 있습니다.  

안드로이드의 경우 액티비티나 클래스 사이에 클래스 전달이 번거롭기 때문에 클래스를 어디서든 사용할 수 있도록 하기 위해 싱글톤
패턴을 적용합니다.

## 유의할 점

싱글톤 인스턴스가 너무 많은 일을 하거나 너무 많은 데이터를 공유하게 되면 각 클래스 간에 결합도가 높아져 '개방-폐쇄 원칙'을
위배하게 됩니다.  
개방-폐쇄 원칙이란 
>"소프트웨어 개체(클래스, 모듈, 함수 등등)는 확장에 대해 열려 있어야 하고, 수정에 대해서는 닫혀 있어야 한다"

는 객체 지향 설계의 원칙입니다.  
또, 멀티쓰레드 환경에서는 동기화처리를 하지 않으면 여러 객체가 생성될 수 있고, 그에 따라 공유된 데이터 값이 달라지는 문제가
발생할 수 있습니다.  

안드로이드의 경우 싱글톤 클래스가 액티비티의 Context를 가지는 경우가 생기는데 이 경우 액티비티가 종료되어도 싱글톤 클래스가 
Context를 계속 가지고 있어 메모리 누수가 발생하게 됩니다.

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

위와 같이 작성해 싱글톤 클래스가 가지게 된 activity를 onDestroy에서 null을 할당하는식으로 메모리 누수를 막을 수 있습니다.
또, 만약 액티비티 라이프사이클에 영향받지 않는 싱글톤 클래스를 만들고 싶다면 activity 대신 Application의 Context를 넘겨주면 됩니다.

### 멀티스레드에서 안전한 싱글톤 예제 
