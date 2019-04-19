# 정규표현식
정규표현식의 메시가 되어보자.

참고 : [ZVON.org](http://zvon.org/comp/r/tut-Regexp.html#Pages~Contents)

간단한 테스트 : [regexr.com](https://regexr.com/)
### patterns of Regular expression

#### ^, $
- ^: 시작
  - ^who : who로 시작하는 것들
  
- $: 끝
  - end$ : end로 끝나는 것들

#### . (point)
- Any character
- . : 1개 문자로 끝나는 것
- ...... : 5개 문자로 구성된 것 (5개 덩어리 단위로 선택 됨)
- \\.\. : O<code>.K.</code>

#### [ ] (square bracket)
- a list of characters
- [oyu] : H<code>o</code>w d<code>o</code> <code>you</code> d<code>o</code>?
- [owy][yow] : H<code>ow</code> do <code>yo</code>u do?
- [abcdefghijklmnopqrstuvwxyz] = [a-z]
- [ABC12345abcde] = [A-C1-5a-e]

#### [^ ] (carrot in sqaure bracket)
- means **NOT**
- [^A-Y] : ABCDEFGH<code>Z</code>


#### (  |   |  ) sub pattern
- (on|ues|rida) : M<code>on</code>day T<code>ues</code>day F<code>rida</code>y
- (Mon|Tues|Fri)day : <code>Monday Tueseday Friday</code>
- ..(id|esd|nd)ay : <code>Monday Tueseday Friday</code>


#### * + ? Quantifiers
- a*b : a는 있어도 없어도 상관없음 / <code>aab</code>c <code>ab</code>c <code>b</code>c
- a+b : a가 최소 1개 이상 있어야함 / <code>aab</code>c <code>ab</code>c bc
- a?b : a가 없거나 1개 / ~~a~~<code>ab</code>c <code>ab</code>c <code>b</code>c
- practice: [page12](http://zvon.org/comp/r/tut-Regexp.html#Pages~Page_12) ~ [page14](http://zvon.org/comp/r/tut-Regexp.html#Pages~Page_14)

#### { } : 갯수를 나타냄
- [els]{1,3} : On<code>e</code> ring to bring th<code>e</code>m a<code>ll</code> and in th<code>e</code> darkn<code>ess</code> bind th<code>e</code>m
- [els]{1,} : e,l,s가 1개에서 한 없이 많은 경우 포함

#### 수량자 + ?
- 해당 수량자의 최소조건??(가장 작은 수량)으로 해석 (lazy)
- r.+? : +?는 r뒤에 문자가 하나만 오는 경우를 찾음 (+ 수량자는 1~여러 개 )
- r.?? : r 한 글자로 구성된 경우 찾음


#### \w 
- 공백을 제외한 문자를 나타냄
- \W <-- 문자가 아니다( 공백, 특수문자 )


#### \d
- 숫자
- \D <-- 숫자가 아닌 것

#### \b
- 바운더리
- .\b : 첫글자
- \b. : 끝글자
- \B : 처음과 끝이 아닌 

#### \A
- 시작점
- cf)^ : multi line

#### \Z
- 마지막점
- cf)$ : multi line


#### (?= )
- 검색에만 도움을 주고 실제 결과에는 반영되지 않음
- \w+(?=X)
  - <code>AAA</code>X---aaax---111
