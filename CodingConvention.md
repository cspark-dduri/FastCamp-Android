# 코딩 컨벤션 

- 기본 정렬은 intelliJ 자동완성을 사용한다.  

   Window : `Ctrl` + `Alt` + `L`
   
   Mac : `Option`+`Command`+`L`

- impor 정리를 잊지 않도록 한다.  
   
   Window : `Ctrl` + `Alt` + `O` 
   
   Mac : `Option`+`Command`+`O`




## Kotlin



### Naming


- **클래스 이름** : [PascalCase](https://zetawiki.com/wiki/%EC%B9%B4%EB%A9%9C%ED%91%9C%EA%B8%B0%EB%B2%95_camelCase,_%ED%8C%8C%EC%8A%A4%EC%B9%BC%ED%91%9C%EA%B8%B0%EB%B2%95_PascalCase) 따르며, 구성 요소 이름으로 끝나야 합니다.
  
  `ex) SignInActivity, SignInFragment, ImageUploaderService, ChangePasswordDialo`
  
- **함수 이름** : [camelCase](https://en.wikipedia.org/wiki/Camel_case) 따르며, 동사 또는 동사구를 사용합니다. 

  `ex) sendMessage 또는 stop`

- **상수 이름** : [UPPER_SNAKE_CASE(모두 대문자)](https://en.wikipedia.org/wiki/Snake_case)를 사용하며, 밑줄로 단어를 구분합니다.
  
  ```
  상수란? 맞춤 get 함수가 없는 val 속성이며 콘텐츠를 세부적으로 변경할 수 없고 함수에 감지할 수 있는 부작용이 없습니다. 
  여기에는 변경할 수 없는 유형과 이 유형의 변경할 수 없는 컬렉션뿐만 아니라 스칼라와 문자열도 포함됩니다(const로 표시된 경우).
  인스턴스의 관찰 가능한 상태가 변경될 수 있는 경우 인스턴스는 상수가 아닙니다. 
  ```

  ``` ex)
  const val NUMBER = 5
  val NAMES = listOf("Alice", "Bob")
  val COMMA_JOINER = Joiner.on(',') // Joiner is immutable
  val EMPTY_ARRAY = arrayOf()
  EXTRA_SOMETHING
  ```
  
- **Member 변수** : mVriableName 

  `ex) mSetUser`

- **Local 변수** : lvVriableName

  `ex) lvPhoneNumber`

- **Member 변수 중 Observe** : mRxVriableName 

  `ex) private val mRxReqLogin: PublishSubject<ReqLogIn> = PublishSubject.create()`

- **Local 변수 중 Observe** : rxVriableName

  `ex) var rxClickLeave: PublishSubject<Boolean> = PublishSubject.create()`

### Class member ordering

1. Constants
2. Fields
3. Constructors
4. Override methods and callbacks (public or private)
5. Public methods
6. Private methods
7. Inner classes or interfaces



### Method Chain case

```
Picasso.with(context)
	   .load("http://ribot.co.uk/images/sexyjoe.jpg")
	   .into(imageView)
```



### Long parameter case

```
loadPicture(context,
       "http://ribot.co.uk/images/sexyjoe.jpg",
       mImageViewProfilePicture,
       clickListener,
       "Title of the picture")
```



### 블록

`else if/else` 분기가 없고 한 줄에 들어가는 `when` 분기 및 `if` 문 본문에는 중괄호가 필요하지 않습니다.

```
if (string.isEmpty()) return

when (value) {
    0 -> return
    // …
}
```
그 외 모두 블록을 사용 합니다. 

### 빈 블록

빈 블록 또는 블록 형식 구문은 K&R 스타일이어야 합니다

```
try {
    doSomething()
} catch (e: Exception) {} // WRONG!
```
```
try {
    doSomething()
} catch (e: Exception) {
} // Okay
```



### Key

| Prefix      | 설명               |
| ----------- | ------------------ |
| `EXTRA_`    | Intent             |
| `PREF_`     | SharedPreferences  |
| `ARGUMENT_` | Fragment Arguments |

#### Activity

- Activity Intent에 `EXTRA_`를 넣어주는 경우, 해당 Activity에 `startActivity()` 혹은 `getIntent()`를 구현하고 이를 사용한다.

```
  companion object{
    private const val EXTRA_ISMAIN = "EXTRA_ISMAIN"
    
    fun startActivity(act: Activity, isMain: Boolean) {
	val intent = Intent(act, SecondActivity::class.java)
	intent.putExtra(EXTRA_ISMAIN, isMain)
	act.startActivity(intent)
     }
   }
   
   정상적인 코드인지 
```

#### Fragment

- Fragment에 `ARGUMENT_`를 넣어주는 경우, 해당 Fragment에 `newInstance()`를 구현하고 이를 사용한다.
- Fragment 생성자의 Parameter로 넘기지 않는다. [Best Practice to Instantiate Fragments with Arguments in Android](https://gunhansancar.com/best-practice-to-instantiate-fragments-with-arguments-in-android/)

```
예제 코드 확인 중
```


### Line

- 한줄에 100자 이내로 지정한다
- 코드의 의미상 그룹지어 한줄로 구분한다
- 1줄이상 사용하지 않는다.
- 



### 새파일 생성시 주석

```
/**
 * Created by cspark on 2021-07-29.
 * 사용 용도 작성 (간략히라도 반드시 작성)
 **/
```

- 수정방법: `Preferences` -> `Editor` -> `File and Code Templates` -> `includes`탭 -> `File Header` 내용 삭제


### Exception

- 기본적으로 모든 Exception을 찾을 수 있도록 한다

  ```
  catch( Exception | newException .. | LastException e) {
  	// errorHandling
  } catch ( SpecialExcpetion se) {
  	// errorHandling2
  }
  
  ```





## Resource files

### Ordering

- 리소스들이 사용되는 장소에 따라 모아둔다.

- 여러장소에 사용되는 것은 제일위에 위치한다

  ```xml
  <!-- all -->
  ...
  ...
  
  <!-- main activity -->
  ...
  ...
  
  <!-- main fragment -->
  ...
  ...
  ```

  



### Naming

![img](https://lh3.googleusercontent.com/mKED7f-09GA0qoDzq2-44Wsx_KKS4xLRZ4xG_FG_aGHvUQyEAk-cCfjwx2YX_aCoQP36k0tH1RN9b_apmYxuCCGQzF-DWyiFjHlUml2YxhglulWNXlhG7_ke5cfu21ZlLqVqnBm2)



### Layout

#### WHAT

| Prefix      | 설명                                                         |
| ----------- | ------------------------------------------------------------ |
| `activity_` | Activity에서 쓰이는 layout                                   |
| `fragment_` | Fragment에서 쓰이는 layout                                   |
| `dialog_`   | Dialog에서 쓰이는 layout                                     |
| `view_`     | CustomView에서 쓰이는 layout                                 |
| `item_`     | RecyclerView, GridView, ListView등에서 ViewHolder에 쓰이는 layout |
| `layout_`   | `<include/>`로 재사용되는 공통의 layout                      |



### ID

- \<what>_\<description>

- 기본은 Android의 view의 CamelCase를 단축한 형태를 사용한다. 

  `ex) TextView -> tv`

- 커스텀은 snake case를 사용한다. 

  `MyCustomView -> my_custom_view`

- 만약 View의 이름이 Space, Switch와 같이 1개의 대문자만 존재한다면 모두 소문자인 아이디로 정한다. 

  ` Space -> space`

  

#### WHAT

- layout과 같은 단축형을 사용한다.

| View             | Prefix           |
| ---------------- | ---------------- |
| TextView         | `tv_`            |
| ImageView        | `iv_`            |
| CheckBox         | `cb_`            |
| RecyclerView     | `rv_`            |
| EditText         | `et_`            |
| ProgressBar      | `pb_`            |
| FrameLayout      | `fl_`            |
| NestedScrollView | `nsv_`           |
| Space            | `space_`         |
| Switch           | `switch`         |
| AbcDeFgh         | `adf_`           |
| Abcdef           | `abcdef_`        |
| MyCustomView     | `my_custom_view` |
| YourView         | your_view        |



### Drawable

- \<WHAT>(\_\<WHERE>)\_<DESCRIPTION(\_\<SIZE>)

- 이미지가 여러군데 활용된다면 WHERE 생략가능
- 이미지 크기가 1개밖에 없을 경우 SIZE 생략 가능



#### WHAT

-  Layout과 같은 단축형을 사용한다

| Prefix | 설명                                                   |
| ------ | ------------------------------------------------------ |
| `btn_` | 버튼으로 쓰이는 이미지                                 |
| `ic_`  | 버튼이 아닌 화면에 보여지는 이미지                     |
| `bg_`  | 버튼이 아닌 화면에 보여지는 이미지                     |
| `img_` | 실제사진이거나 아이콘형태가 아닌 일러스트형태의 이미지 |
| `div_` | divider로 활용되는 이미지                              |



### Selector

- 배경이나 버튼에서 View의 상태에 따라 drawable이 변해야 하는 경우에 대한 이름은 아래와 같다.

  | 상태     | Suffix      |
  | -------- | ----------- |
  | Normal   | `_normal`   |
  | Pressed  | `_pressed`  |
  | Focused  | `_focused`  |
  | Disabled | `_disabled` |
  | Selected | `_selected` |



### Background

- 배경색이 pressed상태에 따라서 white -> sky_blue로 변하는 경우는 bg_white_to_sky_blue.xml로 한다.
- 배경이 white색의 24dp로 테두리를 그리는 경우는 bg_white_radius_24dp.xml로 한다.
- 배경이 투명하며 배경의 선만을 sky_blue색의 8dp로 테두리를 그리는 경우는 bg_stroke_sky_blue_radius_8dp.xml로 한다.



### Dimension

- Default screen margins, per the Android Design guidelines

```xml
  <dimen name="activity_horizontal_margin">16dp</dimen>
  <dimen name="activity_vertical_margin">16dp</dimen>
```

- \<WHERE>\_\<DESCRIPTION>_\<WHAT>

- 기본 margin/padding 은 아래 정의된 space_xxx로만 사용되도록 한다. (Android Design guidelines 4dp 단위 사용)

```xml
<dimen name="space_8dp">8dp</dimen>  
<dimen name="space_12dp">12dp</dimen>  
<dimen name="space_16dp">16dp</dimen>  
<dimen name="space_18dp">18dp</dimen>  
<dimen name="space_20dp">20dp</dimen>  
<dimen name="space_24dp">24dp</dimen>
```

- 그 외 특정 화면에서 위의 값을 따르지 않는경우, \<WHERE>\_\<DESCRIPTION>\_\<WHAT>의 규칙을 만든다.

```xml
<dimen name="main_car_item_padding">40dp</dimen>  
<dimen name="payment_on_item_pagemargin">56dp</dimen>  
```


### String

- \<WHERE>\_\<DESCRIPTION>
- 공통으로 사용한 String 의 경우엔 all\_\<DESCRIPTION>


### Color

- \<WHERE>\_\<COLOR>
- 공통으로 사용한 Color 의 경우엔 all\_\<COLOR>


## Git

### Feature branch

`feature_#000_login`



### commit

- \<#이슈번호>\_\<What>_설명

  `#012_feat_로그인`

 

#### What

- feat: 기능구현
- add: 파일추가
- style: 리소스 수정
- doc: 문서 수정
- fix: 오류수정
- review: 리뷰후 수정



### Github

- 라벨을 꼭 활용한다.
- 리뷰어를 꼭 지정한다
- 풀리퀘스트를 요청하기전에 충돌을 해결한다.
- 풀리퀘스트에는 이슈와 연결시킨다.
  - `resolve #issue num`
  - 리뷰에 답할때는 커밋 코드를 연결시킨다.
- merge와 rebase를 개인판단에 따라 혼용한다.




