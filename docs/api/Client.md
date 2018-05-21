# Client

`boardgame.io` 클라이언트를 생성합니다. 클라이언트 어플리케이션의 시작점입니다.

The `Board` component will receive the following as `props`:

1. `G`: 게임의 상태입니다.

2. `ctx`: 게임의 메타데이터입니다.

3. `moves`: An object containing functions to dispatch various
   moves that you have defined. The functions are named after the
   moves you created using [Game()](/api/Game.md). Each function
   can take any number of arguments, and they are passed to the
   move function after `G` and `ctx`.

4. `events`: An object containing functions to dispatch various
   game events like `endTurn` and `endPhase`.

5. `playerID`: The player ID associated with the client.

6. `isActive`: `true` if the client is able to currently make
   a move or interact with the game.

7. `isMultiplayer`: `true` if it is a multiplayer game.

8. `isConnected`: `true` if connection to the server is active.

9. `enhancer`: An optional Redux store enhancer, passed along to
   the internals store. See the [Debugging](debugging.md) section
   for more details.

### 전달인자

1. obj(_object_): 위에 나와 있는 게임 설정을 포함하는 객체.

### 반환 값

(`client`): 앱을 실행하기 위한 React 컴포넌트.

컴포넌트는 다음의 `props`를 지원합니다:

1. `gameID`: 특정한 게임에 연결합니다. (멀티플레이어).

2. `playerID`: 플레이어와 클라이언트를 연결합니다 (멀티플레이어).

3. `debug`: 디버그 UI를 비활성화 하려면 false로 지정하십시오.

### 사용법

```js
import { Client } from 'boardgame.io/react';

const App = Client({
  // Game()의 반환 값.
  game: game,

  // 플레이어의 수.
  numPlayers: 2,

  // 당신의 게임보드를 표현하는 React 컴포넌트.
  board: Board,

  // Set to true to enable sending move updates to the
  // server via WebSockets. Can also be set to
  // { server: 'hostname:port' }
  // to specify a socket server that's different from
  // the one that served up the page.
  multiplayer: false,

  // 디버그 UI를 비활성화 하려면 false로 지정하십시오.
  debug: true,
});

ReactDOM.render(<App />, document.getElementById('app'));
```

The returned element can also take an optional `gameID`
argument when used in multiplayer mode to connect to a
specific game (as opposed to the default one).

```
<App gameID="my-game-id" />
```
