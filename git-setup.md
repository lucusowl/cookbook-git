Introduction
===

기본적인 **git CLI**설정 설명서입니다

git CLI가 git에서 지원하는 모든 기능을 이용할 수 있기에 추천하지만

GUI와 같은 직관적이고 간편한 인터페이스를 원한다면 git UI App(VS Code, Source Tree, git Kraken, [etc](https://git-scm.com/downloads/guis/))을 이용해 주세요

# git 설치

[공식 다운로드 주소](https://git-scm.com/downloads)에서 사용하고 있는 OS 상황에 맞게 git을 다운로드 & 설치 합니다

# git 설정

설정 범위에 따라 적용되는 내용을 달리 해줄 수 있습니다

범위에 대한 자세한 설명은 [아래의 git 설정 범위](#git-설정-범위) 단락을 확인해주세요

## 초기 설정 과정

1. **작성자Author 설정**

	작성자 이름 & 이메일 설정합니다

	```bash
	git config --global user.name "NAME"
	git config --global user.email "emailname@hostname"
	```

	`user.name`과 `user.email`은 원격 저장소에서 등록된 사용자를 식별하기 위한 용도로도 사용되니 참고해주세요

2. **편집기 설정**

	git의 텍스트 정보를 편집하기 위해 자동으로 열리는 편집기 프로그램을 설정합니다

	예를 들어 VScode를 편집기로 실행시키는 경우 (터미널에서 `code --help`가 동작한다면)

	```bash
	git config --global core.editor "code --wait"
	```

	_`--wait`옵션은 편집기를 종료할 때까지 터미널이 다른 작업을 수행하지 않게 대기시키는 옵션입니다_

	이외에도 편집기의 실행 경로나 실행할 때의 옵션을 `"`로 묶어 설정할 수 있습니다

	```bash
	git config --global core.editor "파일 실행 command"
	```

3. **기타 편의 설정**
   1. 줄바꿈 처리

		Windows의 경우 줄바꿈시 '캐리지 리턴'이 포함되는 경우(`\r\n`)가 있고, 다른 운영체제에서도 복사한 내용에 포함되어 있을 수 있기에
		
		모든 줄바꿈을 '라인 피드'(`\n`)만으로 설정하는 명령어입니다

		Windows의 경우,

		```bash
		git config --global core.autocrlf true
		```

		이외의 OS의 경우,

		```bash
		git config --global core.autocrlf input
		```

그 밖에 개인의 편의에 맞게 색깔이나 서버, 기본 템플릿포멧, 등을 customizing 할 수 있습니다

diff 와 merge 와 같이 운영에 구제적인 정보가 필요해 별도의 tool이 있는 경우, 기본 tool 외에 [다른 tool을 설정하여](#다른-tool-설정하기) 사용할 수도 있습니다

자세한 custom 설정 요소는 [git doc 링크](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration) 참고해 주세요

# 원격 저장소 remote repository 설정

git은 `distributed version control system`입니다

그래서 중앙식 시스템이 강제되지 않지만 백업과 공유의 편의를 위해
제3자에 해당하는 host서버를 따로 두어 이 host를 원격 저장소로 활용하는 방식이 많습니다

## 원격 저장소, Git Server as Service 가입

대표적인 원격 저장소로 아래와 같은 서비스 제공 플랫폼들이 있습니다.
- [GitHub](https://github.com/)
- [GitLab](https://gitlab.com/)
- [Bitbucket](https://bitbucket.org/)

[다른 Git Server 목록 및 비교 링크, 위키백과](https://en.wikipedia.org/wiki/Comparison_of_source-code-hosting_facilities)

상황에 맞는 원하는 저장소를 골라 계정(계정 이메일은 [위에서 설정한](#초기-설정-과정) 이메일로 진행)을 생성해주세요

## SSH 설정

원격 저장소와 데이터를 주고 받기 위해서는 작성자 식별을 위해 로그인과정을 거칩니다

공유할 때마다 로그인하는 번거로움을 줄이기 위해서는 미리 원격저장소와 로컬컴퓨터 간의 SSH 인증 설정을 미리 해두면 좋습니다

Personal Access Token(PAT)발급 & 캐싱과 같은 여러 방법으로 인증을 처리할 수 있지만 SSH는 암호통신을 위해 만들어진 프로토콜인 만큼 보편적으로 사용되는 기술이기에 해당 방법으로 설정합니다

자세한 설정법은 [여기][추가예정]를 참고해주세요

Appendix
===

# git 설정 범위

설정 범위는 크게 `시스템`, `사용자(전역)`, `프로젝트(로컬)` 3가지로 구분됩니다

설정된 내용의 우선순위는 `프로젝트`, `사용자`, `시스템` 순입니다

설정된 내용을 읽어 오려면

```bash
git config --list [범위 option]
```

설정된 내용을 변경 하려면 해당 파일을 열거나

```bash
git config --edit [범위 option]
```

로 편집기를 열어 수정할 수 있습니다

1. ### 시스템 범위

	모든 사용자와 모든 프로젝트의 git 활동에 적용되는 설정입니다

	`<git 프로그램 PATH>/etc/gitconfig`(Windows) 또는
	`/etc/gitconfig`(linux) 파일안에 설정 내용이 저장되어 있습니다

	`--system` 옵션으로 접근할 수 있습니다

2. ### 사용자 범위

	현재 사용자의 git 활동에 적용되는 설정입니다

	`~/.gitconfig` 파일안에 설정 내용이 저장되어 있습니다

	`--global` 옵션으로 접근할 수 있습니다

3. ### 프로젝트 범위

	현재 프로젝트의 git 활동에 적용되는 설정입니다

	`<프로젝트 PATH>/.git/config` 파일안에 설정 내용이 저장되어 있습니다

	생략하거나 `--local` 옵션으로 접근할 수 있습니다

# 다른 tool 설정하기

`difftool`나 `mergetool`와 같은 특정 운영 목적의 UI의 git CLI외에 다른 tool을 설정하는 방법입니다

## 설정 요소

- `diff.tool`: 어떤 difftool을 사용할 지
- `difftool.*.cmd`: 해당 도구를 실제 실행하는 명령어
- `diff.external`: 어떤 wrapper 스크립트를 사용할 지, `diff`명령어를 치면 기본 git이 아니게 변경
  - _Wrapper 스크립트_
  - parameter 구성(7개): `path old-file old-hex old-mode new-file new-hex new-mode`
- 그외의 요소: [링크](https://git-scm.com/docs/git-difftool)
- `merge.tool`: 어떤 mergetool을 사용할 지
- `mergetool.*.cmd`: 해당 도구를 실제 실행하는 명령어
- `mergetool.*.trustExitCode`: 해당 도구가 반환하는 exit 코드가 Merge성공 여부로 사용할 지
- `merge.keepBackup`: Merge 동작 수행후, 원래 파일을 백업할 지(default: false)
- 그외의 요소: [링크](https://git-scm.com/docs/git-mergetool)

## tool 설정 예시

`diff`와 `merge`를 VS Code에서 진행하게 하는 예시입니다

- 파일로 설정하는 방법

	해당 설정 파일(`~/.gitconfig`)을 열고, 아래의 내용을 입력합니다
	```
	[diff]
		tool = vscode-difftool
	[difftool "vscode-difftool"]
		cmd = code --wait --diff $LOCAL $REMOTE

	[merge]
		tool = vscode-mergetool
	[mergetool "vscode-mergetool"]
		cmd = code --wait $MERGED
		trustExitCode = true
	```

- 명령어로 설정하는 방법

	```bash
	git config --global diff.tool vscode-difftool
	git config --global difftool.vscode-difftool.cmd "code --wait --diff \$LOCAL \$REMOTE"
	git config --global merge.tool vscode-mergetool
	git config --global mergetool.vscode-mergetool.cmd "code --wait \$MERGED"
	git config --global mergetool.vscode-mergetool.trustExitCode true
	```

# git 설정 해제 & 변경

해제: `--unset`옵션과 함께 키를 입력해주면 됩니다
변경: `--replace`옵션과 함께 키와 값을 입력해주면 됩니다

해당 설정의 키에 해당하는 값이 여래 개일 경우에는 `--unset-all`, `--replace-all`와 같이 뒤에 `-all`을 붙여줍니다

예시) 
```bash
git config --global --unset user.name
```