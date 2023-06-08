---
layout: post
title: 기존 리액트 포르젝트에 typescript 설치하기
image: typescript_logo.png
excerpt: typescript
categories: typescript
category: typescript
tags: [react, typescript, tsx, tsc]
---

최근에 열심히 공부중인 typescript!  
스터디를 통해서 타입스크립트 프로그래밍 책도 읽고 있고 공식 문서도 읽어보고 있는데 이론만 공부하니 좀 지루한 느낌이다.  
직접 코딩을 해봐야겠다고 생각이 들어서 기존에 가볍게 만들어둔 react 프로젝트에 typescript를 설치하고 적용해보려고 한다.

---

### typscript 모듈 설치

기존 프로젝트에 모듈들을 설치해줬다.
{% highlight npm %}
npm install --save typescript @types/node @types/react @types/react-dom
{% endhighlight %}
<br />

#### `typescript`
TypeScript를 설치하고, 프로젝트의 종속성(dependencies)으로 추가하는 명령어다.  
<br />

#### `@types/node`
Node.js 환경에서 TypeScript로 작성된 코드에서 Node.js의 타입 정의(Type Definitions)를 사용할 수 있도록 해준다.  
ex) fs, http, https  
<br />

#### `@types/react`
React의 타입 정의를 제공한다.
React 컴포넌트, Props, State, 이벤트 핸들러 등에 대한 타입 정보를 포함하고 있다.  
ex) ReactElement, Props, State  
<br />

#### `@types/react-dom`
React DOM에 대한 TypeScript 타입 정의를 제공한다.  
React DOM은 React를 사용하여 웹 애플리케이션을 개발할 때 사용되는 라이브러리이다.  
ex) ReactDOM, ReactDOM.render, ReactDOM.hydrate  
<br />

---

### tsconfig.json 파일 추가

프로젝트 내의 루트 폴더에 ```tsconfig.json```를 직접 추가해주도 되지만 나는 명령어로 생성해줬다.
아래 명령어를 실행하면 자동적으로 ```tsconfig.json```이 추가된다.
{% highlight npm %}
npx tsc --init
{% endhighlight %}

