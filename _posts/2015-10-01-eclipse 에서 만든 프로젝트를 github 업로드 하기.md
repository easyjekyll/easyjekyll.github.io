---
layout: post
tags: git eclipse
---

eclipse 에서 프로젝트를 생성 후, 내가 가진 git hub에 업로드를 하고 싶을때가 있다.
이럴때는 clone 으로 remote 에서 client 로 내려받은 폴더에 내 프로젝트를 이동 후 push 를 하는 식으로 진행 하면 된다.


![시작]({{site.url}}/images/post_img/eclipse 에서 프로젝트를 local repository 에 fetch 하기/1.png)
package exploler 에서 프로젝트 우클릭 -> Share Project 선택  


![2]({{site.url}}/images/post_img/eclipse 에서 프로젝트를 local repository 에 fetch 하기/2.png)
Git 선택  


![3]({{site.url}}/images/post_img/eclipse 에서 프로젝트를 local repository 에 fetch 하기/3.png)
target 디렉토리 선택
*Working directory 는 소스를 이동시킬 target directory 라고 보면 된다. 사진에서의 Working directory는 remote 에서 clone 받은 repo 의 위치가 D:\GItHubLocalRepo\danal.kcredit 일 경우 저렇게 표시되는 것 이다.*  


![4]({{site.url}}/images/post_img/eclipse 에서 프로젝트를 local repository 에 fetch 하기/4.png)
svn 에서 commit 하듯이  


![5]({{site.url}}/images/post_img/eclipse 에서 프로젝트를 local repository 에 fetch 하기/5.png)
모두 선택후, Commit and Push 선택  


![6]({{site.url}}/images/post_img/eclipse 에서 프로젝트를 local repository 에 fetch 하기/6.png)
그다음부터는 크게 신경안쓰고 next 하면 됩니다.  




이렇게 하여 github의 repository 내에 내가 작성 중이던 project를 업로드 하였습니다.
