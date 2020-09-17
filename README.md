# wooahan_tech_learning
우아한 테크러닝 3기 강의내용 정리
# Typescript

redux는 react에 국한된 것이 아니므로, 직접 subscribe 하는 함수를 만들어야 한다!

→ 이걸 라이브러리로 만들어 놓은 것이 `"react-redux"`

```jsx
render(
	<Provider store={store}>
		<App />
	<Provider />,
	rootElement
);
```

(리듀서)

reducer/index.ts

```jsx
import { getType, ActionType } from "typesafe-actions"; // action type 유용하게 쓰게 해줌

export default(
	state: StoreState = initializeState,
	action: ActionType<typeof Actions>
) => {
	switch (action.type) {
	}
}
```

- `getType`은 `ActionType`에서 설정한 action type만 뽑아준다.

(액션)

action/index.ts

```jsx
import { createAction } from "typesafe-actions";

export const startMonitoring = createAction(
	"@command/monitoring/start",
	resolve => {
		return () => resolve();
	}
);
```

→ @는 그저 알아보기 쉽게 하기 위한 장식임! 만약 비동기 액션의 경우 $로 표기하던지의 나름대로 규칙을 만들어서 사용할 수도 있다!

- action type 선언, action creator 작성 및 payload 설정까지 한번에 해주는 편리한 친구임!
- 여담으로, `Redux-Toolkit`도 매우 편리하다! (action, reducer를 한번에 만들어 관리 가능)

index.tsx

```jsx
import rootSaga from "./sagas"; // 미들웨어임! 제너레이터 떠올리기

```

index.ts

```jsx
import { fork, all, take, race, delay, put } from "redux-saga/effects" // saga 헬퍼

function* monitoringWorkflow() {
	while(true){
		yield take(getType(Actions.startMonitoring)); 
		// take: action하나 줄테니, 이 action이 오면 yield 해줘!

		let loop = true;

		while(loop) {
			yield all([ // all: 제너레이터 밖으로 나왔을 때, next를 해야 다시 들어올것임. 이때 action 여러개를 받아올 때 사용
				put({ type: getType(Action.fetchSuccess) }), // put: action을 dispatch 해줌
				put({ type: getType(Action.fetchFailure) }),
			])
		}

		const { stopped } = yield race({
			waitting: delay(200),
			stopped: take(getType(Actions.stopMonitoring))
			// take: 이 action을 기다려줘
		});
		// race: 여러 객체들 중 가장 먼저 들어오는 객체를 stopped에 담는다(경주와 비슷! 가장 먼저 응답오는 친구를 반환)
	}

	if (stoped) {
		loop = false;
	}
} 

export default function* () {
	yield fork(monitoringWorkflow); // next() 호출하면 다시 함수로 돌아가는 상태에서 멈춤!(fork)
}
```

`generator` 떠올리기! 필요할 때 함수에서 나왔다가 들어갔다 할 수 있는 특별한 친구임!

- 제네레이터 복습

fork, all, take, ... 얘네는 객체임!!(effects, 또는 saga helper)

- 녹화본 42분대에 로그인으로 saga-flow 설명해줌 이거 지림!!
- 안쪽과 바깥쪽이 핑퐁할 수 있다!!! (함수의)
