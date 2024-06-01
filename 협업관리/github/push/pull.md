# Git Pull vs. Git Pull --rebase

## git pull origin main

이 명령어는 원격 `main` 브랜치에서 변경 사항을 가져와 로컬 브랜치와 병합합니다. `merge` 전략을 사용하여 커밋 기록이 비선형적으로 합쳐집니다. 즉, 병합 커밋이 생성됩니다.

### 예시
```sh
git pull origin main
```

이 명령어의 결과로 병합 커밋이 생성될 수 있으며, 다음과 같은 형태로 로그가 보일 수 있습니다:
```
*   commit abcdef (HEAD -> feature-branch)
|\  
| * commit 123456 (origin/main)
|/
* commit 789012 (previous commit on feature-branch)
```

## git pull --rebase origin main

이 명령어는 원격 `main` 브랜치에서 변경 사항을 가져와 로컬 브랜치의 베이스로 재설정합니다. `rebase` 전략을 사용하여 커밋 기록이 선형적으로 유지됩니다. 즉, 로컬 커밋이 원격 커밋 뒤로 재배치됩니다.

### 예시
```sh
git pull --rebase origin main
```

이 명령어의 결과로 커밋 로그가 더 선형적이고 깔끔하게 유지됩니다:
```
* commit 123456 (origin/main, main)
* commit 789012 (HEAD -> feature-branch)
* commit abcdef (previous commit on feature-branch)
```

## 차이점 요약

- **병합 커밋**:
  - `git pull origin main`: 병합 커밋이 생성될 수 있어 커밋 기록이 비선형적으로 됩니다.
  - `git pull --rebase origin main`: 병합 커밋 없이 커밋 기록이 선형적으로 유지됩니다.

- **충돌 해결**:
  - `git pull origin main`: 병합 중 충돌이 발생하면, 병합 충돌을 해결해야 합니다.
  - `git pull --rebase origin main`: rebase 중 충돌이 발생하면, 각 커밋에 대해 충돌을 순차적으로 해결해야 합니다.

- **커밋 기록**:
  - `git pull origin main`: 비선형적인 커밋 기록으로, 머지 히스토리가 남습니다.
  - `git pull --rebase origin main`: 선형적인 커밋 기록으로, 머지 히스토리가 없습니다.

## 언제 사용할까?

- **`git pull origin main`**:
  - 팀에서 여러 명이 협업 중이고 병합 커밋을 통해 변경 사항을 명확히 구분하고 싶을 때.
  - 병합 커밋을 남겨두어 히스토리를 추적하고자 할 때.

- **`git pull --rebase origin main`**:
  - 깔끔한 커밋 히스토리를 유지하고 싶을 때.
  - 변경 사항을 선형적으로 유지하고 싶을 때.
  - 협업자가 많지 않거나 병합 커밋을 피하고 싶을 때.

## 예시 시나리오

1. **`git pull origin main`**:
   ```sh
   git pull origin main
   ```
   - 원격 저장소의 `main` 브랜치에서 변경 사항을 가져와 현재 브랜치에 병합합니다.
   - 병합 커밋이 생성될 수 있습니다.

2. **`git pull --rebase origin main`**:
   ```sh
   git pull --rebase origin main
   ```
   - 원격 저장소의 `main` 브랜치에서 변경 사항을 가져와 현재 브랜치의 베이스로 재설정합니다.
   - 병합 커밋 없이 커밋 기록이 선형적으로 유지됩니다.

## 변경 사항을 푸시하는 방법

로컬 변경 사항을 원격 저장소에 푸시하려면 다음 명령어를 사용합니다:

```sh
git push origin <branch-name>
```

여기서 `<branch-name>`은 푸시할 브랜치의 이름입니다. 예를 들어, `main` 브랜치에 푸시하려면 다음과 같이 입력합니다:

```sh
git push origin main
```