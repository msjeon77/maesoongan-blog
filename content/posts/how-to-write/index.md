---
title: "이 블로그에 글 쓰는 법"
slug: "how-to-write"
date: 2026-10-02T09:00:00+09:00
description: "새 글 만들기부터 사진 넣기, 올리기까지. 다 읽었으면 지워도 되는 안내 글이에요."
categories: ["만드는 것들"]
tags: ["블로그", "hugo"]
toc: true
---

이 글은 블로그를 처음 받았을 때 들어 있는 **안내용 예시 글**이에요. 읽고 나서 `content/posts/how-to-write` 폴더를 통째로 지우면 사라져요.

## 새 글 만들기

글 하나는 `content/posts/` 아래의 **폴더 하나**예요. 폴더 안에 `index.md`와 그 글에 쓰는 사진을 같이 넣어요.

```text
content/posts/
└── corridor-previz/
    ├── index.md
    ├── cover.jpg
    └── shot-01.png
```

터미널에서 아래 명령을 쓰면 폴더와 기본 머리말이 자동으로 만들어져요.

```bash
hugo new content posts/corridor-previz/index.md
```

폴더 이름(`corridor-previz`)이 그대로 주소가 돼요. 한글 주소는 공유할 때 길게 깨져 보이니 영문 소문자와 `-`로 짓는 걸 권해요.

## 머리말 채우기

`index.md` 맨 위 `---` 사이가 머리말이에요.

| 항목 | 뜻 |
| --- | --- |
| title | 글 제목 |
| date | 글 날짜. 목록의 큰 날짜 숫자가 여기서 나와요 |
| description | 목록과 검색 결과에 보이는 한 줄 요약 |
| categories | `영상과 3D`, `만드는 것들`, `매순간 기록` 중 하나 |
| tags | 자유롭게 여러 개 |
| cover | 글 맨 위 큰 사진 (폴더 안 파일 이름) |
| toc | `true`면 목차 표시 |
| draft | `true`인 동안은 사이트에 올라가지 않아요 |

## 본문 쓰기

마크다운 문법을 그대로 써요.

- `## 소제목`, `### 작은 소제목`
- `**굵게**`, `[링크](https://maesoongan.com)`
- 사진: `![설명](shot-01.png)`
- 인용: 줄 앞에 `>`

영상은 HTML을 바로 넣을 수 있어요. 렌더 결과를 보여줄 때 편해요.

```html
<video src="render.mp4" controls muted playsinline></video>
```

## 내 컴퓨터에서 미리 보기

블로그 폴더에서 아래 명령을 실행하고 브라우저로 `http://localhost:1313`을 열면, 저장할 때마다 바로 바뀌는 화면을 볼 수 있어요. `-D`를 붙이면 `draft: true`인 글도 보여요.

```bash
hugo server -D
```

## 올리기

GitHub에 올리면 Cloudflare Pages가 1분 안에 maesoongan.com에 반영해요.

```bash
git add .
git commit -m "새 글: 복도 프리비즈"
git push
```

GitHub Desktop을 쓰면 명령어 없이 버튼으로도 할 수 있어요.
