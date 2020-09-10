# 2020-05-03

`` This version of Android Studio cannot open this project, please retry with Android Studio ~ or newer``
 
##### -> project build gradle에 가서 그래들 버젼을 고쳐준다
 
 
 
# 2020-05-04


`` lazy ``

##### -> lazy는 선언 해두고 실제 사용할때 초기화 하는 방법이다 


## Realm

##### Realm을 앱에서 등록(초기화)를 해 두면 어느 액티비티에서 사용하던간에 Realm 객체만 생성하면 공유가 된다.
      

##### [0]  Realm에서 사용할 모델을 먼저 만든다 만들고 난 뒤 RealmObject를 상속해야한다.
##### [1]  Realm.init으로 먼저 초기화를 해 준다. 
#####      (Application 클래스 하나 생성하고 그곳에 초기화 한 후, Manifest에 name을 Application Class 명을 적어넣는다.
##### [2]  Realm 오브젝트를 하나 만들어 주고 [ Realm.getDeaultInstance() ] 
#####      executeTransactionAsync (비동기) 문장 안에insert, update, 등을 사용한다.
  
   
```  
     realm.beginTransaction() // 트랜잭션 시작
     val managedDog = realm.copyToRealm(dog) // Persist unmanaged objects
     val person = realm.createObject<Person>(0) // Create managed objects directly
     person.dogs.add(managedDog)
     realm.commitTransaction()  // 커밋으로 적용, 트랜잭션 종료
```

##### executeTransaction는 시작과 커밋 종료를 자동으로 해준다.
##### 데이터 삽입 시 insert(모델객체)하면 끝이다




# 2020-05-05

`` 상속과 구현의 차이 (extends, implementaion) ``

 하나의 클래스를 인간이라고 봤을때
##### 인간은 동물이다 -> 상속 (근원)
##### 인간은 수리공이다 -> 구현 (역할) 


# 2020-05-09

``` Realm은 모델이 추가되거나 모델의 구조가 변경될 경우에 항상 [마이그레이션]이란 것을 해줘야 한다. ```

Realm을 Application 에서 초기화 해줄때 config를 미리 구현하고 
```
 Realm.init(applicationContext)
 val config = RealmConfiguration.Builder().deleteRealmIfMigrationNeeded().build()
 Realm.setDefaultConfiguration(config)     
```

이렇게 해주면 getDefaultInstance로 객체를 가져와도 config 에 설정해놓은 값대로 설정된다.



# 2020-05-11

``` 문자열.split(구분할문자). ```
 는 문자열을 구분할 문자별로 나눠서 배열형태로 반환해준다 참말로 좋은기능이다.
 
``` 리사이클러뷰 어댑터 매개변수로 넣는다고 무조건 매개변수 만큼의 뷰들이 생기는것이 아니다.``` 
리사이클러뷰를 움직이면 변수 position이 변경되는데 이 값에 따라서 onBind가 실행됐었다.
 
 
Realm에는 ArrayList 가 들어갈 수 없다.


# 2020-05-12


1. 생명주기에 ExoPlayer 등록
2. player 인스턴스 생성
3. PlayerView에 Player 인스턴스 등록 (setPlayer)
4. Uri를 이용해서 미디어 소스를 생성 
5. Player.prepare로 생성한 미디어 소스를 재생

### 프로그래머스 알고리즘 문제 (스택/큐) 탑 문제

```
class Solution {
    fun solution(heights: IntArray): IntArray {
        var answer = intArrayOf()
        var stack: List<Int> = listOf()
        for ((i, h) in heights.withIndex()) {
            stack = stack.dropLastWhile {t -> heights[t] <= h }
            answer +=  (stack.lastOrNull() ?: -1) + 1
            stack += i
        }
        return answer
    }
}
```
* for 안에 (i,h) index와 value 이다.
* dropLastWhile - > 마지막 element 부터 predicate 와 매칭된 결과를 제외하고 가져온다.
* stack.lastOrNull() 마지막 인자를 반환하며, 없을 경우에 Null 리턴

첩첩산중이다


