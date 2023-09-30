# 39_DOM

`HTML 문서의 계층적 구조와 정보를 표현하며 이를 제어할 수 있는 API, 즉 프로퍼티와 메서드를 제공하는 트리 자료구조`

`DOM API(DOM이 제공하는 프로퍼티와 메서드)를 사용하여 노드에 접근하고 HTML의 구조, 내용, 스타일 등을 동적으로 변경하는 방법을 익혀야 한다!`

### 노드(문서, 요소, 어트리뷰트, 텍스트 노드)

- HTML 요소의 어트리뷰트 → 어트리뷰트 노드
- HTML 요소의 텍스트 콘텐츠 → 텍스트 노드
- 트리 자료구조(중첩 관계에 의한 계층적인 부모-자식 관계를 형성하는 비선형 자료구조)
- 노드 객체들로 구성된 트리 자료구조를 DOM이라 한다!
- 모든 노드 객체는 Object, EventTarget, Node 인터페이스를 상속받는다.

### 요소 노드 취득

- document.getElementById → 인수로 전달한 id 어트리뷰트 값을 갖는 하나의 요소 노드를 반환(전달된 id 값을 갖는 HTML 요소가 없으면 null 반환)
- document/getElementsByTagName → 인수로 전달한 태그 이름을 갖는 모든 요소 노드들을 반환(여러 개의 요소 노드 객체를 갖는 DOM 컬렉션 객체인 HTMLCollection 객체 반환. 유사배열 객체이면서 이터러블)
- element.getElementsByTagName → 특정 요소 노드를 통해 호출, 그의 자손 노드 중에서 요소 노드를 탐색하여 반환
- document/getElementsByClassName → 인수로 전달한 class 어트리뷰트 값을 갖는 모든 요소 노드를 반환, 값을 공백으로 구분하여 여러 개 class 지정 가능
- element.getElementsByClassName → 특정 요소 노드의 자손 노드 중에서 요소 노드를 반환
- document/element.querySelector → 인수로 전달한 CSS 선택자를 만족시키는 하나의 요소 노드를 반환
    - 인수로 전달한 CSS 선택자를 만족시키는 요소 노드가 여러 개인 경우 첫 번째 요소 노드만
    - 존재하지 않는 경우 null 반환
    - 문법에 맞지 않는 경우 DOMException 에러
- document/element.querySelectorAll → 인수로 전달한 CSS 선택자를 만족시키는 모든 요소 노드 반환(여러 개의 요소 노드 객체를 갖는 DOM 컬렉션 객체인 NodeList 객체 반환. 유사 배열 객체이면서 이터러블)
- element.matches → 인수로 전달한 CSS 선택자를 통해 특정 요소 노드를 취득할 수 있는지 확인, 불리언 값 반환
- HTMLCollection, NodeList → for…of 문으로 순회 가능, 스프레드 문법과 Array.from 메서드를 사용하여 배열로 변환 가능
- HTMLCollection의 부작용(실시간 노드 객체의 상태 변경을 반영하여 요소 제거 가능성)을 해결하기 위해 NodeList를 반환하는 querySelectorAll 메서드 사용. 예외적으로 childNodes 프로퍼티는 HTMLCollection 객체와 같이 실시간으로 노드 객체의 상태를 변경한다.
- 따라서 HTMLCollection이나 NodeList 객체를 배열로 변환하여 사용하는 것을 권장한다. 배열로 변환하면 배열의 유용한 고차 함수(forEach, map, filter, reduce 등)를 사용할 수 있다.

### 노드 탐색

- 노드 탐색 프로퍼티는 모두 읽기 전용(getter만 존재) 접근자 프로퍼티다.
- 공백 텍스트 노드(스페이스, 탭, 엔터 키 등)
- 자식 노드 탐색
    - Node.childNodes → 요소 노드, 텍스트 노드 모두
    - Element.children → 요소 노드 모두
    - Node.firstChild → 텍스트 노드이거나 요소 노드
    - Node.lastChild → 텍스트 노드이거나 요소 노드
    - Element.firstElementChild → 요소 노드
    - Element.lastElementChild → 요소 노드
- Node.hasChildNodes → 자식 노드 존재 확인, 불리언 반환. 텍스트 노드를 포함하여 자식 노드의 존재를 확인한다. 요소 노드가 존재하는지 확인하려면 children.length 또는 childElementCount 프로퍼티를 사용한다.
- Node.parentNode → 부모 노드 탐색
- 형제 노드 탐색
    - Node.previousSibling → 요소 노드이거나 텍스트 노드
    - Node.nextSibling → 요소 노드이거나 텍스트 노드
    - Element.previousElementSibling → 요소 노드
    - Element.nextElementSibling → 요소 노드
