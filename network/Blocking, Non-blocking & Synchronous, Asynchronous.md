## Blocking / Non-Blocking

상위작업에서 하위작업 호출 시, 상위작업이 하위작업이 처리될 때 대기하는지에 대한 것이다.

### Blocking

하위작업이 상위작업에게 제어권을 넘기지 않는다. 제어권은 작업이 완료될 때 넘겨준다.
따라서 상위작업은 대기상태에 있게된다.

### Non-Blocking

작업 호출된 후 하위작업이 상위작업에게 바로 제어권을 넘겨준다. 상위작업은 하위작업이 처리될 동안 다른 일을 수행할 수 있다.

## Synchronous / Asynchronous

상위작업에서 하위작업 호출 시, 하위작업의 수행 결과 및 종료를 고려하는지에 대한 것이다.

### Synchronous

하위작업의 수행 결과 및 종료를 고려한다. 따라서 하위작업이 종료되야지 다음 작업을 수행한다. 때문에 작업 순서를 예측하기쉽다.

### Asynchronous

하위작업의 수행 결과 및 종료를 고려하지않는다. 따라서 하위작업이 종료되지않아도 다음 작업을 수행될 수 있다. 때문에 작업이 동시에 처리될 수 있다.
