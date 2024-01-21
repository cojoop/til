# Typescript 컴파일시 세부설정

`tsconfig.json`은 `TypeScript` 프로젝트의 설정 파일로, `TypeScript` 컴파일러가 프로젝트를 어떻게 처리해야 하는지에 대한 설정을 지정합니다. 이 파일을 사용하여 컴파일러 옵션, 파일 경로 및 프로젝트 구성 등을 설정할 수 있습니다.
> 타입스크립트 `.ts` 파일들을 `.js` 파일로 변환할 때 어떻게 변환할 것인지 세부설정이 가능합니다.

&nbsp;

## compilerOptions

`TypeScript` 컴파일러의 동작을 제어하는 데 사용되는 옵션입니다.

```json
"compilerOptions": {
  "target": "es5",
  "module": "commonjs",
  "strict": true
}
```

- `target` 속성은 `ECMAScript` 버전을 지정하며, `module` 속성은 코드를 어떻게 모듈화할지를 지정합니다.

> **ECMAScript:** `JavaScript`의 표준 규격을 정의하는 문서

&nbsp;

## include 및 exclude

```json
"include": [
  "src/**/*.ts"
],
"exclude": [
  "node_modules"
]
```

- `include`는 컴파일할 파일이나 디렉토리를 지정합니다.
- `exclude`는 특정 파일이나 디렉토리를 컴파일에서 제외합니다.

&nbsp;

## files

```json
"files": [
  "src/main.ts",
  "src/example.ts"
]
```

- 특정 파일만 컴파일하고자 할 때 사용합니다.

&nbsp;

## extends

```json
"extends": "./common/tsconfig.base.json",
"compilerOptions": {
  "outDir": "./dist"
}
```

- 다른 설정 파일을 확장하여 설정을 상속할 수 있습니다.
- 이는 공통 설정을 분리하여 재사용 가능한 설정을 만드는 데 도움이 됩니다.

&nbsp;

## ts-node

```json
"ts-node": {
  "compilerOptions": {
    "module": "commonjs"
  }
}
```

- `TypeScript`로 작성된 `Node.js` 애플리케이션을 실행하는 데 사용되는 `ts-node`의 설정을 지정할 수 있습니다.

&nbsp;

## references

```json
"references": [
  { "path": "./common" },
  { "path": "./app" }
]
```

- 프로젝트 간에 의존성이 있는 경우, `references`를 사용하여 해당 의존성을 설정할 수 있습니다.

> 이러한 옵션들을 사용하여 프로젝트의 `TypeScript` 설정을 조절할 수 있습니다. `tsconfig.json` 파일을 사용하면 `TypeScript` 컴파일러가 프로젝트에 대한 다양한 측면을 제어할 수 있어 코드의 일관성과 유지보수가 쉬워집니다.