# 2020-05-14

```android:configChanges```

액티비티가 처리하는 구성 변경을 나열합니다. 구성 변경이 런타임에 발생하는 경우 기본적으로 액티비티가 종료되었다가 

다시 시작하지만 이 특성을 사용하여 구성을 선언하면 액티비티가 다시 시작하는 것을 방지합니다. 

그 대신 액티비티는 여전히 실행 상태에 있고 onConfigurationChanged() 메서드가 호출됩니다.

->ExoPlayer 화면 전환시 자꾸 플레이어가 초기화 되는 현상을 이 방법으로 해결
하지만 안드로이드 공식 문서에서는 [최후의 수단]으로 사용하라고 당부하고 있음

 onSaveInstanceState(), ViewModel 등 의 기능을 이용해서 런타임 변경 처리를 할것을 권장한다.


# 2020-05-14

[ ?. ] Null Safety 연산자 -> 참조연산자를 실행하기 전에 객체가 null인지 확인부터 하고 Null이면 실행하지 않는다.

[ ?: ] elvis 연산자       -> 객체가 Null이 아니라면 그대로 사용하지만 Null 이라면 연산자 우측에 있는 객체로 대체된다.

[ !! ] Nonnull 연산자     -> 참조연산자 사용할때 null 여부를 확인하지 않도록 한다.


# 2020-05-21

ActionBar -> 뷰가 아님 액티비티 기본구성요소중 하나
ToolBar -> 뷰처럼 자유자재로 컨트롤 가능한 앱바

액션바를 만들때 많이 헷갈린 부분중 하나이다
xml파일에서 버튼을 넣어주고 하는줄 알았는데 그 방법이 아니였다.

```
setSupportActionBar(toolbar)
supportActionBar?.setDisplayHomeAsUpEnabled(true)
supportActionBar?.setHomeAsUpIndicator(R.drawable.ic_menu_black_24dp);
supportActionBar?.setDisplayShowTitleEnabled(false)
```

# 2020. 06. 15



- android : name 태그 (XML) 

  

  ```xml
  android:name="androidx.navigation.fragment.NavHostFragment"
  ```

 

  어플리케이션을 위해 구현된 어플리케이션 서브클래스의 이름. 

  어플리케이션 프로세스가 시작될 때, 어플리케이션의 다른 어떤 컴포넌트보다 먼저 객체화된다(실행된다). 서브클래스는 없어도 된다(대부분의 어플리케이션은 서브클래스를 사용하지 않는다). 서브클래스가 없으면, 안드로이드는 베이스 어플리케이션 클래스의 객체를 사용한다.

  
  
# 2020.07.06

### 	상태바 색상변경

- ```xml
  <item name="colorPrimaryDark">#ffffff</item>
  <item name="android:windowLightStatusBar">true</item>
  ```

  - colorPrimaryDark  : 작업표시줄(상태창)의 색상 변경해준다.
  - windowLightStatusBar : 상태창의 색깔이 바뀌어도 자동으로 아이콘의 색상을 변경해준다.





 ###     위치서비스 (GPS)

- 위치서비스 접근권한 부여 (checkSelfPermission, requestPermissions)
- 기기의 위치 서비스 활성화
  1. LocationManager (getSystemService 사용) 객체생성
  2. 만든 객체의 getLastKnownLocation으로 위치값을 받는다
- 받아온 위도와 경도를 토대로 GeoCoder의 getFromLocation을 이용해 현재 주소지를 받는다.
  - 이 때 Address 클래스 타입으로 반환된다.
  
  
  
  
# 2020. 07. 12

### Static (Companion Object)

- 코틀린에서 함수를 Static 해줄경우 @JvaStatic을 붙여주어야 한다.

```kotlin
 companion object {
        @BindingAdapter("imageSrc")
        @JvmStatic fun loadImageURL(view: ImageView, url: String){
            Glide.with(view.context).load(url).into(view)
        }

```

 

### BindingAdapter

- XML에서 속성명으로 데이터 바인딩을 하는 경우에 사용

