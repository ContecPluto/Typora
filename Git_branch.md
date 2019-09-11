# 상황 1.fast-forwark

1. feture/text branch 이동

```bash
$git checkout -b feture/test
$ (feture/test)
```



2. 작업 완료후 commit

```bash
touch test.md
git add .
git commit -m "Complte test.md"
```



3. master 이동

```bash
git checkout master
$ (master)
```



4. master에 병합

```bash
git merge feture/test
```

5. 결과
   - 단순히 HEAD가 최신 COMMIT으로 이동
   - feture/test branch 생성 이후 mater branch의 이력에 변화가 없었기 때문



6. branch 삭제

```bash
git branch -d feture/test
```



## 2.merge commit

1. feture/login 이동

```bash
git checkout -b feture/login
```



2. 작업 완료 후 commit

```bash
$ touch login.md
$ git add .
$ git commit -m "complate login.md"
```



3. master로 이동

```bash
$ git checkout master
```



4. master에 추가 commit 생성

```bash
$ touch master.md
$ git add .
$ git commit -m "fix master.md"
```



5. mater에 병합

```bash
$ git merge feture/login
```



6.  자동으로 merge commit 발생

```bash
Merge branch 'feture/login'

#please enter a commit ...
....
```

- Vim 에디터로 열림
- 메시지를 수정하고자하면 i로 편집모드로 바꾼 다음에  COMMIT을 수정하고
- `esc` + `wq` 를 통해 저장 및 종료

7. commit 그래프 확인하기

```bash
$ git log --oneline --graph
```

```
*   be97d68 (HEAD -> master) Merge branch 'feture/article'
|\
| * a66ad1c (feture/article) fix a.txt
* | 1facbfc fix a.txt master
|/
*   e57d8f9 Merge branch 'feture/signout'
|\
| * a4eab93 complete login.txt
| * 9a1ca93 Complte signout.txt
* | 6e838da Make master.txt
|/
* 3f81401 complte text.txt
* 1d42d78 first commit
```



8. branch삭제

```bash

```



## 3. merge conflict

1. feture/article branch 생성 및 이동

```bash
$ git checkout -b feture/article
```

2. 작업 완료 후 commit

```bash
#충돌을 만들어 낼 파일에 코드를 작성
$ git add .
$ git commit -m "fix minor update"
```

3. master로 이동

```bash
$ git checkout master
```

4. mater에 추가 commit 만들기

```bash
#feture/article branch 에서 수정한 파일과 동일 파일의 같은 위치를 수정함
$ git add .
$ git commit -m "fixed master update"
```

5. master에 병합

```bash
$ git merge feture/article
```

6. merge confilct 발생

```bash
$ git merge feture/article
Auto-merging a.txt
CONFLICT ...
Automatic merge faild; fix conflicts and then commit result.
```

7. 충돌 확인 해결

```bash
#충돌이 일어난 파일 열기
<<<<<<<<<HEAD
master에서 작성한 내용
========================
feture/article 에서 작성한 내용
>>>>>>>>>>>>>feture/article
#원하는 코드로 수정
```

8. merge commit 진행

```bash
$ git add .
$ git commit
```

- 커밋 메시지는 미리 작성되어 있다.

9. commit 그래프 확인

```bash
$ git log --oneline --graph
```

```bash
*   be97d68 (HEAD -> master) Merge branch 'feture/article'
|\
| * a66ad1c (feture/article) fix a.txt
* | 1facbfc fix a.txt master
|/
*   e57d8f9 Merge branch 'feture/signout'
|\
| * a4eab93 complete login.txt
| * 9a1ca93 Complte signout.txt
* | 6e838da Make master.txt
|/
* 3f81401 complte text.txt
* 1d42d78 first commit
```

10. branch 삭제

```bash
$ git branch -d feture/article
```