생성된  파일의 내용은 아래와 같다.
{% highlight jsonc %}
{
  "compilerOptions": {
    /* Visit https://aka.ms/tsconfig to read more about this file */

    /* Projects */
    // "incremental": true,                              /* Save .tsbuildinfo files to allow for incremental compilation of projects. */
    // "composite": true,                                /* Enable constraints that allow a TypeScript project to be used with project references. */
    // "tsBuildInfoFile": "./.tsbuildinfo",              /* Specify the path to .tsbuildinfo incremental compilation file. */
    // "disableSourceOfProjectReferenceRedirect": true,  /* Disable preferring source files instead of declaration files when referencing composite projects. */
    // "disableSolutionSearching": true,                 /* Opt a project out of multi-project reference checking when editing. */
    // "disableReferencedProjectLoad": true,             /* Reduce the number of projects loaded automatically by TypeScript. */

    /* Language and Environment */
    "target": "es2016",                                  /* Set the JavaScript language version for emitted JavaScript and include compatible library declarations. */
    // "lib": [],                                        /* Specify a set of bundled library declaration files that describe the target runtime environment. */
    // "jsx": "preserve",                                /* Specify what JSX code is generated. */
    // "experimentalDecorators": true,                   /* Enable experimental support for TC39 stage 2 draft decorators. */
    // "emitDecoratorMetadata": true,                    /* Emit design-type metadata for decorated declarations in source files. */
    // "jsxFactory": "",                                 /* Specify the JSX factory function used when targeting React JSX emit, e.g. 'React.createElement' or 'h'. */
    // "jsxFragmentFactory": "",                         /* Specify the JSX Fragment reference used for fragments when targeting React JSX emit e.g. 'React.Fragment' or 'Fragment'. */
    // "jsxImportSource": "",                            /* Specify module specifier used to import the JSX factory functions when using 'jsx: react-jsx*'. */
    // "reactNamespace": "",                             /* Specify the object invoked for 'createElement'. This only applies when targeting 'react' JSX emit. */
    // "noLib": true,                                    /* Disable including any library files, including the default lib.d.ts. */
    // "useDefineForClassFields": true,                  /* Emit ECMAScript-standard-compliant class fields. */
    // "moduleDetection": "auto",                        /* Control what method is used to detect module-format JS files. */

    /* Modules */
    "module": "commonjs",                                /* Specify what module code is generated. */
    // "rootDir": "./",                                  /* Specify the root folder within your source files. */
    // "moduleResolution": "node",                       /* Specify how TypeScript looks up a file from a given module specifier. */
    // "baseUrl": "./",                                  /* Specify the base directory to resolve non-relative module names. */
    // "paths": {},                                      /* Specify a set of entries that re-map imports to additional lookup locations. */
    // "rootDirs": [],                                   /* Allow multiple folders to be treated as one when resolving modules. */
    // "typeRoots": [],                                  /* Specify multiple folders that act like './node_modules/@types'. */
    // "types": [],                                      /* Specify type package names to be included without being referenced in a source file. */
    // "allowUmdGlobalAccess": true,                     /* Allow accessing UMD globals from modules. */
    // "moduleSuffixes": [],                             /* List of file name suffixes to search when resolving a module. */
    // "resolveJsonModule": true,                        /* Enable importing .json files. */
    // "noResolve": true,                                /* Disallow 'import's, 'require's or '<reference>'s from expanding the number of files TypeScript should add to a project. */

    /* JavaScript Support */
    // "allowJs": true,                                  /* Allow JavaScript files to be a part of your program. Use the 'checkJS' option to get errors from these files. */
    // "checkJs": true,                                  /* Enable error reporting in type-checked JavaScript files. */
    // "maxNodeModuleJsDepth": 1,                        /* Specify the maximum folder depth used for checking JavaScript files from 'node_modules'. Only applicable with 'allowJs'. */

    /* Emit */
    // "declaration": true,                              /* Generate .d.ts files from TypeScript and JavaScript files in your project. */
    // "declarationMap": true,                           /* Create sourcemaps for d.ts files. */
    // "emitDeclarationOnly": true,                      /* Only output d.ts files and not JavaScript files. */
    // "sourceMap": true,                                /* Create source map files for emitted JavaScript files. */
    // "outFile": "./",                                  /* Specify a file that bundles all outputs into one JavaScript file. If 'declaration' is true, also designates a file that bundles all .d.ts output. */
    // "outDir": "./",                                   /* Specify an output folder for all emitted files. */
    // "removeComments": true,                           /* Disable emitting comments. */
    // "noEmit": true,                                   /* Disable emitting files from a compilation. */
    // "importHelpers": true,                            /* Allow importing helper functions from tslib once per project, instead of including them per-file. */
    // "importsNotUsedAsValues": "remove",               /* Specify emit/checking behavior for imports that are only used for types. */
    // "downlevelIteration": true,                       /* Emit more compliant, but verbose and less performant JavaScript for iteration. */
    // "sourceRoot": "",                                 /* Specify the root path for debuggers to find the reference source code. */
    // "mapRoot": "",                                    /* Specify the location where debugger should locate map files instead of generated locations. */
    // "inlineSourceMap": true,                          /* Include sourcemap files inside the emitted JavaScript. */
    // "inlineSources": true,                            /* Include source code in the sourcemaps inside the emitted JavaScript. */
    // "emitBOM": true,                                  /* Emit a UTF-8 Byte Order Mark (BOM) in the beginning of output files. */
    // "newLine": "crlf",                                /* Set the newline character for emitting files. */
    // "stripInternal": true,                            /* Disable emitting declarations that have '@internal' in their JSDoc comments. */
    // "noEmitHelpers": true,                            /* Disable generating custom helper functions like '__extends' in compiled output. */
    // "noEmitOnError": true,                            /* Disable emitting files if any type checking errors are reported. */
    // "preserveConstEnums": true,                       /* Disable erasing 'const enum' declarations in generated code. */
    // "declarationDir": "./",                           /* Specify the output directory for generated declaration files. */
    // "preserveValueImports": true,                     /* Preserve unused imported values in the JavaScript output that would otherwise be removed. */

    /* Interop Constraints */
    // "isolatedModules": true,                          /* Ensure that each file can be safely transpiled without relying on other imports. */
    // "allowSyntheticDefaultImports": true,             /* Allow 'import x from y' when a module doesn't have a default export. */
    "esModuleInterop": true,                             /* Emit additional JavaScript to ease support for importing CommonJS modules. This enables 'allowSyntheticDefaultImports' for type compatibility. */
    // "preserveSymlinks": true,                         /* Disable resolving symlinks to their realpath. This correlates to the same flag in node. */
    "forceConsistentCasingInFileNames": true,            /* Ensure that casing is correct in imports. */

    /* Type Checking */
    "strict": true,                                      /* Enable all strict type-checking options. */
    // "noImplicitAny": true,                            /* Enable error reporting for expressions and declarations with an implied 'any' type. */
    // "strictNullChecks": true,                         /* When type checking, take into account 'null' and 'undefined'. */
    // "strictFunctionTypes": true,                      /* When assigning functions, check to ensure parameters and the return values are subtype-compatible. */
    // "strictBindCallApply": true,                      /* Check that the arguments for 'bind', 'call', and 'apply' methods match the original function. */
    // "strictPropertyInitialization": true,             /* Check for class properties that are declared but not set in the constructor. */
    // "noImplicitThis": true,                           /* Enable error reporting when 'this' is given the type 'any'. */
    // "useUnknownInCatchVariables": true,               /* Default catch clause variables as 'unknown' instead of 'any'. */
    // "alwaysStrict": true,                             /* Ensure 'use strict' is always emitted. */
    // "noUnusedLocals": true,                           /* Enable error reporting when local variables aren't read. */
    // "noUnusedParameters": true,                       /* Raise an error when a function parameter isn't read. */
    // "exactOptionalPropertyTypes": true,               /* Interpret optional property types as written, rather than adding 'undefined'. */
    // "noImplicitReturns": true,                        /* Enable error reporting for codepaths that do not explicitly return in a function. */
    // "noFallthroughCasesInSwitch": true,               /* Enable error reporting for fallthrough cases in switch statements. */
    // "noUncheckedIndexedAccess": true,                 /* Add 'undefined' to a type when accessed using an index. */
    // "noImplicitOverride": true,                       /* Ensure overriding members in derived classes are marked with an override modifier. */
    // "noPropertyAccessFromIndexSignature": true,       /* Enforces using indexed accessors for keys declared using an indexed type. */
    // "allowUnusedLabels": true,                        /* Disable error reporting for unused labels. */
    // "allowUnreachableCode": true,                     /* Disable error reporting for unreachable code. */

    /* Completeness */
    // "skipDefaultLibCheck": true,                      /* Skip type checking .d.ts files that are included with TypeScript. */
    "skipLibCheck": true                                 /* Skip type checking all .d.ts files. */
  }
}

