# Game

초기 게임 상태 및 행동에 의해 구현된 새로운 게임을 생성합니다.
`G`를 유지하기 위해 행동들은 [Redux](http://redux.js.org/docs/basics/Reducers.html)
reducer로 전환됩니다.

### 전달인자

1. `obj` (_object_): 다음을 포함하는 객체

  * `name` (_string_): 게임의 이름입니다.
  * `setup` (_object_): `G`를 초기화하여 반환하는 함수입니다.
  * `moves` (_object_): 키들은 행동의 이름이고,
    값들은 행동이 발생하고 난 후 새로운 `G` 값을 반환하는 순수한 함수입니다.
  * `playerView` (_function_): 주어진 유저를 위해 커스텀마이즈된 `G`를 반환합니다.
    자세한 정보는 [Secret State](/secret-state)를 참고하세요.
  * `seed` (_string_): PRNG를 위한 시드입니다.
  * `flow` (_object_): 게임의 흐름을 커스텀마이즈하기위한 전달인자입니다.
    자세한 정보는 [Phases](/phases)를 참고하세요.
  * `flow.endGameIf` (_function_): _(G, ctx) => {}_
    이 함수가 어떠한 것이라도 반환하면 게임은 자동으로 종료됩니다.
    (행동할때 마다 확인합니다).
    반환 값은 `ctx.gameover`에서 얻을 수 있습니다.
  * `flow.endTurnIf` (_function_): _(G, ctx) => boolean_
    이 함수가 true를 반환하면 자동으로 턴이 종료됩니다
    (행동할때 마다 확인합니다).
  * `flow.onTurnBegin` (_function_): _(G, ctx) => G_
    턴이 시작될 때 실행될 코드입니다.
  * `flow.onTurnEnd` (_function_): _(G, ctx) => G_
    턴이 종료될 때 실행될 코드입니다.
  * `flow.onMove` (_function_): _(G, ctx, { type: 'moveName', args: [] }) => G_
    행동이 종료될 때 실행될 코드입니다.
  * `flow.movesPerTurn` (_number_): 특정 횟수의 행동이 이루어지면 자동을 턴을 종료합니다.
  * `flow.undoableMoves` (_array_): 행동을 번복하거나 다시 할 수 있도록 합니다.
  만약 모든 행동이 되돌릴수 없다면 `undefined`로 두십시오.
  * `flow.phases` (_array_): 게임 페이즈의 추가적인 목록.
    자세한 정보는 [Phases](/phases)를 참고하세요.

### 반환 값

(`game`): 다음을 포함하는 객체

1. `setup`: 전달인자에 있던 `setup`과 동일합니다.
2. `moveNames`: 게임의 행동들의 이름입니다.
3. `processMove`: `G`를 유지하기 위한 reducer입니다.
4. `playerView`: 전달된 `playerView` 함수입니다.
5. `flow`: `obj.flow`로부터 파생되어 `ctx`를 유지하기 위한 reducer를 포함하는 객체입니다.

### 사용법

#### 간단한 게임

```js
import { Game } from `boardgame.io/core';

const game = Game({
  setup: (ctx) => {
    const G = {...};
    return G;
  },

  moves: {
    moveWithoutArgs(G, ctx) {
      return {...G, ...};
    },

    moveWithArgs(G, ctx, arg0, arg1) {
      return {...G, ...}
    }
  }
});
```

#### 승리 조건이 있는 게임

```js
import { Game } from 'boardgame.io/core';

const game = Game({
  setup: (ctx) => {
    ...
  },

  moves: {
    ...
  },

  flow: {
    endGameIf: (G, ctx) => {
      if (IsWinner(G, ctx.currentPlayer)) {
        return ctx.currentPlayer;
      }
    },
  }
});
```

#### Phases가 있는 게임

```js
import { Game } from 'boardgame.io/core';

const game = Game({
  setup: (ctx) => {
    ...
  },

  moves: {
    ...
  },

  flow: {
    phases: [
      {
        name: 'A',
        endGameIf: ...
        endTurnIf: ...
        onTurnBegin: ...
        onTurnEnd: ...
        onPhaseBegin: ...
        onPhaseEnd: ...
        allowedMoves: ...
        ...
      },
      {
        name: 'B',
        endGameIf: ...
        endTurnIf: ...
        onTurnBegin: ...
        onTurnEnd: ...
        onPhaseBegin: ...
        onPhaseEnd: ...
        allowedMoves: ...
        ...
      },
    ]
  }
});
```
