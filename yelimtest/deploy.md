# vercel 배포이후 .env 적용하기

- gitignore 된.env 파일을 배포이후에도 적용해보자.

- 해결법 : vercel에서 환경 변수를 따로 등록해줘야 배포된 사이트가 제대로 동작할 수 있었다

<img src='./img/vercel.env.png' width='300px'/>

- 다음과 같이 들어간후 배포이후 필요한 환경변수들을 적용해주자

- 이러고 나서 다시 build 후 배포하면 끝
