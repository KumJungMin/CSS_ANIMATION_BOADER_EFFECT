# hover시 밑줄이 생기는 menu

## 1. preview

### flex, before, after, hover, fontawesome, transition, position 사용

<img src="https://j.gifs.com/6XqzDO.gif" />


## 2. 코드 분석

### 1) html

#### (1) navigation 형태로 구성
- `ui`, `li` : `navigation`들이 일정한 간격을 유지하도록 ul을 사용

```html
    <ul class="gnb">
        <li><a>HOME</a></li>
        <li><a>ABOUT</a></li>
        <li><a>SERVICE</a></li>
        <li><a>PORTPOLIO</a></li>
        <li><a>CONTACT</a></li>
    </ul>

</body>

```

<br/><br/>

### 2) css

#### (1) 중앙 정렬하기
- `body`안의 내부 요소들을 중앙정렬한다.
            
```css
a{
    text-decoration: none;
    color: #222;
}

body{
    margin: 0;
    font-weight: 300;
    color: #222;
    background-color: #f4f4f4;

    /* body안의 내부 요소 중앙정렬 */
    display: flex;
    justify-content: center;  /*가로 중앙*/
    align-items: center;      /*세로중앙*/
    height: 100vh;            /*높이값 정해줘야->중앙정렬됨*/ 
}
```

<br/>

#### (2) li 디자인 설정 및 가로 정렬하기
- `li` 디자인 설정

  : `li`태그에서 default로 생기는 생기는 점을 아예 없앤다.
  
  : `li`태그에서 default로 적용되는 `padding`, `margin`을 없앤다.

<br/>

- `li`를 가로정렬하는 방법(1)

  : `float`를 `left`로 해서 왼쪽 정렬을 한다.
  
  : `gnb`의 전체넓이(600) / 5개의 메뉴 = 120이므로, `li`한개의 넓이를 120로 설정한다.

  : 그 다음 `li`의 `text-align`를 `center`로 설정한다.

```css
.gnb {
    list-style: none;   /*li시 자동으로 생기는 점을 아예 없앰*/
    padding: 0;         /*li시 자동으로 생기는 패딩을 없앰*/
    margin : 0;         /*li시 자동으로 생기는 마진을 없앰*/
    width: 600px;
    background-color: #fff;
    border-radius: 10px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);   /*그림자 추가*/
    padding: 50px 30px;
}
.gnb li{
/* li를 가로정렬하는 방법(1) 권장*/
    float : left;    /*요소를 왼쪽 정렬시킴*/
    width : 120px;   /* 600 / 5개의 메뉴 = 120 */
    text-align: center;
}



/* li를 가로정렬하는 방법(2) 
.gnb{
    display: flex;         li들이 가로배치됨
  }  
.gnb li{  
    flex : 1               1로 줌
    text-align: center;
 }
*/


```


<br/>

#### (3) li의 자식인 a태그의 가상클래스 구성하기

- 가상클래스 위치 고정

  : 부모(`gnb li a`)는 상대위치로 둔다.
  
  : `a`의 가상 자식 클래스인 `before`를 절대위치로 두어 가상클래스의 위치를 고정시킨다.
  
  : `a`의 가상 자식 클래스인 `before`에 `bottom`을 주어, 글자 밑에 위치시킨다.

<br/>

- 가상클래스 `before 애니메이션 적용

  : `hover`시 `before`의 `width`가 `0`에서 `100%`가 되면서 나타나게 한다.
   
   : 그렇게 하기 위해선, 가상클래스를 중앙에 배치시킨다.
   

 
```css
.gnb li a{
    font-size: 14px;
    position: relative;   /*부모는 상대위치*/
}

.gnb li a:before{
    content : '';
    position: absolute;  /*before를 절대위치*/
    background-color: dodgerblue;
    height: 2px;
    width : 0;
    bottom: -10px;       /*bottom을 주어, 글자 밑에 위치시킴*/       
    transition: 0.5s;    /*가상클래스에 이벤트 발생시 시간 지정*/
    
    
    left : 50%;         /*만약 왼쪽에서부터 커지게하려면-> left를 0으로 두면 됨*/
    transform: translateX(-50%);
}

.gnb li a:hover:before{ /*hover시 width:0 -> 100%가 됨*/
    width : 100%;
      
}
    
```

