---
layout: post
title:  "Typescript 자주 쓰는 tsconfig 설정 메모"
author: Hyunseok
categories: frontend
comments: true
---

#### Typescript 사용 시 자주 쓰는 tsconfig 옵션 메모 

```
{
  "compilerOptions": {
    "target": "es5", // 사용할 ECMAScript 버전 설정
    // 컴파일에 포함될 라이브러리 파일 목록
    // target 옵션 값에 따라 기본으로 포함되는 라이브러리가 있다.
    // lib 옵션 설정시 그 라이브러리 파일만 포함된다.
    "lib": [
      "dom",
      "dom.iterable",
      "esnext"
    ],
    "outDir": "./build/", // 컴파일 출력 폴더 설정
    "sourceMap": true,
    "allowJs": true, // 자바스크립트 파일 컴파일 허용 여부.
    "skipLibCheck": true, // 모든 선언 파일의 유형 검사 건너뛰기 (*.d.ts)
    "esModuleInterop": true, // import default를 사용 가능하게 설정.
    "allowSyntheticDefaultImports": true, // export default 를 export 한 값들을 가지는 객체로 설정
    "strict": true, // 엄격한 유형 검사 활성화
    "forceConsistentCasingInFileNames": true, // 동일 파일에 대해 일관되지 않은 참조 허용하지 않음.
    "module": "commonjs", // 모듈 설정
    "moduleResolution": "node", // 모듈 (검색)해석 방식 설정
    "isolatedModules": true, // 각 파일을 별도의 모듈로 변환.
    "noEmit": true, // 출력을 표시하지 않음.
    "removeComments": true,  // 주석 삭제
    "jsx": "react", // jsx 지원
    "baseUrl": "./src",
    "resolveJsonModule": true,
    "keyofStringsOnly": true
  },
  "include": [
    "./src/**/*"
  ],
  "exclude": [
    "./node_modules/**/*"
  ]
}
```
