Introduction
===

## ssh 에 대한 개요

[ssh 뜻, 설명]

- https://www.ssh.com/
- https://www.openssh.com/

`linux`나 `macOS` 환경에서는 OpenSSH가 기본적으로 탑재되어 있지만

`Windows`의 경우에는 기본적으로 탑재되어 있지 않지만
git을 설치할 때 SSH 설정을 따로 건들이지 않았다면(bundled OpenSSH(default)로 설정 = git에서 제공할 경우) git의 bash에서 실행하실 수 있습니다

# ssh-key 생성

## ssh 키가 이미 생성되어 있는 지 확인 하는 방법

ssh 키는 `~/.ssh`(사용자폴더 아래에 숨김디렉토리) 디렉토리 아래에 존재합니다

- 목표로 하는 ssh 키가 등록되어 있는 지 확인

	```bash
	eval $(ssh-agent -s)
	ssh-add -l
	```
	ssh 에이전트에 키가 등록되어 있는지 확인할 수 있습니다

## KEY 생성

[ssh-keygen]

# ssh-key 등록

[ssh-agent]
[ssh-add]

# ssh 연결 테스트

옵션 `-T`를 추가하여 해당 url와의 연결을 테스트할 수 있습니다

```bash
ssh -T git@github.com # github의 경우
ssh -T git@gitlab.com # gitlab의 경우
```

연결 내역까지 보고자 한다면 `-v` 옵션을 추가해서 내용을 확인할 수 있습니다

`Hi ~!`(GitHub)이나 `Welcome ~`(GitLab)와 같은 메시지가 출력되면 성공적으로 인증되었다는 뜻입니다

Appendix
===

# ssh-key 설정

# ssh-key 해제

# references

- [SSH Home Page, Published 220615, Accessed 220718](https://www.ssh.com/academy/ssh)
- [linux manual page - ssh-keygen, Published 220624, Accessed 220718](https://man7.org/linux/man-pages/man1/ssh-keygen.1.html)