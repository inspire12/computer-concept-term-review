# JSX
 리액트용 자바스크립트 확장 문법

# Bundling Tool
Node.js 의 주요 특징은 코드를 모듈화하여 재사용할 수 있다는 것! <br>
* es5 까지
```
var React = require('react');
var Component = React.Component;
```
* es6 부터 (2015년)
```
import React, {Component} from 'react';
```
> 하지만 이는 Node.js 의 기능으로 웹 브라우저는 Node.js 런타임으로 실행하는 것이 아니기 때문에 html 파일 안에 script 태그로 파일을 불러온다 <br>
이 때 번들링 도구의 loader를 이용하면 브라우저에서도 파일을 "묶듯이" 연결할 수 있다.

## web-pack을 사용

* babel-loader
ES6을 ES5로 변환해주는 도구, 구 버전 웹 브라우저와 호환하기 위해 사용
* css-loader
* file-loader