- 노드 정보 취득
    - Node.nodeType → 요소 노드 타입:1, 텍스트 노드 타입: 3, 문서 노드 타입: 9
    - Node.nodeName → 요소 노드: 대문자 태그 이름, 텍스트 노드:#text, 문서 노드:#document
- 요소 노드의 텍스트 조작
    - nodeValue → 노드 객체의 값 반환(텍스트 노드가 아니면 null)
    - textContent → 시작 태그와 종료 태그 사이 내의 콘텐츠 영역(텍스트)를 모두 반환
    - 문자열을 할당하면 요소 노드의 모든 자식 노드가 제거되고 할당한 문자열이 텍스트로 추가됨
- DOM 조작
    - innerHTML → 요소 노드의 시작 태그와 종료 태그 사이 콘텐츠 영역 내 포함된 모든 HTML 마크업을 포함하여 문자열로 반환
        - 할당하면 요소 노드의 모든 자식 노드가 제거되고 할당한 문자열에 포함되어 있는 HTML 마크업까지 파싱되어 요소 노드의 자식 노드로 DOM에 반영
        - 사용자로부터 입력받은 데이터를 innerHTML 프로퍼티에 할당하는 것은 크로스 사이트 스크립팅 공격에 취약하다.
        - 기존 요소를 제거하지 않으면서 위치를 지정해 새로운 요소를 삽입하는 것이 불가능
    - insertAdjacentHTML → 기존 요소를 제거하지 않으면서 위치를 지정해 새로운 요소 삽입
        - innerHTML과 동일하게 크로스 사이트 스크립팅 공격에 취약
        - innerHTML 프로퍼티보다 효율적이고 빠르다.
    - 노드 생성과 추가
        - document.createElement(tagname) → 요소 노드를 생성하여 반환. 아직 자식 노드(텍스트 노드)를 가지지 않고 DOM에 추가 처리가 따로 필요함
        - document.createTextNode(text) → 텍스트 노드를 생성하여 반환. 아직 부모 요소를 가지지 않아 추가 처리가 따로 필요함
        - Node.appendChild(childNode) → appendChild를 호출한 노드의 마지막 자식 노드로 인수 노드를 추가. 텍스트를 요소 노드에 추가하고, 요소 노드를 부모 노드에 추가해야만 비로소 요소 노드가 DOM에 추가됨.
        - 여러 번 요소 노드를 생성하여 추가하는 것은 리플로우와 리페인트도 여러 번 실행되기에 높은 비용이 든다. 횟수를 줄이는 것이 성능에 유리하다. → document.createDocumentFragment 메서드를 사용
    - 노드 삽입
        - Node.appendChild →인수로 전달받은 노드를 호출한 노드의 마지막 자식 노드로 DOM에 추가
        - Node.insertBefore(newNode, childNode) → 첫 번째 인수로 전달받은 노드를 두 번째 인수로 전달받은 노드 앞에 삽입. 두 번째 인수로 전달받은 노드는 반드시 insertBefore 메서드를 호출한 노드의 자식 노드이어야 한다. 아니면 DOMException 에러 발생. 두 번째 인수가 null이면 appendChild와 동일하게 마지막 자식 노드로 추가
    - 노드 이동
        - appendChild 또는 insertBefore 메서드를 사용하여 DOM에 이미 존재하는 노드를 DOM에 다시 추가하면 현재 위치에서 해당 노드를 제거, 새로운 위치에 노드를 추가(이동)
    - 노드 복사
        - Node.cloneNode([deep: true | false]) → 노드의 사본을 생성, 반환. true면 깊은 복사, false면 얕은 복사. 얕은 복사로 생성된 요소 노드는 자손 노드를 복사하지 않으므로 텍스트 노드도 없다.
    - 노드 교체
        - Node.replaceChild(newChild, oldChild) → 자신을 호출한 노드의 자식 노드를 다른 노드로 교체. oldChild 노드는 DOM에서 제거됨.
    - 노드 삭제
        - Node.removeChild(child) → 인수로 전달된 노드를 DOM에서 삭제. 인수는 호출한 노드의 자식 노드이어야 한다.
    

### 어트리뷰트

