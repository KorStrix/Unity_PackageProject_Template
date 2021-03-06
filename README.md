# Unity_PackageProject_Template

이 프로젝트는 Unity Package 프로젝트에서 자주 보이는 패턴을 담아 Template 프로젝트로 만들었습니다.

## 무엇이 있는지?

### Master, Workspace Branch

하단은 `Unity Project` 폴더 구조입니다.

```
 Unity Project Sample
 |-- Assets
 |-- Packages
 └-- ProjectSettings
 ```
 
 그리고 하단은 `Unity Package Project` 폴더의 구조입니다.
 
 ```
 Unity Package Project Sample
 |-- Editor
 |-- Runtime
 |-- Tests
 └-- package.json
 ```
 
 `폴더 구조가 다르기 때문에`
 
 workspace 브렌치는 Unity Project와 이 Template 대상인 Package를 담고 있으며,
 workspace 브렌치에서 커밋할 경우 Github Action에 따라 master 브렌치로 Package 내용만 동기화 하는 구조입니다.
 

### Github Action
| Name | COMMENT | Branch |
| ------ | ------ | ------ |
| <b>UnityTest and Upload Package</b> | Unity UnitTest를 실행 후 이상이 없으면 Package를 master로 커밋합니다. | workspace |
| <b>Build and Deploy DocFX</b> | 문서화 도구인 DocFX를 빌드합니다. | workspace |
| <b>Copy Master to Workspace Branch</b> | Master Branch에서 바로 작업한 경우 workspace로 커밋합니다. | master |


## 설치 방법
설치 후 자동화가 필요한 공정입니다.

### 파일 수정
1. `master` branch의 `package.json`에 있는 내용들을 해당 패키지에 맞게 수정합니다.
2. `master` branch의 `.github/workflows/`에 있는 `.yml` 파일들의 `env` 항목들을 수정합니다.
3. `workspace` branch의 `.github/workflows/`에 있는 `.yml` 파일들의 `env` 항목들을 수정합니다.
4. `workspace` branch의 `Documentation/docfx.json` 파일의 `build/globalMetadata/_gitContribute/repo` 항목을 수정합니다.
5. `workspace` branch의 `Packages/package.json` 파일을 프로젝트에 맞게 수정합니다.

### Github Secret 추가
깃허브 엑세스 토큰은 깃허브에 로그인 하지 않고 저장소에 엑세스(커밋, 병합, 삭제 등)할수 있는 토큰이므로 외부에 노출되야 하지 않아야 합니다.
이런 외부에 노출되지 않아야 하는 것들을 보통 githubaction에서는 Secret으로 관리합니다.

##### 주의
토큰의 경우 원본파일을 저장하지 않을 경우 유실되므로 반드시 백업 해둘 것.

#### Github Access Token
Github Settings-Developer Settings-Personal access tokens-Generate new token
별도의 권한 체크 없이 Generate

#### Unity License Secret 얻어오기
Unity - `UnitTest` 의 경우 `UnityEngine` 에서 실행합니다.
하지만 `UnityEngine` 을 사용하려면 `Unity License` 가 있어야 합니다. (무료, 유료 관계없이)

이 `Repo` 는 `webbertakken/unity-test-runner`를 사용하기 때문에,
해당 `action`의 메뉴얼에 가서 `Unity License`를 설정해야 합니다.

링크 : https://unity-ci.com/docs
