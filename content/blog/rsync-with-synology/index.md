---
title: rsync를 이용한 동기화
date: "2021-01-19T05:25:03.284Z"
description: "rsync for synchonizing files"
---


# rsync란?

rsync는 remote sync의 약자로, 네트워크 상의 파일이나 디렉토리를 동기화할 때 사용합니다.
Unix 계열에서는 보편적인 utility로, 손쉽게 사용할 수 있습니다. 비슷한 류의 utility로는 scp나 rcp가 있으나, 훨씬 빠르고 효율적으로 동기화를 수행합니다.
자체적인 프로토콜인 rsync://를 지원하나, SSH를 이용하는 편이 훨씬 간단합니다.(참고로 rsync://인 경우는 873 포트를 이용합니다.)


# rsync 사용법

```
> rsync [options] source [USER@]host:destination

> rsync [options] [USER@]host:source destination
```

예를 들어 다음과 같습니다.

```
> rsync -az conda-sheet.pdf kiyonghan@myhome.net:/volume1/homes/kiyonghan/
```


### options

위의 예제에서 사용한 옵션은 다음과 같습니다.

* -a : archive mode라고 하여 -rlptgoD 옵션을 선택한 것과 동일합니다. 백업용 모드라고 생각하시면 됩니다. 하위 폴더 포함은 물론, symlink 나 owner, timestamp 대부분의 것들을 유지합니다.
* -z : 압축하여 전송합니다.

# Trouble shooting

## ERROR: module is read only

rsync가 쓰기 오류가 난 경우 입니다. synology에서 해당 destination에 대한 쓰기 권한이 있는지 확인할 필요가 있습니다.

Control Panel -> Shared Folder -> Destination Folder 의 Permission을 수정하면 됩니다.


# Reference

* [Rsync](https://en.wikipedia.org/wiki/Rsync)

* [What is archive mode](https://serverfault.com/questions/141773/what-is-archive-mode-in-rsync)

* [error: module is read only](https://serverfault.com/questions/425589/rsync-over-ssh-error-module-is-read-only-suddenly-appeared)