```xml
<ImageView
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   imageSrc="@{userProfile.imageURL}"/>
            
```

```kotlin
 companion object {
        @BindingAdapter("imageSrc")
        @JvmStatic fun loadImageURL(view: ImageView, url: String){
            Glide.with(view.context).load(url).into(view)
        }
```

-> ImageIvew의 imageSrc라는 바인딩 속성을 만들고

-> 어댑터를 하나 생성해 Static  함수로 URL값을 어떻게 처리해줄지 구현해준다.




  # 2020. 07. 16

### - Exception from call site #4 bootstrap method

​	자바 버전을 올려주면 해결이 가능하다.

```
compileOptions {
targetCompatibility = "8"
sourceCompatibility = "8"
}
```

# 2020. 07. 29

#### [ERROR] CLEARTEXT communication to x.x.x not permitted by network security policy

application에 해당 문구를 작성해준다.

```
android:usesCleartextTraffic="true"
```

**-> API 27까지는 http 통신을 기본 허용했지만 API28부터는** 

​	**아래 문장을 추가해주거나 https 로 해야한다.**


# 2020-07-30

## BottomNav + NavGraph 사용시

```xml
	<item android:id="@+id/fragment_Dogdrip"
        android:title="Daily"
        android:icon="@drawable/cube" />

    <item android:id="@+id/dailyFragment2"
        android:title="Wrtie"
        android:checkable="true"/>

    <item android:id="@+id/myFragment"
        android:title="MY"
        android:icon="@drawable/cube"/>
```

***BottomNav Menu XML에서 item들의 id를 띄우고 싶은 프래그먼트 id와 같게 해준다***



# 2020. 07. 30

### 이미지 뷰 이미지 속성

```XML
<ImageButton
    android:id="@+id/btn_back"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:background="#00000000"
    android:src="@drawable/btn_back"
    android:scaleType="centerInside" //이 부분
 />
```

- MATRIX = 원본 크기 그대로 보여줌 (왼쪽상단 정렬) 
- CENTER = 원본 크기 그대로 보여줌 (가운데 정렬)
- CENTER_CROP = View 영역에 공백이 있으면 채워서 보여줌(비율유지)
- CENTER_INSIDE = View 영역을 벗어나면 맞춰서 보여줌(비율유지)
- FIT_START = View 영역에 맞게 보여줌 (왼쪽상단 정렬, 비율유지)
- FIT_CENTER = View 영역에 맞게 보여줌 (가운데 정렬, 비율유지)
- FIT_END = View 영역에 맞게 보여줌 (왼쪽하단 정렬, 비율유지)
- FIT_XY = View 영역을 가득 채워서 보여줌(비율유지 안함)


# 2020. 08. 12

## # Lifecycle

<img src="https://user-images.githubusercontent.com/53253298/90026384-305fc300-dcf2-11ea-9c7e-20f266037ae3.png" alt="Lifecycle" style="zoom: 33%;" />

 - 종류 

    - **onCreate**
       - 활동을 생성할때 가장먼저 실행된다.
       - 실행이 된 다음엔 Created 상태가 된다.
    - **onStart**
       - Created 상태에서 활동이 시작될때 실행된다. (액티비티가 실행될 때)
       - 실행이 된 다음엔 Started 상태가 된다.
    - **onResume**
       - 액티비티가 focus를 얻었을때 실행된다. (focus를 잃을때까진 Resumed 상태)
       - ex) 다이얼로그 화면에서 확인을 눌러서 다시 액티비티 화면으로 됐을때
       - 실행이 된 다음엔 Resumed 상태가 된다.
    - **onPause**
       - Resumed 상태에서 focus를 잃었을때 실행된다.
       - ex) 다이얼로그를 띄워서 다이얼로그 화면이 뜰때
    - **onStop**
       - 액티비티 화면에서 벗어나면 실행된다.
       - ex) 앱을 백그라운드에 숨겨놓을때 onStop이 실행됨
    - **onDestroy**
       - 액티비티가 소멸되기 전에 실행된다. (앱을 프로세스에서 종료)

   

## # LifecycleObserver

