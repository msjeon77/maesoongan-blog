# 매순간 블로그 (maesoongan.com)

Hugo로 만든 정적 블로그예요. 글은 마크다운으로 쓰고, GitHub에 올리면 Cloudflare Pages가 자동으로 사이트에 반영해요.

## 폴더 구조

```
hugo.toml              사이트 설정 (제목, 소개 문장, 메뉴, 댓글/통계)
content/
  _index.md            메인 페이지
  about.md             소개 페이지
  posts/<글-주소>/      글 하나 = 폴더 하나 (index.md + 사진)
  categories/<이름>/    카테고리 설명
layouts/               화면 틀 (HTML)
assets/css/main.css    디자인
static/                그대로 복사되는 파일 (favicon 등)
archetypes/posts.md    새 글 머리말 템플릿
```

## 1. 내 컴퓨터에 Hugo 설치 (Windows)

PowerShell에서:

```powershell
winget install Hugo.Hugo.Extended
hugo version
```

`v0.152` 이상이면 돼요.

## 2. 미리 보기

```powershell
cd maesoongan-blog
hugo server -D
```

브라우저에서 http://localhost:1313 을 열어요. 파일을 저장하면 바로 반영돼요.

## 3. 새 글 쓰기

```powershell
hugo new content posts/corridor-previz/index.md
```

만들어진 `index.md`에 글을 쓰고, 다 쓰면 `draft: true`를 지워요. 사진은 같은 폴더에 넣고 `![설명](사진.jpg)`로 불러요.

- 날짜(`date`)가 미래인 글은 그 시각이 지나고 다음 배포 때 올라가요.
- 예시 글 `content/posts/how-to-write`는 읽고 나서 지워도 돼요.

## 4. 내 컴퓨터로 가져오기와 올리기

저장소는 https://github.com/msjeon77/maesoongan-blog 에 있어요. 처음 한 번 내 컴퓨터로 가져와요.

```powershell
git clone https://github.com/msjeon77/maesoongan-blog.git
```

글을 쓰거나 고친 뒤에는 이렇게 올려요. 올리면 Cloudflare Pages가 1분 안에 사이트에 반영해요.

```powershell
git add .
git commit -m "새 글: 복도 프리비즈"
git push
```

GitHub Desktop을 쓰면 "Clone a repository"로 가져오고, Commit과 Push 버튼으로 올리면 돼요. 짧은 수정은 GitHub 웹에서 파일을 열고 연필 버튼으로 바로 고쳐도 돼요.

## 5. Cloudflare Pages 연결

1. Cloudflare 대시보드 → **Workers & Pages** → **Create** → **Pages** → **Connect to Git** → 저장소 선택
2. 빌드 설정
   - Framework preset: **Hugo**
   - Build command: `hugo --gc --minify`
   - Build output directory: `public`
   - Environment variables: `HUGO_VERSION` = `0.152.2`
3. **Save and Deploy** → 1분쯤 뒤 `<프로젝트>.pages.dev` 주소로 열려요.

## 6. maesoongan.com 연결

1. 도메인이 Cloudflare에 없다면 먼저 Cloudflare에 사이트를 추가하고, 도메인 구입처(가비아 등)에서 네임서버를 Cloudflare가 알려준 두 개로 바꿔요. (반영까지 몇 분~하루)
2. Pages 프로젝트 → **Custom domains** → `maesoongan.com` 추가 → 안내대로 확인. `www.maesoongan.com`도 추가해 두면 좋아요.
3. HTTPS 인증서는 자동으로 붙어요.

## 7. 켜 두면 좋은 것 (hugo.toml)

- **방문 통계**: Cloudflare → Web Analytics → 사이트 추가 → 토큰을 `cfAnalyticsToken`에 넣기
- **댓글**: 저장소를 Public으로 두고 Discussions를 켠 뒤, https://giscus.app 에서 나온 값을 `[params.giscus]`에 넣기
- **소개 문장**: `description`(메인 큰 제목), `intro`(그 아래 한 줄)
- **검색 노출**: Google Search Console과 네이버 서치어드바이저에 사이트 등록 후 `https://maesoongan.com/sitemap.xml` 제출
