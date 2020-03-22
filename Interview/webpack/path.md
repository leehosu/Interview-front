# Path

## `__dirname`, `__filename`

노드에서는 모듈 관계가 있는 경우가 많아 현재 파일의 경로나 파일명을 알아야하는 경우가 많다.

`__filename`, `__dirname`이라는 키워드로 경로에 대한 정보를 나타낸다.

파일에 `__filename`, `__dirname` 변수를 넣어두면 실행시 현재 파일명과 파일 경로로 바뀐다.

```js
// file명을 포함한 절대 경로
console.log(__filename);

//file 명을 제외한 절대 경로
console.log(__dirname);
```

해당 변수의 결과는 어떤 운영체제를 사용하냐에 따라 달라질 수 있는데, `windows`의 경우 구분자로 `\`를 써서 나타내고 `mac/linux` 운영체제의 경우 구분자 `/`를 써서 결과가 출력된다.

## path 모듈

`path` 모듈은 운영체제별로 경로 구분자가 달라 생기는 문제를 쉽게 해결하기 위해 등장했다.

운영체제 별로 달라지는 이슈는 다음과 같다.

- windows : `\`를 사용하여 폴더를 구분한다.
- mac/linux : `/`를 사용하여 폴더를 구분한다.

`path` 모듈을 사용하면 폴더와 파일의 경로를 쉽게 조작할 수 있어 구분자 이슈를 쉽게 해결하고, 이외에 파일명에서 파일명, 확장자를 별도로 떼어서 활용할 수 있다.

## path 모듈의 사용

`path` 모듈은 내장 모듈이므로 별도의 `npm` 설치 없이 사용할 수 있다.

```js
const path = require("path");
```

## path.resolve([...paths])

- `...paths<string>` : a sequence of paths or path segments
- `returns` : `<string>`

여러 인자를 넣으면 경로를 묶어 root 경로를 고려한 새로운 경로를 반환한다.

1. 오른쪽 인자부터 읽어가며 절대경로를 만든다.

```js
path.resolve("/a", "b", "c");
// return : /a/b/c

// a가 root 경로가 아닌 경우 root folder까지의 경로를 붙여서 반환한다.
path.resolve("/a", "b", "c");
//return : user/temp/a
```

2. 오른쪽 인자부터 읽다가 `/folder_name` 형태의 경로가 등장하면 절대 경로로 인식하여 반환한다.

```js
// /b가 절대 경로이므로 /b/c가 반환되고 /a는 무시한다.
path.resolve("/a", "/b", "c");
// return : /b/c
```

3. 인자 중 절대 경로가 지정되어 있지 않으면 `working directory`를 추가하여 절대 경로를 만든다.

```js
path.resolve("a", "b", "c");
// {current_working_directory}/a/b/c
```

4. 어떤 인자도 전달하지 않는다면 현재 `working directory`를 반환한다.

```js
// user/temp/directory.js에서 실행했다면
console.log(path.resolve(""));
//return : /user/temp
```

## path.join([...paths])

- `...paths<string>` : a sequence of path segments
- `retruns` : `<string>`

여러 인자를 넣으면 하나의 경로를 합쳐 반환한다.

상대 경로를 표시하는 `..`와 현 위치를 표현하는 `.`도 반영한 결과를 `return`한다.

```js
path.join("/foo", "bar", "baz/asdf", "qwer");
// return : /foo/bar/baz/asdf/qwer

path.join("/foo", "bar", "bax/asdf", "qwer", "...");
// return : /foo/bar/asdf

//__dirname : user/ano/temp/directory
path.join(__dirname, "..", "..", "workspace", ".", "/ano");
// return : /user/ano/workpace/ano
```

## path.sep

경로의 구분자(`seperator`)이다.

windows에서는 `\`, mac/linux에서는 `/`이다.

## path.delimiter

환경 변수의 구분자이고 `:`, clone이 쓰이고 있다.

## path.dirname(paths)

- `path` : `<string>`
- `return` : `<string>`

현재 파일이 위치한 폴더 경로를 보여준다.

```js
// __filename : '/user/ano/temp/directory.js
path.dirname(__filemane);
// return : /user/ano/tmp
```

## path.extname(paths)

- `path` : `<string>`
- `return` : `<string>`

파일의 확장자를 보여준다.

```js
// __filename : '/user/ano/temp/directory.js
path.extname(__filemane);
// return : .js
```

## path.basename(path[, ext])

- `path` : `<string>`
- `ext` : `<string>`
- `return` : `<string>`

파일의 이름(확장자 포함)을 보여준다.

파일의 이름만 표시하고 싶다면 `basename`의 두 번째 인자로 파일의 확장자(ext)를 넣어주면 된다.

```js
// __filename : '/Users/ano/temp/directory.js'

path.basename(__filename);
//return : 'directory.js'

path.basename(__filename, path.extname(__filename));
// return : directory
```

## path.parse()

- `path` : `<string>`
- `return` : `<object>`

파일 경로를 인자로 받아 `root`, `dir`, `base`, `ext`, `name`으로 분리한 후 해당 내용을 담은 객체 값을 `return`한다.

```js
// on mac/linux:
path.parse('/home/user/dir/file.txt');
// Returns:
// { root: '/',
//   dir: '/home/user/dir',
//   base: 'file.txt',
//   ext: '.txt',
//   name: 'file' }
┌─────────────────────┬────────────┐
│          dir        │    base    │
├──────┬              ├──────┬─────┤
│ root │              │ name │ ext │
"  /    home/user/dir / file  .txt "
```

```js
// On Windows:
path.parse('C:\\path\\dir\\file.txt');
// Returns:
// { root: 'C:\\',
//   dir: 'C:\\path\\dir',
//   base: 'file.txt',
//   ext: '.txt',
//   name: 'file' }
┌─────────────────────┬────────────┐
│          dir        │    base    │
├──────┬              ├──────┬─────┤
│ root │              │ name │ ext │
" C:\      path\dir   \ file  .txt "
└──────┴──────────────┴──────┴─────┘
```

`path`가 문자열이 아닌 경우 `Type Error`를 return한다.

## path.format(pathObject)

pathObject : `<Object>`

- `dir` : `<string>`
- `root` : `<string>`
- `base` : `<string>`
- `name` : `<string>`
- `ext` : `<string>`
  `return` : `<string>`

`path.parse()`한 객체를 인자로 받아 합친 후 경로를 return한다.

```js
// __filename : '/Users/ano/temp/directory.js'
path.prase(__filename);
/*Returns: 
{
  root: "/", 
  dir: "/Users/ano/temp", 
  base: "directory.js", 
  ext: ".js", 
  name: "directory"
}
*/
```

## path.normalize(path)

- `path` : `<string>`
- `return` : `<string>`

```js
path.nomalize("\\Users///ano\\\temp/directory.js");
// return: '/Users/ano/temp/directory.js'
```

## path.isAbsolute(path)

- `path` : `<string>`
- `return` : `<string>`

파일의 경로가 절대 경로인지, 상대경로인지 `true`, `false`로 반환하여 알려준다.

```js
path.isAbsolute("/users"); // return : true
path.isAbsolute("./ano"); // return : false
```

## path.relative(from,to)

- `from` : `<string>`
- `to` : `<string>`
- `return` : `<string>`

두 경로를 인자로 전달하면, 첫 번째 경로에서 두 번째 경로로 가는 방법을 결과로 `return`한다.

```js
path.relative('/user/ano/temp/directory.js','/users);
//return : '../../..'
```
