# 03. UI 이벤트 

## 마우스 이벤트
- `mousedown·mouseup`, `mouseover·mouseout`, `mousemove`, `click`, `dbclick`, `contextmenu`
- `oncopy="alert('copy 불가능!!'); return false;" : 텍스트 복사 막기 
- `mouseover/out` : 버블존재, 한 번에 하나의 요소만 있다고 생각 
- `mouseenter/leave` : 마우스가 요소 전체에 들어오고 나올 때만 트리거처리됨

## 키보드 이벤트
- `keydown` : 키보드 눌렀을 때 
- `keyup` : 키를 놓았을 때 

## 스크롤
```
window.addEventListener('scroll', function() {
  document.getElementById('showScroll').innerHTML = window.pageYOffset + 'px';
});
```
- 마우스 스크롤 시 이벤트 리스너
