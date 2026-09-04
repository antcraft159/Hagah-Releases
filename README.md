# Hagah-Releases

설교 메모 앱 **Hagah** 가 읽는 파일을 두는 곳이다.

## notices.json — 앱 안에 뜨는 공지

앱은 뜰 때마다 아래 주소를 받아 읽는다.

    https://raw.githubusercontent.com/antcraft159/Hagah-Releases/main/notices.json

고치는 방법은 이 파일을 고쳐서 push 하는 것뿐이다. 서버도 DB 도 없다.

```json
{
  "schemaVersion": 1,
  "notices": [
    {
      "id": "2026-09-04-hello",
      "title": "제목",
      "content": "본문. 줄바꿈은 \n 이다.\n주소를 적으면 눌리는 링크가 된다: [보이는 말](https://example.com)",
      "date": "2026-09-04",
      "important": false,
      "minVersion": "0.2.0",
      "maxVersion": "0.9.0"
    }
  ]
}
```

| 칸 | 뜻 |
|---|---|
| `id` | 읽음 처리의 기준. **한 번 정하면 절대 바꾸지 않는다.** 바꾸면 이미 읽은 사람에게 새 공지로 다시 뜬다 |
| `title` | 제목. 없으면 그 공지는 통째로 버려진다 |
| `content` | 본문. `\n` 으로 줄을 나눈다. `[말](https://…)` 와 맨 주소가 링크로 그려진다 |
| `date` | `yyyy-MM-dd`. 최신순 정렬에 쓴다 |
| `important` | `true` 면 목록 맨 위로 가고, 안 읽었으면 앱 시작 때 공지 창이 저절로 열린다 |
| `minVersion` · `maxVersion` | 이 공지를 볼 앱 판의 범위. 비우면 제한 없음 |

### 손대기 전에 알아 둘 것
- **raw 주소는 CDN 캐시가 5분이다.** push 해도 곧바로 반영되지 않는다(앱이 캐시 우회 값을 붙이지만
  GitHub 쪽 반영에도 몇 초가 걸린다). 긴급 공지용으로는 쓸 수 없다.
- **저장소는 반드시 공개(public)** 여야 한다. 비공개로 바꾸면 토큰이 필요해져 이 방식이 통째로 무너진다.
- **쉼표 하나만 틀려도** 앱은 그 파일을 버리고 마지막으로 받아 둔 것을 보여 준다. 올리기 전에 JSON 을 한 번 검사할 것.
- 공지를 지우면 그 공지는 앱에서 사라진다. 읽음 기록은 사용자 컴퓨터에 남는다.
