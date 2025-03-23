## 이벤트

> * 브라우저는 처리해야 할 특정 사건이 발생하면 이를 감지하여 이벤트를 발생
> * 이벤트가 발생했을때 호출될 함수를 ***이벤트 핸들러***라고 한다.

## 이벤트 타입

### 마우스 이벤트
> * click: 마우스 버튼 클릭
> * dblclick: 마우스 버튼 더블 클릭
> * mousedown: 마우스 버튼 누르고 있을때
> * mouseup: 누르고 있던 마우스 버튼을 놓았을 때
> * mousemove: 마우스 커서를 움직였을때
> * mouseenter: 마우스 커서를 HTML 요소 안으로 이동했을때 (버블링x)
> * mouseover: 마우스 커서를 HTML 요소 안으로 이동했을때 (버블링O)
> * mouseleave: 마우스 커서를 HTML 요소 밖으로 이동했을대(버블링X)
> * mouseout: 마우스 커서를 HTML 요소 밖으로 이동했을때(버블링O)

### 키보드 이벤트
> * keydown: 모든 키를 눌렀을 때 발생
>   * control, option, shift, tab, delete, enter, 방향 키와 문자, 숫자, 특수 문자 키를 눌렀을때 발생
>   * 단 문자, 숫자, 특수 문자, enter키를 눌렀을땐 연속 발생, 그 외의 키는 한번만 발생
> * keyup: 누르고 있던 키를 놓았을 때 한번만 발생
>   * keydown 이벤트와 마찬가지로 control, option, shift, tab, delete, enter, 방향키와 문자 숫자, 특수 문자 키를 놓았을때 발생

### 포커스 이벤트
>* focus: HTML 요소가 포커스를 받았을 때(버블링X)
>* blur: HTML 요소가 포커스를 잃었을 때(버블링X)
>* focusin: HTML 요소가 포커스를 받았을 때(버블링O)
>* focusout: HTML 요소가 포커스를 잃었을 때(버블링O)

