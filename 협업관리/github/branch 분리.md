
# Git 브랜치 워크플로우

여러 명이 함께 작업할 때, 브랜치를 나누고 메인 브랜치(main)에 통합하는 과정은 다음과 같습니다.

## 1. 브랜치 생성 및 작업
팀 프로젝트에서 작업할 때, 각 개발자는 메인 브랜치(main)에서 분기하여 자신의 작업 브랜치를 생성합니다.

```bash
# 메인 브랜치에서 새로운 브랜치 생성
git checkout main
git pull origin main # 최신 상태로 업데이트
git checkout -b feature/my-feature # 새로운 브랜치 생성
```

## 2. 브랜치에서 작업하기
각자 생성한 브랜치에서 작업을 진행합니다. 변경 사항을 커밋하고, 필요할 경우 원격 저장소에 푸시합니다.

```bash
# 파일 수정
git add .
git commit -m "Implement new feature"
git push origin feature/my-feature # 원격 저장소에 브랜치 푸시
```

## 3. 풀 리퀘스트(PR) 생성
작업이 완료되면 해당 브랜치를 메인 브랜치로 병합하기 위해 풀 리퀘스트(Pull Request, PR)를 생성합니다. 

- GitHub에서 해당 브랜치에 대한 PR을 생성합니다.
- 팀원들이 PR을 리뷰하고 피드백을 제공합니다.

## 4. 코드 리뷰 및 수정
팀원들의 피드백을 반영하여 코드를 수정하고, 다시 푸시합니다. PR에 대한 리뷰가 끝나고 승인이 되면 브랜치를 메인 브랜치에 병합합니다.

```bash
# 피드백 반영 후 커밋 및 푸시
git add .
git commit -m "Address review comments"
git push origin feature/my-feature
```

## 5. 메인 브랜치에 병합
PR이 승인되면 메인 브랜치에 병합합니다. 이 과정은 일반적으로 GitHub 등의 플랫폼에서 수행할 수 있습니다.

- GitHub에서 "Merge pull request" 버튼을 눌러 병합합니다.
- 병합 후 로컬 메인 브랜치를 최신 상태로 유지합니다.

```bash
# 메인 브랜치를 최신 상태로 업데이트
git checkout main
git pull origin main
```

## 6. 브랜치 삭제
병합이 완료된 브랜치는 더 이상 필요하지 않으므로 삭제합니다.

```bash
# 원격 브랜치 삭제
git push origin --delete feature/my-feature
# 로컬 브랜치 삭제
git branch -d feature/my-feature
```

## 브랜치 워크플로우 요약
1. **브랜치 생성**: 메인 브랜치에서 작업 브랜치를 분기합니다.
2. **작업 및 커밋**: 작업을 진행하고 변경 사항을 커밋합니다.
3. **푸시 및 PR 생성**: 작업 브랜치를 원격 저장소에 푸시하고, PR을 생성합니다.
4. **코드 리뷰**: 팀원들이 PR을 리뷰하고 피드백을 제공합니다.
5. **병합**: PR이 승인되면 메인 브랜치에 병합합니다.
6. **브랜치 삭제**: 병합된 브랜치는 삭제합니다.

이 과정을 통해 팀은 병렬로 작업할 수 있으며, 코드 품질을 유지하면서 효율적으로 협업할 수 있습니다.