- 라이프사이클을 옵저버 패턴으로 관리를 하는것이다.
- 해당 옵저버 클래스는 항상 라이프사이클을 보고있다가 맞는주기에 알아서 실행되게끔 설정할 수 있다. 



#### 1.  옵저버를 달아줄 클래스에 LifecyycleObserver 상속

```kotlin
class DessertTimer(lifecycle: Lifecycle): LifecycleObserver
```



#### 2. addObserver로 해당 클래스 옵저버로 등록한다.

```kotlin
lifecycle.addObserver(this)
```



#### 3. Annotation으로 어떤 주기에 어떤행동을 할지 설정한다.

```kotlin
@OnLifecycleEvent(Lifecycle.Event.ON_START)
fun startTimer(){ ... }
```



#### 4. 액티비티에서는 해당클래스를 만들때 Lifecycle을 전달 해준다.

```kotlin
dessertTimer = DessertTimer(this.lifecycle)
```


# 2020. 08. 14

### 맥북을 처음으로 산 날 

- 단축키

  - cmd + / : 한줄 주석a

  - cmd + f12 : 파일 구조 보기

  - cmd + y : 정의된 부분 빠르게 보기

  - cmd + d : 선택 블록을 복사하거나 해당 라인을 복사해준다.

  - cmd + p : 해당 메소드의 사용을 위해 필요한 파라미터를 표시해줌.

  - option + cmd + / : 블록 주석

  - option cmd + L : 라인정리

  - ctrl + O : Override methods

  - ctrl + I : Implement methods

  - ctrl + space : 기본 단어 자동 완성 ( 맥의 단축키랑 중복되어서 변경함 )

  - shift + F6 : 이름 변경하기 ( 변수명 등 )

  - shift + cmd + 위 또는 아래 : 해당 메서드 안에서의 라인 이동

  - ctrl + shift + space : 타입 캐스팅( ex) Button button = (까지 입력하고 누르면 (Button)생성해줌)

  - f3 : 북마크 (숫자나 문자로 북마크 = alt + f3, ctrl + 숫자 or 문자로 이동)
  
  
  
# 2020. 08. 23

### ViewModel 캡슐화

- UI에서 라이브데이터가 변경되는것을 방지하고자 캡슐화를 한다.

```kotlin
private val _score = MutableLiveData<Int>() // 뷰모델 내부에서 사용
    val score: LiveData<Int>				// 외부에서 사용 (변경불가)
        get() { return _score }
```

변경이 불가능한 LiveData인 score는 외부에서 참조용으로만 사용한다.

직접적인 값 변경은 ViewModel 내부에서 _score변수로 처리한다.



### ViewModelFactory

- ViewModel을 생성할 시 생성자가 필요한경우(파라미터)에  ViewModelFactory를 만들어준다.

```kotlin
class ScoreViewModelFactory(private val finalScore: Int) : ViewModelProvider.Factory {
    override fun <T : ViewModel?> create(modelClass: Class<T>): T {
        if (modelClass.isAssignableFrom(ScoreViewModel::class.java)) {
            return ScoreViewModel(finalScore) as T
        }
        throw IllegalArgumentException("Unknown ViewModel class")
    }
}
```

Factory에서 미리 정의를 해둔 후 ViewModel을 생성할때는 

```kotlin
viewModelFactory = ScoreViewModelFactory(scoreFragmentArgs.score)
viewModel = ViewModelProviders.of(this, viewModelFactory)
                .get(ScoreViewModel::class.java)
```

Factory객체를 만들고 ViewModelProviders의 of메소드에 객체를 추가해 준다.



### Transformations.map

- 라이브데이타를 다른형태의 라이브 데이터로 바꿔준다

```kotlin
val userLiveData: MutableLiveData<User> = repository.getUser(id)
val userNameLiveData: LiveData<String> = Transformations.map(userLiveData) { user ->
    user.firstName + " " + user.lastName
}
```

userLiveData가 바뀔때마다 userNameLiveData 도 같이 바뀌게 된다.


# 2020. 08. 24

