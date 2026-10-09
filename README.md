# 오늘의 할 일

대표님 개인 할 일 사이트. 직장/집 두 목록, 중요도 A~D, 완료 기록, 날짜별 화면.

## 날짜 (2026-10-09)

- 할 일마다 날짜(`date`, `YYYY-MM-DD`, 서울 기준). 그냥 넣으면 **보고 있는 날짜**(처음 열면 오늘).
- 맨 위 「◀ 10월 9일 (금) ▶ 오늘」: 날짜를 누르면 달력, 「오늘」로 복귀. 목록·진행률·개수는 그 날 기준.
- **오늘 화면에서만** 「밀린 일」: 오늘보다 앞 날짜(또는 날짜 없음)인데 안 끝낸 일. 체크하면 완료(날짜는 원래 날짜 그대로).
- 입력칸 옆 달력 단추로 다른 날짜 지정(넣고 나면 보고 있는 날짜로 되돌아감). 할 일마다 달력 단추로 날짜 옮기기.
- 「완료한 일 비우기」·「전체 초기화」는 보고 있는 날짜의 그 목록만.
- 자정이 지나면(서울) 오늘이 바뀌고 다시 그린다.

- 주소: https://dragon2x.github.io/to-do-list/
- 저장: Firebase 프로젝트 `neo-todo-dragon2x` 의 Firestore (서울 리전)
  - `todos/{id}` 할 일 한 건 = 문서 한 건 `{ id, text, done, priority, category, createdAt, completedAt, date }`. 필드 목록은 `index.html` FIELDS/clean·`할일-연동\store.js`·`firestore.rules` 가 같아야 한다.
  - `history/{id}` 완료 기록(완료하면 쓰고, 완료 취소하면 지움. 할 일을 지워도 기록은 남음)
- 로그인: 구글 계정. `firestore.rules` 가 대표님 계정만 읽기·쓰기를 허용한다(다른 로그인 방식은 꺼 둠).
- 여러 기기 동기화: Firestore 실시간 구독. 오프라인에서 바꾼 것은 기기에 보관했다가 연결되면 보낸다.

## 파일

| 파일 | 내용 |
|---|---|
| `index.html` | 사이트 전체(한 파일) |
| `firestore.rules` | 보안 규칙 |
| `firestore.deny.rules` | 비상용 「모두 거부」 규칙 |
| `firebase.json`, `.firebaserc` | 규칙 배포 설정 |

## 배포

- 사이트: 이 저장소 `main` 에 올리면 GitHub Pages 가 반영한다.
- 규칙: `firebase deploy --only firestore:rules --project neo-todo-dragon2x`
- 비상 잠금: `firestore.deny.rules` 를 `firestore.rules` 로 복사해 배포.

웹 설정값(apiKey 등)은 공개돼도 되는 값이다. 접근 제어는 보안 규칙이 한다.

## 이력

- 2026-10-01 ukey1358-cmyk/to-do-list(구글 시트 동기화)에서 옮김. 화면은 그대로, 저장만 Firestore 로.
- 2026-10-09 날짜 기능(날짜별 화면 + 밀린 일). 규칙에 `date`(선택) 추가.
