# 키친포스

## 퀵 스타트

```sh
cd docker
docker compose -p kitchenpos up -d
```

## 요구 사항
> `<상태>`는 이렇게 표시된다.
> ***엔티티***는 이렇게 표시된다.

- 모든 이름은 비어있으면 안 된다.
- ***상품***
    - [ ] ***상품***은 이름을 가지고 있고, 이름에 비속어가 포함되지 않아야 한다.
        - https://www.purgomalum.com/service/containsprofanity
    - [ ] ***상품***은 가격을 가지고 있고, 가격은 음수일 수 없다.
    - [ ] ***상품***의 가격을 바꿀 수 있다. 이때 해당 ***상품***이 속한 ***메뉴***의 총 가격이 ***상품*** 가격의 합보다 커지면, 그 ***메뉴***는 보이지 않게 변경된다.
        - 할인은 인정하지만 할증은 인정하지 않는 모양
    - [ ] 모든 ***상품***의 목록을 조회할 수 있다.
- ***메뉴그룹***
    - [ ] ***메뉴그룹***은 이름을 가지고 있다.
- ***메뉴***
    - [ ] ***메뉴***는 이름을 가지고 있고, 이름에 비속어가 포함되지 않아야 한다.
    - [ ] ***메뉴***는 가격을 가지고 있고, 가격은 음수로 설정할 수 없다.
    - [ ] ***메뉴***는 ***상품***을 하나 이상 가지고 있어야 하며, ***상품***의 수량을 설정할 수 있다.
    - [ ] 특정 ***메뉴그룹***에 무조건 포함되어야 한다.
    - [ ] ***메뉴***를 만들 때, ***상품*** 수량은 음수가 아니어야 하고, ***메뉴*** 가격은 ***메뉴***에 포함된 ***상품***들의 총 가격보다 크지 않아야 한다.
    - [ ] ***메뉴*** 가격을 바꿀 수 있다. 이때 ***메뉴*** 가격은 ***메뉴***에 포함된 ***상품***들의 총 가격보다 크지 않아야 한다.
    - [ ] ***메뉴***는 공개/비공개 설정할 수 있다. 이때, ***메뉴*** 가격이 ***메뉴***에 포함된 ***상품***들의 총 가격보다 크다면 공개할 수 없다.
    - [ ] 모든 ***메뉴***의 목록을 조회할 수 있다.
- ***매장테이블***
    - [ ] ***매장테이블***은 이름을 가지고 있으며, 생성 시 손님 수는 0으로 설정되고 `비워짐` 상태가 된다.
    - [ ] ***매장테이블**은 손님을 앉힐 수 있으며, `차지돰` 상태가 된다.
    - [ ] `차지됨` 상태인 ***매장테이블***만 0 이상의 손님 수를 설정할 수 있다.
    - [ ] ***매장테이블***은 `완료`되지 않은 ***주문***이 있다면 비울 수 없다. 그렇지 않다면, ***매장테이블***을 비울 수 있으며, 손님 수는 0으로 설정되고, `비워짐` 상태가 된다.
    - [ ] 모든 ***매장테이블***의 목록을 조회할 수 있다.
- ***주문***
    - [ ] ***주문***은 `배달`, `포장`, `매장식사` 중 한 종류다.
    - [ ] ***주문***을 생성하면 `대기중` 상태가 된다.
        - [ ] ***주문***은 ***주문세부항목***들을 하나 이상 선택해야 한다.
        - [ ] ***주문세부항목***은 선택한 메뉴, 수량, 가격으로 구성된다.
        - [ ] `매장식사` ***주문***만 음수 수량을 가질 수 있고, 그 외에는 음수(-) 수량을 가지지 않아야 한다.
        - [ ] 비공개된 ***메뉴***가 포함된 ***주문***은 유효하지 않다.
        - [ ] 설정된 ***메뉴*** 금액과 요청한 ***메뉴*** 금액이 같아야 한다.
        - [ ] `배달` ***주문***은 배달 주소가 존재해야 한다.
        - [ ] `매장식사` ***주문***은 차지되지 않은 ***매장테이블*** 하나가 선택되어야 하며, 선택된 ***매장테이블***은 `차지됨` 상태가 된다.
    - [ ] `대기중`  상태인 ***주문***만 접수할 수 있다.
        - [ ] `배달` 주문은 접수 시 배달 요청을 보낸다.
        - [ ] ***주문***을 접수하면 `접수됨` 상태가 된다.
    - [ ] `접수됨`상태인 ***주문***만 제공할 수 있다.
        - [ ] ***주문***을 제공하면 `제공됨` 상태가 된다.
    - [ ] `제공됨` 상태인 `배달` ***주문***만 배달을 시작할 수 있다.
        - [ ] 배달을 시작한 ***주문***은 `배달중` 상태가 된다.
    - [ ] `배달중` 상태인 ***주문***만 배달을 완료할 수 있다. (`배달`주문이 아니어도 됨)
        - [ ] 배달을 완료한 ***주문***은 `배달됨` 상태가 된다.
    - [ ] ***주문***을 완료할 수 있다
        - [ ] `배달`***주문***은 `배달됨` 상태여야 한다.
        - [ ] `포장` 혹은 `매장식사` ***주문***은 `제공됨` 상태여야 한다.
        - [ ] `매장식사`***주문***일 때, 그 ***주문***에서 선택된 ***매장테이블***로 완료되지 않은 주문이 하나도 없다면, 다시 `비워짐` 상태가 되며, 손님 수는 0이 된다.
            - 즉, 아직 제공되지 않은 다른 `매장식사` 주문이 남아 있디면, 완료예정인 주문이 완료된다고 해서 해당 테이블을 비우지는 않는다.
        - [ ] ***주문***이 완료되면 `완료됨` 상태가 된다.

(개별 엔티티를 조회하는 API가 없다...)

## 용어 사전

| 한글명 | 영문명 | 설명 |
| --- | --- | --- |
|  |  |  |

## 모델링
