# Git submodule

Submodule은 다른 Git repository를 포함하는 기능을 제공하여, 프로젝트의 외부 종속성을 쉽게 관리할 수 있다.

## Clone

Git repository 안에 submodule이 포함되어 있을 때 `git clone` 사용법은 다음과 같다.

1. 두 단계로 나눠서 하는 경우
   
   1. **기본 클론**: 먼저 기본적으로 repository를 clone한다.
       
       ```bash
       git clone <repository_url>
       ```

   2. **submodule 초기화 및 업데이트**: clone한 후 submodule을 초기화하고 업데이트한다.

       ```bash
       cd <repository_directory>
       git submodule init
       git submodule update
       ```

2. 한 꺼번에 하는 경우
   
   ```bash
    git clone --recurse-submodules <repository_url>
   ```

## Update

submodule이 추가되거나 변경될 경우 아래와 같은 방법으로 submodule을 업데이트할 수 있다.

파일 구조는 다음과 같다고 가정하자.

my_project/<br>
├── my_submodule<br>
├── ...<br>
└── ...

1. Parent directory로 이동

    ```bash
    cd my_project
    ```

2. Submodule 최신화
   
   ```bash
   git submodule update --remote
   ```

3. 변경 사항 commit 및 push
   
   ```bash
   git add my_submodule
   git commit -m "<commit message>"
   git push origin <branch_name>
   ```


## Push

submodule에서 변경사항이 있을 경우 다음과 같은 절차를 따른다.

1. **Submodule에서 변경사항 commit 및 push**
   - Submodule directory로 이동하여 변경사항을 commit하고 push한다.
  
  ```bash
    cd my_project/my_submodule
    git add .
    git commit -m "<commit message>"
    git push origin <branch name>
  ```

2. **Parent repository에서 submoudle 업데이트**
   - Submodule에서 commit과 push를 완료한 후, parent directory로 돌아가서 submodule의 최신 commit을 반영한다.
  
  ```bash
  cd ..
  git add my_submodule
  git commit -m "<commit message>"
  git push origin <branch_name>
  ```

## Delete

Submodule 삭제

```bash
git submodule deinit -f -- my_project/my_submodule
git rm -f my_project/my_submodule
rm -rf .git/modules/my_project/my_submodule
```

## Re-add

Submodule 재추가

```bash
git submodule add <submodule_repository_url> my_project/my_submodule
git submodule init
git submoudle update
```