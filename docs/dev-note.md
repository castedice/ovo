# One Versus One development note

## 2024-04-03

### Development environment setup

1. npx create-next-app@latest ovo
2. git init
3. git add .
4. git commit -m "Initial commit"

### 브레인 스토밍

- 계정
  - 슬랙 SSO 로그인
  - 게임 별 정보(주 캐릭터 등)
  - 슬랙 채널 연동(주간 랭킹)
- 대전
  - 대전 결과 기록
  - 대전 결과 조회
  - 대전 결과 바탕으로 elo 점수 계산
  - elo 점수 바탕으로 랭킹 갱신
  - 슬랙을 통한 대전 신청
- 대회
  - 대회 개설
  - 대회 참가 신청
  - 자동 대진 완성 및 시간 조율
  - 대회 결과 기록
- 모바일
- 확장성
  - 철권 외의 게임도 지원 가능

### 유저 스토리

- 유저는 슬랙 SSO 로그인을 통해 계정을 생성한다.
- 유저는 게임 별로 주 캐릭터를 설정할 수 있다.
- 유저는 슬랙 채널을 통해 주마다 업데이트되는 랭킹을 확인할 수 있다.
- 유저는 슬랙을 통해 다른 유저에게 대전을 신청할 수 있다.
- 유저는 대전 결과를 기록할 수 있다.
- 유저는 대전 결과를 조회할 수 있다.
- 유저는 대전 결과를 바탕으로 자신의 elo 점수를 확인할 수 있다.
- 유저는 대전 결과를 바탕으로 랭킹을 확인할 수 있다.
- 유저는 대회를 개설할 수 있다.
- 유저는 대회에 참가할 수 있다.
- 유저는 대회 결과를 기록할 수 있다.
- 유저는 대회 결과를 조회할 수 있다.
- 유저는 대회 대전 일정을 잡을 수 있다.
- 유저는 모바일에서도 서비스를 이용할 수 있다.
- 유저는 철권 외의 게임에서도 서비스를 이용할 수 있다.

### 화면 구성

- 메인페이지
  - 로그인
    - 슬랙 SSO 로그인
  - 헤더
    - 사이드바
    - 로고
    - 서비스 이름
    - 게임 선택
    - 유저 정보
    - 로그아웃
  - 사이드바
    - 랭킹
    - 대전
    - 대회
    - 설정
- 랭킹
  - 일간, 주간, 월간, 누적 랭킹
  - 유저 조회
- 대전
  - 최근 대전 결과
  - 대전 검색
  - 대전 기록
  - 대전 신청
- 대회
  - 대회 목록
  - 대회 개설
  - 대회 참가
  - 대회 경기 신청
  - 대회 결과 등록
- 유저 정보
  - 설정
  - 통계

### 데이터 모델링

- User
  - id
  - slack_id
  - name
  - nickname
  - created_at
- Game
  - id
  - name
- GameAttribute
  - id
  - game_id
  - key
  - value
- Game-User
  - id
  - user_id
  - game_id
  - main_character
- Match
  - id
  - game_id
  - player1_id
  - player2_id
  - winner_id
  - description
  - created_at
- Match-User
  - id
  - user_id
  - match_id
  - description
- Elo
  - id
  - user_id
  - game_id
  - elo
- Ranking
  - id
  - user_id
  - game_id
  - ranking
  - elo
  - created_at
  - daily_change
  - weekly_change
  - monthly_change
- Tournament
  - id
  - game_id
  - name
  - start_at
  - end_at
- Tournament-User
  - id
  - tournament_id
  - user_id
- Tournament-Match
  - id
  - tournament_id
  - match_id
