### gird basic

flex와 마찬가지로
father 컨테이너에 display : grid; 설정 후 시작한다.

grid-template-cloumns는 기본적으로 수평을 의미하고 각각 칸마다의 넓이를 설정해줌으로써 칸을 생성할 수있다.

grid-template-rows는 기본적으로 수직을 의미하고 각각 칸마다의 넓이를 설정해줌으로써 칸을 생성 할 수있다. 또한 grid-template-rows 설정이 안되어있을 경우 자식의 폰트 사이즈가 수직의 크기를 결정한다.

gap/coumn-gap/row-gap 은 칸마다의 틈새 크기를 결정하는 키워드

### grid-template areas

repeat 키워드를 이용하여 grid-template areas를 사용할 수있다. 
직접 칸에 클래스 이름을 배치하여 위치를 지정한다.  
위치 지정은 부모 컨테이너안에 명시.
grid-templeat-clomns: repeat(반복수, 크기설정);
grid-templeat-rows: repeat(반복수, 크기설정);
추가// grid-templeat-clomns: auto 200px;
auto를 이용하면 모든 칸수를 자동으로 전부 사용한다.
```
grid-template-areas:
        "header header header header" row의 크기설정
        "content content content nav" 2fr
        "content content content nav" 1fr
        "footer footer footer footer" 1fr/ 각 칸마다의 넓이 설정
				(repeat은 작동안함)
```
자식 클래스에서 area이름을 설정해줘야하며, 클래스이름과 area이름은 같을 필요가 없다. 다만 area이름과 grid-template-areas 에서 설정한 위치명은 같아야한다.

### grid-clomns-start & grid-clomns-end

자식에게 명시해주는 배치방법이다.
반드시 start와 end가 있어야한다.

독특한 점은 칸의 수로 설정하는 것이 아닌 선의 수로 설정한다. 이를테면 정사각형의 칸에 네개의 선이 존재한다. clomns는 가로방향에 존재하는 선, rows는 수직방향에 존재하는 선의 수를 세어서 설정하는 것이다.

```
ex) grid-clomns-start : 1; //1번 선에서 부터
     grid-clomns-end : 3; // 3번 선까지 가진다. 
고로 두칸의 상자를 가지는 것.
```

(sortcuts)
grid-column: 1 / 3;
또는
grid-column: 1 / -1;
-1이 의미하는 바를 알려면 선의 수를 세는 법에 대해 알아야한다. 보통은 오른쪽으로 1 2 3 순으로 세지만 - 가 붙으면 마지막선에서 반대방향으로 수를 센다고 생각하자. 마지막 지점인 -1 마지막에서 두번째 선 -2 
고로 전체를 쓰고 싶다면 1/-1로 설정할 수 있다.

또는 span 키워드 사용
```
grid-column: span 4;
```
span 은 직접 칸의 수를 세서 지정하는 방식이다. 칸의 수가 4칸이라면 span 4; 즉 전부를 쓰겠다는 의미.


### fr 
크기 단위의 하나이다. 1 fraction 은 1칸의 사용가능한 공간이다. grid공간의 비율을 이용하는것이기 때문에 환경에 따라 유연하게 변화가 가능하다.
vh 
크기 단위의 하나이다. 화면의 크기를 정한다.
ex) height : 50vh;  


### place items

부모컨테이너에 명시
align-items & justify-items 키워드를 사용하면 셀안에 stretch하지않고 존재하게 된다. 디폴트 값은 stretch
```
ex) align-items : start; 
```
 칸의 첫번째 즉 왼쪽에 위치

shortcut 으로는 아래와 같이 사용 가능.
```
 place-items: stratch center;
  ``` 
 수직으로 늘어나고 수평으로는 가운데를 의미한다.

### place content

부모컨테이너에 명시
items는 grid안의 각각을 의미하지만 content는 grid전체를 의미한다. background를 기준으로 그리드 전체를 이동시키는 것. 디폴트값은 start이다.
```
ex) justify-content: center;
```
shortcut 
```
ex) place-content: end center;
```
수직으로 end 수평으로 center를 의미한다.

### place self

자식컨테이너에 명시 왜냐하면 셀안의 자식이 움직이기 때문이다.
```
ex) place-self : end center;
```
셀안에 수직으로 end 수평으로 center로 이동을 의미한다.
당연하게도 justify 나 align으로 각각 명시도 가능하다.

### grid-auto
부모컨테이너에 명시
grid-auto-flow는 column과 row을 가지고있다. grid를 수평방향(cloumn)이나 수직방향(row)으로 바꿀 수 있는 키워드이다.

grid-auto-columns는 방대한 양의 데이터를 알아서 설정해주는 키워드이다. 
```
ex) 
grid-template-columns: repeat(4,100px);
grid-auto-columns : 100px;
```
기존 100px 크기를 가진 4개의 칸이 데이터로 가득 차게되면 남은 데이터들을 위한 칸을 100px 크기로 자동 생성해준다.

### minmax

화면이 줄어듬에 따라 더이상 줄어들지 않았으면 하는 순간이 있다. 
또는 화면이 늘어남에 따라 더이상 커지지 않았으면 하는 순간도 있다. 그럴 때 minmax를 사용해보자.

```
ex)grid-template-columns: repeat(5, minmax(100px, 150px));
```
평소와 같이 그리드 템플릿을 정해준 후 사이즈 지정란에 minmax를 설정해주는 것으로 쉽게 사용할 수 있다.

### auto-fill, auto-fit

```
Grid-template-columns: repeat(auto-fill, minmax(100px,1fr));
```
//창 너비가 늘어나면 빈 column들로 row를 채워준다.(fill)

```
Grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
```
// 창 너비가 늘어나면 element를 늘려서 row에 맞게 해준다.(fit)

### min-content max-content

Div 내부 컨텐츠에 따라서 셀의 크기를 조절하는 것.
```
 Grid-template-columns: max-content min-content;
```
//1열은 컨텐츠를 
나타내는 최대 사이즈로, 2열은 최소 사이즈로 열의 너비를 조정
Minmax와 결합가능
```
 Grid-template-columns: repeat(auto-fit, minmax(20px,max-content));
```
Max-content를 최소값으로 두면, 컨텐츠를 다 싸고 있는 영역으로 최소값이 설정
Min-content를 최소값으로 두면, 창이 줄었을 때, 컨텐츠가 들어갈 수 있는 최소한의 영역만 보존된다.