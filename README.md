# Unity_PackageProject_Template

이 프로젝트는 Unity Package 프로젝트에서 자주 보이는 패턴을 담아 Template 프로젝트로 만들었습니다.

## 무엇이 있는지?

### Master, Workspace Branch

하단은 Unity Project 폴더 구조입니다.

```
 Unity Project Sample
 |-- Assets
 |-- Packages
 └-- ProjectSettings
 ```
 
 그리고 하단은 Unity Package Project 폴더의 구조입니다.
 
 ```
 Unity Package Project Sample
 |-- Editor
 |-- Runtime
 |-- Tests
 └-- package.json
 ```
 
 폴더 구조가 다르기 때문에 
 
 workspace 브렌치는 Unity Project와 이 Template 대상인 Package를 담고 있으며,
 workspace 브렌치에서 커밋할 경우 Github Action에 따라 master 브렌치로 Package 내용만 동기화 하는 구조입니다.
 

### Github Action
| Name | COMMENT | Branch |
| ------ | ------ | ------ |
| <b>UnityTest and Upload Package</b> | Unity UnitTest를 실행 후 이상이 없으면 Package를 master로 커밋합니다. | workspace |
| <b>Build and Deploy DocFX</b> | 문서화 도구인 DocFX를 빌드합니다. | workspace |
| <b>Copy Master to Workspace Branch</b> | Master Branch에서 바로 작업한 경우 workspace로 커밋합니다. | master |
