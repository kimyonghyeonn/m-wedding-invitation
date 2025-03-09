# 모바일 청첩장 React.js 템플릿

결혼식 초대를 위한 청첩장 템플릿입니다.  
이 저장소가 마음에 들거나 사용하게 되신다면, Star와 Fork 부탁드리겠습니다😉

## 👰🏻‍♀️ 미리 보기

https://wedding-templete.netlify.app/

## 📚 내용 및 기능

- 결혼식 날짜, 위치, 인사말 출력
- 사진첩
- 축의금을 보내실 곳 (계좌번호 클립보드 복사 기능 지원)
- 카카오톡 공유 기능 및 링크 공유 기능

## 🚘 시작하기

1. `$ cd WEDDING_INVITATION` - 해당 프로젝트 폴더로 이동
2. `$ npm install` - 디펜던시 설치
3. `$ npm start` - 로컬로 실행

## 🔧 Netlify로 만들기

Netlify로 만드신다면 아래 글을 참고하세요 🕵🏻‍♂️

[Gatsby 테마로 모바일 결혼 청첩장 만들기](https://joy.pe.kr/gatsby-wedding-deploy/)

2025.03.09 개정

- 배포 전 netlify 세팅

해당 프로젝트 클릭 => 좌측 Site configuration 클릭 => Build & deploy 에서 아래 절차를 실행 or ctrl + f 로 키워드 찾기 후 진행

1. Build settings > Build command 는 CI= npm install && npm run build 로 설정
2. Dependency management 의 Node.js 는 20.x 로 설정
3. Environment variables 의 NODE_VERSION 의 VALUES 도 20으로 세팅 후 저장
4. Environment variables > Add a variable 클릭 => Key : GO_VERSION 입력, Values 는 1.20 으로 세팅 후 저장

- 배포 전 패키지 업데이트 절차

1. sharp 패키지 최신버전으로 업데이트
   => 로컬에서 다음 명령어 실행 (명령어 : npm install sharp@latest)

2. netlify 배포 최적화를 위해 gatsby-plugin-netlify를 추가하고 설정
   => 로컬에서 패키지 설치 (명령어 : npm install gatsby-plugin-netlify)

3. getsby-config.js 에 아래 플러그인 추가
   module.exports = {
   plugins: [`gatsby-plugin-netlify`],
   };

4. Git에 반영 후 push

---

개정된 절차대로 진행했다면 Deploys 에서 Clear cache and deploy site 클릭하여 배포

## ❌ 오류 발생 시

`rm -rf package-lock.json` 과 `rm -rf node_modules` 후 다시 `npm install` 수행

## 🛠 커스터마이징

`./config.js`를 수정하여 사용합니다.

```javascript
export const WEDDING_INVITATION_URL = "http://localhost:8000/";
export const KAKAOTALK_API_TOKEN = "JavaScript 키 입력";
export const KAKAOTALK_SHARE_IMAGE =
  "https://cdn.pixabay.com/photo/2014/11/13/17/04/heart-529607_960_720.jpg";

export const WEDDING_DATE = "1970년 01월 01일, 목요일 오전 12시 00분";
export const WEDDING_LOCATION = "○○○웨딩, ○층 ○○홀";

export const GROOM_NAME = "○○○";
export const GROOM_ACCOUNT_NUMBER = "○○은행 ***-***-******";
export const GROOM_FATHER_NAME = "○○○";
export const GROOM_FATHER_ACCOUNT_NUMBER = "○○은행 ***-***-******";
export const GROOM_MOTHER_NAME = "○○○";
export const GROOM_MOTHER_ACCOUNT_NUMBER = "○○은행 ***-***-******";

export const BRIDE_NAME = "○○○";
export const BRIDE_ACCOUNT_NUMBER = "○○은행 ***-***-******";
export const BRIDE_FATHER_NAME = "○○○";
export const BRIDE_FATHER_ACCOUNT_NUMBER = "○○은행 ***-***-******";
export const BRIDE_MOTHER_NAME = "○○○";
export const BRIDE_MOTHER_ACCOUNT_NUMBER = "○○은행 ***-***-******";
```

`./src/components/location.jsx`를 수정하여 원하는 위치의 카카오 지도를 사용합니다.

```javascript
//  1. `https://map.kakao.com/`로 이동
//  2. 원하는 위치를 검색하여 `HTML 태그 복사`클릭
//  3. `소스 생성하기`클릭
//  4. `timestamp,key` 위의 코드에 알맞게 입력

const executeScript = () => {
  const scriptTag = document.createElement("script");
  const inlineScript = document.createTextNode(`new daum.roughmap.Lander({
    "timestamp" : "1652464367301",
    "key" : "2a8fe",
    "mapWidth" : "640",
    "mapHeight" : "360"
  }).render();`);
  scriptTag.appendChild(inlineScript);
  document.body.appendChild(scriptTag);
};
```
