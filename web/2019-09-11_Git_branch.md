# Git Branch(나뭇가지의 비유적 표현)

- Git 브랜치는 매우 가볍다
- 순식간에 브랜치를 만들고 브랜치 사이를 이동할 수 있다.
- git이 가지고온 혁신 중 하나는 브랜치 기능을 매우 쓸만한 수준까지 만들었다는 것.



```bash
$git branch
```

현재 브랜치 상황 확인



```bash
$git branch ssafy
```

ssafy라는 이름의 브랜치를 생성함

![banch](.\image\banch.PNG)

생성된 이후 git banch를 이용해 확인

> ssafy를 생성하기전 a,b 라는 텍스트 파일을 생성하였다.



```bash
$git checkout ssafy
```

ssafy의 브런치로 이동합니다. 이후 이 폴더에서 c라는 텍스트 파일을 생성하여도 master에서는 변화가 없다.

즉 master로 이동하면 c가 삭제되는 모습을 볼수 있다. 반대로 master에서 ssafy로 이동한다면 c라는 파일이 다시 생성된다. 



```bash
$git checkout-b branch_name
```

브런치를 생성하며 이동합니다.



 이를 이용하여 협업 등 에 사용합니다.

master(원본)를 유지하고 또다른 추가 기능을 제작하며 실패했을경우 취소가 용이하고 병합역시 용이합니다. 



### 삭제를 하려면 

```bash
$git branch -d ssafy
```

master로 이동하여 삭제하여야합니다.  병합 되지 않았을경우 d를 대문자를 사용하여 지우라고 표시됩니다.



### 병합을 하려면

```bash
$git merge feture/test
```

병합은 마스터를 기준으로 합니다. 

### Fast-forword 상황

- 병합되는 순간에 마스터에 변화가 없다는 의미입니다.
- feture/test에서 마스터에 추가된 모습만 master에 추가됩니다.
- log는 feture/test에서의 마지막 커밋이 최종 커밋이 될 것 입니다.
- 오류없이 끝난 제일 좋은 케이스입니다.

> git log --oneline 으로 log를 한줄로 볼 수 있습니다.



### merge-commit상황

#### 3-way-merge

branch 에서  commit 즉 버전이 생기고 그 이후 마스터에서 변화가 생겻을때 3-way-merge 가 발생합니다.

이 상황에서 merge를 한다면 발생하는 상황입니다.  

이 상황에서 병합한다면 빔이 발생하는대 esc => :wq로 git이 branch와 마스터를 병합하여 커밋을 생성합니다.

- 서로가 다른걸 수정했을경우에만 발생합니다.

>git log --oneline --graph
>
>깃의 로그를 한줄로 그래프로 보여주게됩니다.



### 충돌 상황

branch에서 a를 수정하고 master(HEAD)에서 a를 수정했다면 충돌상황이 발생합니다. 이 경우 merge(병합)을 한다면 git에서 수정을 하라는 메시지가 발생합니다.(git의 능력 밖입니다. 충돌이 난 파일을 git이 알려주며 사람이 해결하여야합니다.)

이후 커밋에 메시지를 사용하지 않고 3-way와 같은 방식으로 진행합니다.

- 같은 파일에 서로 다른 줄을 수정한다면 충돌이 일어나지 않습니다.



## 협업 Branch

- master

repositories에서 새로운 레포지토리를 생성

일련의 과정을 거쳐 푸시



- branch

레포지토리를 클론

master에서 추가

push => 디나이

branch생성 => git add commit 

git push -u origin branch_name

콜라보레이터가 됫다면 마스터에게 브런치로서 생성이 됩니다.



## 1. feture branch wolkflow

- master

레포지토리에서 github에서 branch를 클릭해 pull request를 선택

Pull request

-기능 개발을 끝내고 master에 바로 병합시키는게 아니라 브랜치를 중앙 원격 저장소에 올리고(push) master에 병합을 요청

이후 merge



주의사항

-중앙에서 병합을 했따면, 다른 팀원들은 master 브랜치를 pull 받아야 한다.

> 소규모 팀

---

## 2. forking workflow

master

- 레포지토리생성

branch

- 레포지토리 fork 
- 자신의 레포지토리에 복사하여 가져옴
- 클론하여 가져옴
- 원본의 주소를 remote로 연결합니다.

> upstrem으로 연결

- branch를 하나 생성하고 이동합니다.
- 필요한것을 변경하고 add => commit
- git push -u origin feture/login



git hub에서 pull request를 원본에게 요청하는 메시지를 보냅니다.



같은 줄을 변경하여 충돌상황이 발생하였을 경우

- master가 직접 변경
- 거절 후 branch가 변경