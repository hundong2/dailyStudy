# npm

- Node Packaged Manager

npm이란 무엇일까?
npm은 Node Packaged Manager의 약자입니다. 무슨 의미인지 한 번 추측을 해볼까요? 

먼저 Node는 Node.js를 의미하는 것 같습니다. Packaged라는 것은 package로 만들어진 것들을 의미하는 것 같습니다. package는 모듈이라고도 불리는데 패키지나 모듈은 프로그램보다는 조금 작은 단위의 기능들을 의미합니다. 그리고 Manager는 잘 아시는 것처럼 관리자를 의미합니다.  이걸 합쳐보면 npm이라는 것은 Node.js로 만들어진 pakage(module)을 관리해주는 툴이라는 것이 됩니다. 

이름처럼 npm은 Node.js로 만들어진 모듈을 웹에서 받아서 설치하고 관리해주는 프로그램입니다. 개발자는 단 몇 줄의 명령어로 기존에 공개된 모듈들을 설치하고 활용할 수 있습니다. 프로그램보다 조금 작은 단위인 이 모듈들을 필요에 따라서 이런 저런 모양으로 쌓아서 활용을 할 수 있다고 하는데 필요한 기능을 적절하게 활용할 수 있다면 개발자 입장에서는 참 좋은 일이죠(Java랑 비교를 하자면 메이븐과 비슷한 역할을 하는 것 같습니다).

거기서 그치는 것이 아니라 이 모듈들을 활용했다면 이후에 그 모듈을 만든 개발자가 업데이트를 하거나 할 경우 체크를 해서 알려주는 듯합니다. 버전관리도 쉬워진다는 의미이죠. 저도 아직 파악 중이긴 하지만 npm을 잘 사용한다면 개발이 훨신 쉬워질 것 같네요 :)
어떻게 npm을 사용하는가?
간략화 해서 설명을 해보겠습니다. 우선 npm을 설치해야겠죠? 예전에는 npm을 따로 설치해야 했지만 지금은 node.js를 설치하면 내장(built in)되어 있다고 합니다. node.js 는 npm을 사용하기 위해서 꼭 필요합니다. node.js의 설치는 node.js의 홈페이지를 방문하거나 간단히 검색을 하면 쉽게 찾으실 수 있습니다(제 경우 다운로드를 하고 다 디폴트 설정으로 했기 때문에 어려운 건 없었습니다).

(이하는 terminal아니 cmd 등에서 실행을 해야 합니다. )

npm은 node.js로 만들어진 모듈을 관리하는 툴이니  npm을 사용한다는 것은 곧 모듈을 활용한다는 것이겠죠? 그러니 가장 먼저 해야 할 일은 사용할 모듈을 다운로드 하는 일입니다. 모듈 다운로드는  'npm install 모듈'과 같은 명령어로 할 수 있습니다. 저는 번들링을 위해서 webpack을 설치해 보겠습니다(번들링은 java가 언어를 컴파일하는 것과 비슷한 역할을 합니다. 여러 파일을 하나로 합쳐주고 또 효율이 좋게 빈칸을 줄이거나 글자수를 줄이는 등의 일을 합니다).
npm install --g webpack
이렇게 일일히 설치할 수도 있지만 모듈의 의존성을 한꺼번에 관리하는 방법도 있습니다. json 파일을 만들어 그 안에 기록을 통해서 관리를 합니다. 우선 json파일을 먼저 생성을 해야겠죠?
npm init
위 명령어를  Terminal 창 등에 입력을 하면 name을 시작으로 여러 가지를 입력을 요청받는데 이름 규약 같은 것을 위반하지 않았으면 엔터를 치면 defaul로 등록이 됩니다. 그 단계에서 바로 설정을 해도 되고 나중에 수정할 수도 있습니다.

이제 package.json파일이 생성된 것을 보실 수 있으실 겁니다.  
```js
{
  "name": "application-study",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "dependencies": {
    "http-server": "0.9.0",
    "rimraf": "2.6.1",
    "webpack": "2.2.1",
    "worker-loader": "0.8.0"
  },
  "scripts": {
    "prebuild": "rimraf dist",
    "build": "webpack --config webpack/webpack.config.js",
    "http-server": "http-server -c-1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/aaa/bbb.git"
  },
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/aaa/bbb/issues"
  },
  "homepage": "https://github.com/aaa/bbb#readme"
}
```

여기서 중요한 부분은 "scripts" 와  "dependencies" 입니다. script는 우리가 run 명령어를 통해서 실행할 것들을 적어두는 것이고 dependencies의 경우는 설치할 모듈들을 의미합니다. npm install -g webpack 같이 설치를 해서 자동으로 기록할 수 있습니다. 

이렇게 package.json 파일이 정리되면 배포를 해야 할 때  파일만 같이 배포를 한다면 해당 프로그램 개발에 사용되었던 모듈을 그대로 인스톨할 수 있게 됩니다.  인스톨은 다음 명령어로 간단하게 할 수 있습니다. 
npm install
그리고 scipts 안의 내용을 실행하기 위해서는 'npm run 이름' 같은 형식으로 실행할 수 있습니다. 예를 들어서 webpack.config.js를 실행시키기 위해서는 다음과 같이 입력합니다(webpack을 통해서 bundling을 하기 위해서 실행해야 할 파일이었습니다).

```
npm run build
```

그리고 http-server를 동작시키기 위해서 아래와 같이 입력합니다.
```
npm run http-server
```

## reference 

[what's the npm?](https://m.blog.naver.com/magnking/220961896609)  