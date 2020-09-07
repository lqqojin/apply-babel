#Babel Tutorial
출처:[1분코딩 자바스크립트 바벨 튜토리얼](https://www.youtube.com/watch?v=VeK3a29x1hE&t=3s)

## 초기화

프로젝트 폴더에서,

```
npm init -y
```
## babel-cli 설치

```
npm install --save-dev babel-cli
```

-g 옵션으로 글로벌로 설치하거나, 각 프로젝트마다 다른 babel 버전을 사용하는 경우 --save-dev 옵션으로.

### npm script로 자동화

package.json 파일을 수정

```
"scripts": {
  "build": "babel ./public/src -d ./public/lib -w"
},
```
실행은 아래와 같이.

```
npm run build
```

./public/src 경로에 있는 원본 코드를 변환해서 ./public/lib 안에 생성.

이 상태에서 그냥 npm run build를 실행하면, 바벨은 그냥 src 안의 파일과 같은 파일을 lib에 생성한다. 변환 작업을 위해서는 변환 옵션을 설정해야 하는데, 그 때 사용하는 파일이 아래의 .babelrc

## .babelrc 파일로 설정

.babelrc를 생성하고 아래의 기본 구성 내용을 입력.
플러그인을 사용하지 않는다면 plugins는 생략해도 무방.

```
{
  "presets": [],
  "plugins": []
}
```

우리는 ECMA 2015 preset을 사용하기 위해 해당 preset을 설치

```
npm install --save-dev babel-preset-es2015
```

그리고 .babelrc 파일에 우리가 사용할 프리셋(설치한 프리셋)을 추가
```
{
	"presets": ["es2015"]
}
```

여기까지 하면 기본적으로 잘 동작한다.

## minify

lib에 압축된 버전의 파일을 생성하기 위해 minify 패키지를 설치.

```
npm install --save-dev babel-preset-minify
```

.babelrc 파일에도 추가

```
{
	"presets": ["es2015", "minify"]
}
```

npm run build 수행 시 "Couldn't find intersection" 에러가 날 경우,
.babelrc 파일을 아래와 같이 바꾸어 주자.

```
{
	"presets": [
		"es2015",
		["minify", {builtIns: false, evaluate: false, mangle: false}]
	]
}
```
