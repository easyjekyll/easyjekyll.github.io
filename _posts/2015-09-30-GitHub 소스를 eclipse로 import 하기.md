---
layout: post
tags: git eclipse
---


github 에는 clone URI 를 제공한다. 이 URI를 이용하여 desktop 에 소스를 복사 해 올수가 있고 자동으로 origin-client 관계가 설정된다. 당연히 client 에서의 수정사항을 origin 으로 commit & push 할 수가 있고, 
이러한 원리를 이용해 svn과 비슷한 환경을 셋팅 할 것 이다.







![1]({{site.url}}/images/post_img/GitHub 에서 eclipse 로 프로젝트 import 하기/1.png)
Git Repositories 창에서 Clone a Git Repository and add the clone to this view 클릭

**사진에서는 잘 안보이네요. 아이콘 잘 확인 해 주세요.**


![2]({{site.url}}/images/post_img/GitHub 에서 eclipse 로 프로젝트 import 하기/2.png)
clone URI 를 입력하면 나머지 blank 는 자동 입력됨.


![3]({{site.url}}/images/post_img/GitHub 에서 eclipse 로 프로젝트 import 하기/3.png)
remote 에 있는 branch 모두 체크 후 Next


![4]({{site.url}}/images/post_img/GitHub 에서 eclipse 로 프로젝트 import 하기/4.png)
그냥 기본설정으로 두고 Finish



![6]({{site.url}}/images/post_img/GitHub 에서 eclipse 로 프로젝트 import 하기/6.png)
eclipse Git Repositories 에 추가가 되고 (실제로 내 pc에 clone 되어있는 상태임) 우클릭하여 Import Projects 선택



![1]({{site.url}}/images/post_img/GitHub 에서 eclipse 로 프로젝트 import 하기/7.png)
Working Directory 밑에 있는 Import 할 프로젝트 선택


![1]({{site.url}}/images/post_img/GitHub 에서 eclipse 로 프로젝트 import 하기/8.png)
Finish




