# 코드스테이츠 30일차 정리(개인 TIL)

생성일: 2023년 3월 27일 오전 10:06
태그: 코드스테이츠 일일 정리

### DeepDive 챕터 09 타입 변환 공부 및 정리

### DeepDive 챕터 10 객체 리터럴 공부  및 정리

## Project-Flag 개발

1. FormData() 객체를 이용해서 파일을 서버에 전송하기
2. Edit Page 레이아웃 수정
3. Edit Page 회원탈퇴 Modal 수정 및 기능 구현
4. My Page 기본 사진 출력, 수정된 사진 출력 기능 구현

## 처음 듣거나 어려웠던 부분(암기할 부분)

**에러 1**: is a void element tag and must neither have `children` nor use `dangerouslysetinnerhtml`.

⇒ Edit Page에서 Delete Modal 화면의 div를 input으로 잘못 바꾸고 생긴 오류 / input 태그 내에 태그가 있으면 안된다는 의미

**에러 2**: react form submission canceled because the form is not connected

⇒ form 형식에서 submit이 엔터로 눌리지 않고 나타난 오류 / button이 두 개 이상 있다면, type을 정확히 명시해주거나 button을 아예 하나로 통합해야한다.

FormData() 공부