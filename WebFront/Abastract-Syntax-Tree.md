 # AST
1. AST 가 무엇인지
2. plain 코드에서 AST가 어떻게 만들어지는지 
3. AST 처리 위에 만들어진 도구 중 가장 많이 쓰이는 사례들 
4. AST 데모 

## Abstract Syntax Tree 
소스 코드 구조를 표시하는 계층적 프로그램 표현 

### plain 코드에서 추출 
컴파일러의 Lexical and Syntax Analysis <br>
1. Lexical analyzer (스캐너) : 어휘 분석기
 -> 문자열을 토큰 목록으로 분할

2. Syntax 
 -> 토큰 목록으로 언어구문을 검증하고 트리 구조로 변환 
 
### 코드 Transpiling과 Babel 

Babel : JS 컴파일러 (코드 파싱, 변환, 생성 3단계)
     AST를 구축하고 적용된 플러그인에 기반하여 AST를 탐색하며 수정 후, 수정된 AST에서 새로운 코드 생성 

     

[자바스크립트 개발자를 위한 AST 번역](https://gyujincho.github.io/2018-06-19/AST-for-JS-devlopers)