## # Coroutine (코루틴)

- ### Scope 

  ```
  코루틴이 실행되는 범위로, 
  Globalscope는 앱 전체의 생명 주기를 따른다. 즉, 앱이 실행중이라면 코루틴이 계속 실행될 수 있다. 
  만약 Activity와 라이프사이클을 같이 하는 scope를 만든다면 activity가 종료되기 전까지만 실행되고, 액티비티가 종료되면 해당 스코프를 사용한 코루틴도 같이 종료된다.
  ```

- ### Launch 

  ```
  비동기적으로 실행될 코드 블럭을 받아서 코루틴을 실행시키는 함수
  ```

- ### Suspend function 

  ```
  코루틴 블럭을 임시로 빠져나가는 함수. 코루틴 블럭 안에서만 호출할 수 있으며, 
  이 함수를 만나면 코루틴 블럭을 잠시 빠져나가고, 이 함수는 그대로 비동기적으로 수행된다.
  그 후, 해당 함수의 작업이 완료되면 다시 코루틴 블럭으로 돌아와서 해당 함수의 다음부터 이어서 실행된다.
  해당 함수의 작업이 완료되기 전까지는 코루틴 블럭 안에서 다음으로 넘어가지 않는다.
  ```

- ### Job 

  ```
  객체는 코루틴 동작을 제어하기 위한 객체
  ```

  # 2020. 08. 27

### DiffUtil (RecyclerView)

- RecyclerView Support Library의 유틸리티 클래스이다

  목록(Item)간의 차이점을 찾고 업데이트 되어야할 목록을 반환해 준다.



### ViewModel 그리고 AndroidViewModel

```
액티비티가 재생성 될 때, ViewModel은 액티비티 수명주기 외부에 존재하기 때문에
UI 컨텍스트를 ViewModel에 저장한다면 메모리 릭을 발생시키는 직접적인 원인이 될 수 있다.
다만 Application 컨택스트를 저장하는 것은 문제가 되지 않습니다. 
Application 컨택스트는 전체 앱의 수명주기를 의미하기 때문에 
메모리 릭에 영향을 주지 않으며 이런 용도를 위해 AndroidViewModel 클래스를 제공한다.
```

즉  그냥 ViewModel 는 Fragment나 Activity에 의존적인 뷰모델 객체이고

AndroidViewModel은 Application의 Scope 를 따른다. 그래서 특정 액티비티나 프래그먼트가 Destroy 되더라도 어플리케이션이 종료되지 않는 이상 인스턴스가 유지된다.

// 출처 https://readystory.tistory.com/176


# 2020.08.30

- ### getKnownLastLocation() 오류

  공기계에서는 null값 AVD에서는 잘 받아오는 현상이 있어서 한창을 뒤지다가 찾아냈다

  ```kotlin
  locationManager.getLastKnownLocation(LocationManager.GPS_PROVIDER)
  ```

  1. GPS가 작동하지 않고, WI-FI/Cell Tower(기지국)으로부터 위치정보를 얻지 못할 때
  2. 가장 최근에 읽은 위치정보가 없을 때

  ```kotlin
  location = if(  locationManager?.getLastKnownLocation(LocationManager.GPS_PROVIDER) != 				null)
              locationManager?.getLastKnownLocation(LocationManager.GPS_PROVIDER)
          else
              locationManager?.getLastKnownLocation(LocationManager.NETWORK_PROVIDER)
  ```

   이 방법으로 GPS_PROVIDER로 값을 가져오지 못할때는 NETWORK_PROVIDER를 사용하는것으로 수정


# 2020.09.08

### Navigation

1. 네비게이션을 gradle에 추가해준다.

2. res에 navigation 메뉴를 추가하고 navGraph를 만들어준다.

3. navigationGraph를 표현할 fragment에 아래와 같이 설정

   ```xml
   <fragment
   android:id="@+id/myNavHostFragment"
   android:name="androidx.navigation.fragment.NavHostFragment"
   app:defaultNavHost="true"
   app:navGraph="@navigation/navigation" />
   ```

