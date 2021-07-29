# 코딩 컨벤션

기본 정렬은 intellij 자동완성을 사용 한다.  `Window` `ctrl`+`alt`+`l`  `Mac`  `option`+`Command`+`l`

impor 정리를 잊지 않도록 한다.  `Window` `ctrl`+`alt`+`o` `/`  `Mac`  `option`+`Command`+`o`

기본은 [ribot](https://github.com/ribot/android-guidelines) [prnd](https://github.com/PRNDcompany/android-style-guide)의 가이드라인을 참고하여 작성.



## Java



### Naming

- 단축형은 절대 :x:

- **Class files** : UpperCamelCase

- **Values** : 명사형

- **Method** : 동사형

  `ex) isTure();`

- **Static 변수** : sVariableName 
  `ex) sMaxNumber`

- **Member 변수** : mVriableName 

  `ex) mTextFeild`

- **(Static) Final 변수** : ALL_UPPER_CASE

  `ex) EXTRA_SOMETHING`

  

### Class member ordering

1. Constants
2. Fields
3. Constructors
4. Override methods and callbacks (public or private)
5. Public methods
6. Private methods
7. Inner classes or interfaces



### Method Chain case

```java
Picasso.with(context)
	   .load("http://ribot.co.uk/images/sexyjoe.jpg")
	   .into(imageView);
```



### Long parameter case

```java
loadPicture(context,
       "http://ribot.co.uk/images/sexyjoe.jpg",
       mImageViewProfilePicture,
       clickListener,
       "Title of the picture");
```



### 제어문 블럭 설정

항상 블럭을 사용하도록 한다

```java
if( isTrue() ) {

   ...
}
```



### Key

| Prefix      | 설명               |
| ----------- | ------------------ |
| `EXTRA_`    | Intent             |
| `PREF_`     | SharedPreferences  |
| `ARGUMENT_` | Fragment Arguments |

#### Activity

- Activity Intent에 `EXTRA_`를 넣어주는 경우, 해당 Activity에 `startActivity()` 혹은 `getIntent()`를 구현하고 이를 사용한다.

```java
public static void startActivity(Context context, @DrawableRes int photoResourceId) {  
  Intent intent = new Intent(context, PhotoDetailActivity.class);  
  intent.putExtra(EXTRA_PHOTO_RESOURCE_ID, photoResourceId);  
  context.startActivity(intent);  
}
public static Intent getIntent(Context context, String brandId, String brandName) {  
  Intent intent = new Intent(context, SelectCarActivity.class);  
  intent.putExtra(EXTRA_BRAND_ID, brandId);  
  intent.putExtra(EXTRA_BRAND_NAME, brandName);  
  return intent;  
}
```

#### Fragment

- Fragment에 `ARGUMENT_`를 넣어주는 경우, 해당 Fragment에 `newInstance()`를 구현하고 이를 사용한다.
- Fragment 생성자의 Parameter로 넘기지 않는다. [Best Practice to Instantiate Fragments with Arguments in Android](https://gunhansancar.com/best-practice-to-instantiate-fragments-with-arguments-in-android/)

```java
public static UserFragment newInstance(User user) {
	UserFragment fragment = new UserFragment();
	Bundle args = new Bundle();
	args.putParcelable(ARGUMENT_USER, user);
	fragment.setArguments(args)
	return fragment;
}
```



### Line

- 한줄에 100자 이내로 지정한다
- 코드의 의미상 그룹지어 한줄로 구분한다
- 1줄이상 사용하지 않는다.
- 



### 새파일 생성시 주석

```ㅓㅁㅍㅁ
/**
 * Created by ted on 2018-07-12.
 * 사용 용도
 */
```

- 수정방법: `Preferences` -> `Editor` -> `File and Code Templates` -> `includes`탭 -> `File Header` 내용 삭제



### Util/Helper/Manager

- 특정기능을 수행하거나 상태를 관리하거나 분리되어 동작을 수행하는 클래스에 대한 사용처별 이름을 정의한다.



#### Util

- `public static void AAA`등으로 쓰이는 여러곳에서 사용되는 util성 기능을 보아둔 클래스
- `aa.bb.cc.util` 패키지에 모두 모아둔다.
- 예) `DateFormatUtil`, `PixelUtil`, `BitmapUtil`등



#### Helper

- 특정 패키지나 기능에서 한정되어 사용되는 `public static void AAA` 클래스
- 공통으로 쓰이지 않고 특정 기능의 코드를 분리하기 위한 용도로 사용한다.
- 예) `NotificationChannelHelper`등



#### Manager

- 항상 내부에서 instance로 만들어서 관리되는 용도
- 내부적으로 state 혹은 information을 가지고 있어서 호출한곳에서의 상태에 따라서 관리되는 값을 변경하고 반영하는 작업을 해준다.
- 예) `RegisterStepManager`, `RegisterCarInfoConfirmManager`등



### Exception

- 기본적으로 모든 Exception을 찾을 수 있도록 한다

  ```java
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

- \<WHERE>\_\<DESCRIPTION>_\<WHAT>

- 대부분의 margin/padding 은 아래 정의된 space_xxx로만 사용되도록 한다.

```xml
<dimen name="space_8dp">8dp</dimen>  
<dimen name="space_12dp">12dp</dimen>  
<dimen name="space_16dp">16dp</dimen>  
<dimen name="space_18dp">18dp</dimen>  
<dimen name="space_20dp">20dp</dimen>  
<dimen name="space_24dp">24dp</dimen>
```

- 그외에 특정 화면에서 위의 값을 따르지 않는경우, \<WHERE>\_\<DESCRIPTION>\_\<WHAT>의 규칙으로 만든다.

```xml
<dimen name="register_car_item_car_model_start_padding">40dp</dimen>  
<dimen name="register_car_item_grade_start_padding">56dp</dimen>  
<dimen name="register_car_item_car_detail_start_padding">72dp</dimen>
```

- 2번이상 쓰이는 경우에는 정의해주는 것을 강제하고 1번만 쓰는 경우에는 xml코드에 넣는 것을 허용한다.



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
- PR을 Merge 할 때는 리뷰어 1명 이상이 리뷰를 해줘야 한다.
- 본인 `PR`은 본인이 merge 한다.

```
## 개요
## 작업사항
## 변경로직
 
// 리팩토링
## 변경전
## 변경후
 
// 새로운 커스텀뷰
## 사용방법

```
