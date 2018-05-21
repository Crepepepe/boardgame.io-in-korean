# Boardgame.io 한글 문서

<p align="center">
  <img src="https://raw.githubusercontent.com/google/boardgame.io/master/docs/logo.svg?sanitize=true" alt="boardgame.io" />
</p>

<p align="center">
<a href="https://www.npmjs.com/package/boardgame.io"><img src="https://badge.fury.io/js/boardgame.io.svg" alt="npm version" /></a>
<a href="https://travis-ci.org/google/boardgame.io"><img src="https://img.shields.io/travis/google/boardgame.io/master.svg" alt="Travis" /></a>
<a href="https://coveralls.io/github/google/boardgame.io?branch=master"><img src="https://img.shields.io/coveralls/google/boardgame.io.svg" alt="Coveralls" /></a>
<a href="https://gitter.im/boardgame-io"><img src="https://badges.gitter.im/boardgame-io.svg" alt="Gitter" /></a>
</p>

<p align="center">
  <strong>전체 문서: <a href="https://google.github.io/boardgame.io">링크</a></strong>
</p>

The goal of this framework is to allow a game author to
essentially translate the rules of a game into a series of
simple functions that describe how the game state changes
when a particular move is made, and the framework takes
care of the rest. You will not need to write any
networking or backend code.

## 기능

* **상태 관리**: Game state is managed seamlessly across clients, server and storage automatically.
* **크로스-플랫폼 멀티플레이어**: 모든 클라이언트들은 (Web / Android / iOS) 실시간으로 같은 게임에 연결되고 동기화됩니다.
* **UI Agnostic**: React, React Native 또는 일반 JS를 위한 클라이언트 API.
* **게임 Phases**: with different game rules (including custom turn orders) per phase.
* **비밀 상태**: Secret information (like the opponent's cards) can be hidden from the client.
* **프로토타이핑**: Debugging interface to simulate moves even before you render the game.
* **로그**: Game logs with the ability to time travel (viewing the board at an earlier state).
* **컴포넌트 도구**: Components for hex grids, cards, tokens (React only at the moment).

## 사용법

### 설치

```
$ npm install --save boardgame.io
```

### 해당 리포지토리에서 예제 실행

```
$ npm install
$ npm run examples
```

## 변경사항

[변경사항](docs/CHANGELOG.md)을 참고하세요.

## 기여하기

기여 [가이드라인](CONTRIBUTING.md)을 참고하세요.

## Disclaimer

이건 구글의 공식 제품이 아닙니다.
이것은 구글러의 취미 프로젝트이며 커뮤니티의 기여자들로 부터 도움을 받습니다.
