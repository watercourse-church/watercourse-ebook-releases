# 물줄기교회 좋은 씨앗 — 전자책 배포

조춘숙 목사 설교집 시리즈의 **완성된 전자책(EPUB·PDF)** 을 내려받는 곳입니다.
원고와 제작 도구는 별도의 비공개 저장소에서 관리하고, 이 저장소에는 **배포 산출물만** 올라옵니다.

> 이 책들은 **전도용이며 판매하지 않습니다.**

## 내려받기

[**릴리스 목록**](../../releases) 에서 원하는 책을 고르면 됩니다.
릴리스 하나가 책 한 권이고, 태그는 `<번호>-v<버전>` 형식입니다 (예: `17-v1.0.0` = 아모스 강해 1.0.0).

각 릴리스에는 두 파일이 붙습니다.

| 파일 | 용도 |
|---|---|
| `<번호>-<이름>-v<버전>.epub` | 전자책 단말기·앱 (리디북스, 애플 북스, 구글 플레이 북스 등) |
| `<번호>-<이름>-v<버전>.pdf` | 인쇄하거나 화면에서 그대로 볼 때 |

## 홈페이지에 붙이기 — `books.json`

책이 새로 나올 때마다 홈페이지를 고치지 않아도 되도록, 전체 목록과 최신 다운로드 링크를
`books.json` 하나에 모아 둡니다. 발행할 때마다 자동으로 갱신됩니다.

```
https://raw.githubusercontent.com/watercourse-church/watercourse-ebook-releases/main/books.json
```

### 형식

```json
{
  "generated": "2026-08-03",
  "repo": "watercourse-church/watercourse-ebook-releases",
  "books": [
    {
      "id": "17",
      "slug": "17. 아모스",
      "title": "아모스 강해",
      "bibleBook": "아모스",
      "author": "조춘숙 목사",
      "publisher": "물줄기교회 출판부",
      "edition": "제1판",
      "version": "1.0.0",
      "releaseDate": "2024-02",
      "description": "아모스 설교집 (제17권).",
      "tags": ["기독교", "설교", "아모스", "강해"],
      "tag": "17-v1.0.0",
      "downloads": {
        "epub": "https://github.com/.../releases/download/17-v1.0.0/17-amos-v1.0.0.epub",
        "pdf":  "https://github.com/.../releases/download/17-v1.0.0/17-amos-v1.0.0.pdf"
      }
    }
  ]
}
```

`books` 는 번호 순으로 정렬되어 있습니다. `downloads` 에는 그 책의 **최신 버전** 링크가 들어갑니다
(과거 버전은 릴리스 목록에 그대로 남습니다).

### 필드

| 필드 | 뜻 |
|---|---|
| `id` | 시리즈 번호. 번호가 없는 책은 별칭(`ark` 등) |
| `title` | **책 제목** — 인쇄본 표지의 큰 글자 |
| `bibleBook` | 이 책이 다루는 **성경책**. 특정 성경책 강해가 아니면 빈 문자열 |
| `author` | 지은이 + 직함 |
| `edition` / `version` | 판 / 전자책 버전 |
| `releaseDate` | 인쇄본 발행 연월 |
| `description` | 책 소개 |
| `tag` | 릴리스 태그 |
| `downloads` | `epub` / `pdf` 내려받기 주소 |

`title` 과 `bibleBook` 은 다릅니다. 예를 들어 12번은 제목이 `너희가 섬길 자를 오늘 택하라`,
다루는 성경책이 `여호수아` 입니다. 표지도 제목을 크게, 성경책을 작게 적습니다.

### 예시

```html
<div id="books"></div>
<script>
const URL = "https://raw.githubusercontent.com/watercourse-church/watercourse-ebook-releases/main/books.json";

fetch(URL)
  .then(r => r.json())
  .then(({ books }) => {
    document.getElementById("books").innerHTML = books.map(b => `
      <article>
        <h3>${b.title}</h3>
        <p>${b.author} · ${b.edition} · ${b.releaseDate}</p>
        <p>${b.description ?? ""}</p>
        <p>
          ${b.downloads.epub ? `<a href="${b.downloads.epub}" download>EPUB 내려받기</a>` : ""}
          ${b.downloads.pdf  ? `<a href="${b.downloads.pdf}"  download>PDF 내려받기</a>`  : ""}
        </p>
      </article>
    `).join("");
  });
</script>
```

## 문의

대한예수교장로회 물줄기교회 출판부
서울 강서구 수명로 68-27 웨스트엔드 2차 문화센터 4층 · 02-6403-3221