4.  추가하면 해당 프래그먼트에는 네비게이션 그래프 그대로 화면에 표시가 된다.

5. navGraph에 프래그먼트간을 이으면 action이 생기게 되는데 fragmentA to fragmentB 이런식으로

6. 이 액션들을 아래와같이 실행시키면 프래그먼트간 이동이 가능하다.

   ```kotlin
   view.findNavController().navigate(R.id.action_gameWonFragment_to_gameFragment)
   ```



### Navigation BackStack

 1. 네비게이션의 액션을 선택(간선을 선택한다.)

 2. Pop Behavior에 보면 popUpTo와 popUpToInclusive 가 있는데

    popUpTo는 어떤프래그먼트 위에 스택이 쌓일지를 뜻한다.

	3. popUpToInclusive는 팝업이 되면 자기 자신은 스택에서 사라지게 할건지를 선택



### Navigation with ActionBar

- 네비게이션에 따라서 액션바의 버튼이 바뀌게 되는 기능

  ```kotlin
   val navController = this.findNavController(R.id.myNavHostFragment)
  NavigationUI.setupActionBarWithNavController(this, navController)
  ```

  백스택이 있는지 없는지를 판별

  ```kotlin
  override fun onSupportNavigateUp(): Boolean {
          val navController = this.findNavController(R.id.myNavHostFragment)
          return navController.navigateUp()
      }
  ```
  
  
  
  ### NavigationView & Drawer

- 네비게이션뷰를 메뉴 버튼을 클릭했을때 출력하게끔 한다.

  1. 레이아웃부분은 DrawerLayout으로 감싸준다.

  2. 감싼 레이아웃부분 안에서 평상시 표시될부분과 메뉴를 클릭했을때 나타날 NavigationView로 나눠준다.

  3. 드로어 레이아웃을 생성해주고 navigation controller를 만들어 연동되게끔 한다.

     ```kotlin
     drawerLayout = binding.drawerLayout
     val navController = this.findNavController(R.id.myNavHostFragment)
     NavigationUI.setupActionBarWithNavController(this, navController, drawerLayout)
     ```

  4. 앱 바 설정부분에 네비게이션 그래프와 드로어 레이아웃을 넣어준다.

     ```kotlin
     appBarConfiguration = AppBarConfiguration(navController.graph, drawerLayout)
     NavigationUI.setupWithNavController(binding.navView, navController)
     ```

  5. 뒤로 돌아가야 하는 부분이 있는지를 보고 없으면 메뉴를 출력

     ```kotlin
     override fun onSupportNavigateUp(): Boolean {
        val navController = this.findNavController(R.id.myNavHostFragment)
        return NavigationUI.navigateUp(drawerLayout, navController)
     }
     ```

  6. NavigationView의 XML속성에는 반드시 아래와 같은 속성이 있어야 한다

     ```xml
     android:layout_gravity="start"
     ```

     이건 네비게이션뷰가 어떤 방향으로 나오는지를 설정하기 위함이다.

  7. NavigationView를 사용할때는 다른 프레그먼트에서는 끌었을때 나오지 않게 처리해야한다.

     ```kotlin
     navController.addOnDestinationChangedListener { nc: NavController, nd: NavDestination, bundle: Bundle? ->
                 if (nd.id == nc.graph.startDestination) {
                     drawerLayout.setDrawerLockMode(DrawerLayout.LOCK_MODE_UNLOCKED)
                 } else {
                     drawerLayout.setDrawerLockMode(DrawerLayout.LOCK_MODE_LOCKED_CLOSED)
                 }
             }
     ```

     

  # 2020.09.10

### colorControlHighlgiht

- 스타일에서 색깔을 설정하고 해당 버튼의 배경에 설정하면 클릭 시 효과가 나타남

  ```xml
  // 스타일 부분에서 색상을 설정해준다.
  <item name="colorControlHighlight">@color/colorLightYellow</item>
  ```

  ```xml
  // 효과를 주고자 할 뷰에 가서 속성을 아래와 같이 지정한다.
  android:background="?attr/selectableItemBackground"
  ```

  



