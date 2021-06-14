# 다국어 마크다운 생성기

🚀 **version 0.2.0**

[![Multilingual Markdown Generator](https://img.shields.io/badge/markdown-multilingual%20🌐-ff69b4.svg)](https://github.com/ryul1206/multilingual-markdown)
![GitHub code size in bytes](https://img.shields.io/github/languages/code-size/ryul1206/multilingual-markdown.svg)
![GitHub](https://img.shields.io/github/license/ryul1206/multilingual-markdown.svg)
[![CodeFactor](https://www.codefactor.io/repository/github/ryul1206/multilingual-markdown/badge/master)](https://www.codefactor.io/repository/github/ryul1206/multilingual-markdown/overview/master)

</div>

🌏 [English](README.md), [Français](README.fr.md), [한국어](README.kr.md)

---

**목차** ⚡

1. [개요 ](#개요-)
    1. [작동 방식](#작동-방식)
    1. [기능들](#기능들)
1. [설치](#설치)
1. [사용법](#사용법)
    1. [(1) 파일 지정](#1-파일-지정)
    1. [(2) 재귀 옵션 (recursive option)](#2-재귀-옵션-recursive-option)
    1. [부연 설명](#부연-설명)
1. [명령어 태그](#명령어-태그)
    1. [헤더](#헤더)
    1. [뱃지 달기](#뱃지-달기)
    1. [본문](#본문)
1. [기여하기](#기여하기)
    1. [Contributors](#Contributors)

## 개요 🔎

### 작동 방식
![how it works](how-it-works.png)

### 기능들

- 파일 이름 뒤에 자동 접미사
- 접미사 생략 옵션 (한 개 언어만 가능)
- UTF-8 인코딩. 따라서 *아마도* 거의 모든 언어를 지원할겁니다. :) 🍷
- 자동 목차
    - 목차로 만들 제목수준 설정 가능
    - 목차에서 이모티콘 **표시/생략** 설정 가능

## 설치

먼저 필요한 파이썬3 패키지를 안전한 user 권한으로 설치합니다. ()

```sh
pip3 install click --user
```

아래 명령을 사용하여`multilang_md.py`를 홈 디렉토리에 숨겨진 파일로 다운로드합니다.

```sh
cd
curl -fsSL https://raw.githubusercontent.com/ryul1206/multilingual-markdown/master/multilang_md.py > .multilang_md.py
```

그 다음, 아래와 같은 alias를 당신의 shell에 등록하세요. 그저 아래 내용을 `~/.bashrc`나 `~/.zshrc`의 마지막에 추가하면 됩니다.

```sh
# vim ~/.bashrc
alias mmg="python3 ~/.multilang_md.py"
```

이제 새터미널을 열면 새로운 명령어 `mmg`를 사용할 수 있습니다.

```sh
mmg --help
```

## 사용법

`{파일이름}.base.md` 파일을 만듭니다. 예제는 [README.base.md](README.base.md) 와 [example.base.md](example/example.base.md) 를 참고하시고, 작성하는 규칙은 [명령어 태그](#명령어-태그)를 참고하십시오.

**(경고) 베이스 파일 형식이 잘못되면 생성된 스타일이 깨집니다.**

### (1) 파일 지정

다국어로 생성하고 싶은 `*.base.md` 파일을 `mmg` 명령에 인자(arguments)로 넣어줍니다.

```sh
mmg FileName.base.md
```

여러 인자는 띄어쓰기로 구분합니다.

```sh
mmg Foo.base.md Bar.base.md Baz.base.md
```

### (2) 재귀 옵션 (recursive option)

현재 디렉토리와 하위 디렉토리에 있는 모든 베이스 파일을 변환하고 싶다면 `--recursive` 또는 `-r` 옵션을 사용하세요.
recursive option은 명령어가 입력된 위치를 기준으로 모든 하위 폴더를 탐색합니다.
아직은 인자로 폴더를 지정할 수 없습니다.

```sh
mmg --recursive
```

### 부연 설명

- 각 폴더의 동일한 위치에서 `{파일이름}.{접미사}.md`으로 된 파일들을 볼 수 있습니다. 예를 들어:
    - 기본일 때: `{파일이름}.en.md`, `{파일이름}.kr.md`, `{파일이름}.es.md`, ...
    - `en`에 접미사 생략 옵션일 때: `{파일이름}.md`, `{파일이름}.kr.md`, `{파일이름}.es.md`, ...
- 이 생성기는 자동생성된 파일을 매번 덮어쓰기 때문에, `{파일이름}.base.md` 파일을 수정하더라도 매번 지울 필요가 없습니다. 그저 방금 전 2단계를 다시 실행하면 됩니다.

## 명령어 태그

### 헤더

헤더는 반드시 본문이 시작하기 전에 선언되어야 합니다.

1. **접미사 선언**

    사용할 언어를 선언하십시오. 다음 예제는 `en`과 `kr`을 키워드로 선언하였습니다. 이 키워드들은 접미사로 사용됩니다.

    ```markdown
    <!-- multilingual suffix: en, kr, fr, es, jp, cn -->
    ```

1. **접미사 숨기기** (필수 아님)

    `no suffix` 옵션은 파일을 생성할 때 접미사가 붙는 것을 방지할 수 있습니다. 다시 말하자면 `no suffix`를 `en`으로 설정하면 `파일이름.en.md`가 아니라 `파일이름.md`가 생성됩니다. **GitHub**에서 메인 `README`는 접미사가 붙으면 인식이 안되기 때문에 이 기능이 유용합니다.

    ```markdown
    <!-- no suffix: en -->
    ```

### 뱃지 달기

[![Multilingual Markdown Generator](https://img.shields.io/badge/markdown-multilingual%20🌐-ff69b4.svg)](https://github.com/ryul1206/multilingual-markdown)
[![Multilingual Markdown Generator](https://img.shields.io/badge/markdown-multilingual%20🌐-yellow.svg)](https://github.com/ryul1206/multilingual-markdown)
[![Multilingual Markdown Generator](https://img.shields.io/badge/markdown-multilingual%20🌐-green.svg)](https://github.com/ryul1206/multilingual-markdown)
[![Multilingual Markdown Generator](https://img.shields.io/badge/markdown-multilingual%20🌐-blue.svg)](https://github.com/ryul1206/multilingual-markdown)
...

```markdown
[![Multilingual Markdown Generator](https://img.shields.io/badge/markdown-multilingual%20🌐-ff69b4.svg)](https://github.com/ryul1206/multilingual-markdown)
```

### 본문

파서가 아래의 태그들를 읽는 순간부터 그 이후에 읽는 모든 것은 메인 텍스트로 인식합니다. (그래서 헤더를 메인 이전에 적어야 합니다.)

1. **키워드**

    1. 언어 분류

        언어를 구분하는 태그는 `<!-- [키워드] -->` 같은 형태로 작성합니다. 하나의 키워드가 인식되면 다른 키워드가 나타날 때까지 해당 키워드로 인식됩니다.

        ```markdown
        <!-- [en] -->
        <!-- [kr] -->
        <!-- [fr] -->
        <!-- [es] -->
        <!-- [jp] -->
        <!-- [cn] -->
        ...
        ```

    1. 공통 영역

        생성될 모든 파일에 공통적으로 들어갈 내용은 `common` 키워드를 사용하여 작성하면 됩니다.

        ```markdown
        <!-- [common] -->
        ```

    1. 무시되는 영역

        주석이나 TODO와 같은 몇 가지 항목들은 생성될 파일에 포함하고 싶지 않는 경우가 있습니다. 그런 경우 `ignore` 키워드를 사용하세요.

        ```markdown
        <!-- [ignore] -->
        ```

1. **목차**

    아래 태그는 생성기에 의해 목차로 자동교체됩니다. 목차의 수준은 `level` 부분을 통해 정할 수 있습니다. 가장 큰 제목(`# 제목`)은 html에서 `<h1>`이기 때문에 `level 1`입니다.

    **(주의) `#`으로 표시하는 마크다운의 제목수준을 건너뛰면 에러가 발생합니다. 다시말해, `##`의 하위 제목은 `###` 이여야 합니다.**

    ```markdown
    <!-- [[ multilingual toc: level=2~3 ]] -->
    ```

    1. **`level` 옵션**
        - `level`을 표기하는 방법은 총 4가지입니다. 여러분의 필요에 따라 숫자는 바꾸시면 됩니다.
            - `level=2`: 2수준의 제목만 목차로 만듭니다.
            - `level=2~`: 2~9수준의 제목만 목차로 만듭니다.
            - `level=~4`: 1~4수준의 제목만 목차로 만듭니다.
            - `level=2~4`: 2~4수준의 제목만 목차로 만듭니다.
        - 하나의 문서에서 `table of contents` 태그는 여러번 쓸 수 있고, 매번 다른 `level` 옵션을 줄 수도 있습니다.
        - **주의💥**: 만약 `level`을 생략하면 파서가 인식하지 못합니다.
        - **주의💥**: 목차 태그는 자동으로 현재 키워드를 `common`으로 변경합니다. 그래서 목차 태그 또한 암묵적으로 `common`에 속합니다.
    2. **`no-emoji` 옵션**
        - 드문 경우지만 제목에는 이모티콘을 넣으면서 목차에서는 이모티콘을 지우고 싶을 때가 있습니다.😱 만약 당신이 이와 같은 상황이라면, 아래와 같이 `no-emoji` 옵션을 적용하세요.😎

        ```markdown
        <!-- [[ multilingual toc: level=2~3 no-emoji ]] -->
        ```

## 기여하기

번역, 단순한 개선, 버그 제보 등 어떠한 것이라도 소중히 받습니다.

> 특히 이 `README.md` 문서를 여기에 없는 다른 언어로 번역해주신다면 매우 감사드립니다.

### Contributors

> 기여자 명단은 영어로만 제공됩니다.

- [Francis Piérot](https://github.com/bkg2018) - French translation ([#1](https://github.com/ryul1206/multilingual-markdown/pull/1))