{% endhighlight %}
<br/>

주석처리가 안된 설정들에 내가 필요하다고 느낀 설정들을 추가해 아래 코드처럼 바꿔주었다.
{% highlight jsonc %}
{
  "compilerOptions": {
    "outDir": "dist",   // 컴파일된 JavaScript 파일이 생성될 디렉토리를 지정
    "target": "es2016",   //컴파일된 JavaScript 코드가 대상으로 하는 ECMAScript 버전을 지정
    "jsx": "react-jsx",  // JSX 코드를 어떻게 변환할지 지정. 여기서는 React JSX를 변환하는 데 사용
    "module": "commonjs",   // 컴파일된 JavaScript 모듈 시스템을 지정
    "allowJs": true,  // TypeScript 컴파일러가 JavaScript 파일을 컴파일할 수 있는지 여부
    "esModuleInterop": true,  // ES 모듈과 CommonJS 모듈 간의 상호 운용성을 향상시키기 위해 추가적인 코드를 생성
    "forceConsistentCasingInFileNames": true,  // 파일 이름의 대소문자 일관성을 검사하는 옵션
    "strict": true,  // 엄격한 타입 체크 옵션을 활성화
    "skipLibCheck": true  // .d.ts 파일에 대한 타입 체크를 건너뛰도록 설정
  }
}
{% endhighlight %}
설정들이 아주 많은데 아직 다 파악하지 못했다.  
나중에는 이 설정들을 이해해서 더 많이 사용해보고 싶다.  
<br/>

이제 프로젝트의 루트인 index.jsx를 index.tsx로 바꿔줬다.
typescript는 `document.getElementById("root")` 이 구문의 타입을 이해할 수 없다.
따라서 HTMLElement로 타입 단언을 해줘야 한다.

{% highlight tsx %}
import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
import reportWebVitals from "./reportWebVitals";
import AppTodo from "./views/AppTodo";

const root = ReactDOM.createRoot(document.getElementById("root") as HTMLElement);
root.render(
  <React.StrictMode>
    <AppTodo />
  </React.StrictMode>
);

reportWebVitals();
{% endhighlight %}

설정들을 활성화했을 때와 안했을 때가 궁금해서 몇가지 테스트를 해보았다.  
`allowJs`를 `true`로 설정해주었을 때는 오류가 발생하지 않았다.
![1](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/a5189f35-47d0-4441-98a3-6077da03bfb8)  
<br/>

하지만 `false`로 설정해주니 jsx파일이나 js파일을 `import`하는 부분에서 에러가 발생했다.  
난 아직 타린이(?)니까 이 설정이 꼭 필요해😂😂😂
![2](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/a129f039-f9d8-4ce6-91b7-06ba48ad441e)