- type, value, check 어트리뷰트는 input 요소에만 사용 가능하다.
- HTML 문서가 파싱될 때 HTML 요소의 어트리뷰트는 어트리뷰트 노드로 변환되어 요소 노드와 연결된다.
- 모든 어트리뷰트 노드의 참조는 유사 배열 객체이자 이터러블인 NamedNodeMap 객체에 담겨서 요소 노드의 attributes 프로퍼티에 저장된다.
- Element.attributes → getter만 존재하는 읽기 전용 접근자 프로퍼티, 요소 노드의 모든 어트리뷰트 노드의 참조가 담긴 NamedNodeMap 객체를 반환.
- HTML 어트리뷰트 조작
    - Element.getAttribute(attributeName)/setAttribute(attributeName, attributeValue) → HTML 어트리뷰트 값을 참조/변경
    - Element.hasAttribute → 특정 HTML 어트리뷰트 존재 확인
    - Element.removeAttribute → 특정 HTML 어트리뷰트 삭제
- HTML 어트리뷰트 vs DOM 프로퍼티
    - 요소 노드의 초기 상태는 어트리뷰트 노드가 관리
    - 요소 노드의 최신 상태는 DOM 프로퍼티가 관리
    - (사용자 입력에 의한 상태 변화와 관계 있는)DOM 프로퍼티에 의해 값이 할당되어 HTML 요소의 최신 상태 값이 변경되어도 HTML 요소에 지정된 어트리뷰트 값은 변하지 않는다!
- data 어트리뷰트, dataset 프로퍼티
    - HTML 요소에 정의한 사용자 정의 어트리뷰트와 자바스크립트 간에 데이터 교환 가능
    - data 어트리뷰트 값은 HTMLElement.dataset 프로퍼티로 취득.
    - dataset 프로퍼티는 HTML 요소의 모든 data 어트리뷰트의 정보를 제공하는 DOMStringMap 객체를 반환. DOMStringMap 객체는 data어트리뷰트의 data- 접두사 다음에 붙인 임의의 이름을 카멜 케이스로 변환한 프로퍼티를 가진다. → data 어트리뷰트의 값을 취득 or 변경 가능하다.
    - data- 접두사 다음에 존재하지 않는 이름을 키로 사용하여 dataset 프로퍼티에 값을 할당하면 HTML 요소에 data 어트리뷰트가 추가됨.

### 스타일

- HTMLElement.style →인라인 스타일 조작. setter, getter 존재하는 접근자 프로퍼티로서 요소 노드의 인라인 스타일을 취득 or 추가 or 변경.
- CSS 프로퍼티는 케밥 케이스. background-color → backgroundColor
    
    ```jsx
    $div.style.backgroundColor = 'yellow';
    $div.style['background-color'] = 'yellow';
    
    //단위 지정 필요한 CSS 프로퍼티 값은 반드시 단위 지정해야 한다.
    $div.style.width = '100px';
    ```
    
- 클래스 조작
    - Element.className → setter, getter 존재하는 접근자 프로퍼티 → HTML 요소의 class 어트리뷰트 값을 취득 or 변경. 문자열을 반환하므로 공백으로 구분된 여러 개의 클래스를 반환하는 경우 다루기가 불편하다.
    - Element.classList → class 어트리뷰트의 정보를 담은 DOMTokenList 객체 반환 → 유사 배열 객체이면서 이터러블
        - .add → 인수로 전달한 1개 이상의 문자열을 class 어트리뷰트 값으로 추가
        - .remove → 인수로 전달한 1개 이상의 문자열과 일치하는 클래스를 class 어트리뷰트에서 삭제
        - .item → 인수로 전달한 index에 해당하는 클래스를 class 어트리뷰트에서 반환
        - .contains → 인수로 전달한 문자열과 일치하는 클래스가 class 어트리뷰트에 포함되어 있는지  확인. 불리언 반환
        - .replace → class 어트리뷰트에서 첫 번째 인수로 전달한 문자열을 두 번째 인수로 전달한 문자열로 변경
        - .toggle → class 어트리뷰트에 인수로 전달한 문자열과 일치하는 클래스가 존재하면 제거, 존재하지 않으면 추가
        - forEach, entries, keys, values, supports 메서드 제공
- 요소에 적용되어 있는 CSS 스타일 참조
    - window.getComputedStyle → 첫 번째 인수로 전달한 요소 노드에 적용되어 있는 평가된 스타일(모든 스타일이 조합되어 최종 적용된 스타일)을 CSSStyleDeclaration 객체에 담아 반환.