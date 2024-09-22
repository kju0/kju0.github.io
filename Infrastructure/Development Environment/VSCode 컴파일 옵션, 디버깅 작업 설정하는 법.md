vscode에서 실행 버튼을 눌렀을 때 헤더가 없다는 오류가 있었습니다

### 컴파일 옵션 주기
`tasks.json`는 빌드 및 자동화 작업을 정의하는 설정 파일입니다.
이 파일에서 빌드, 컴파일, 테스트 실행, 스크립트 실행과 같은 반복적인 작업을 자동으로 할 수 있게 설정할 수 있죠!

이번에 저는 gcc 컴파일 옵션을 넣어봤습니다.

```shell
gcc -g -o test test.c -I../../headers -L/usr/local/modsecurity/lib -lmodsecurity
```

원래 이렇게 컴파일을 했다면 아래처럼 옵션으로 넣어줄 수 있습니다!

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "build",
      "type": "shell",
      "command": "gcc",
      "args": [
        "-g",
        "${file}",
        "-o",
        "${fileDirname}/${fileBasenameNoExtension}",
        "-I../../headers", // 헤더 파일 경로 추가
        "-L/usr/local/modsecurity/lib", // 라이브러리 경로 추가
        "-lmodsecurity" // ModSecurity 라이브러리 추가
      ],
      "group": {
        "kind": "build",
        "isDefault": true
      },
      "problemMatcher": ["$gcc"]
    }
  ]
}

```


### 디버깅 설정 하기
`launch.json` 디버깅 작업 정의하기

**주요 설정**
- **`program`**: 디버깅할 프로그램의 경로 (예: `./a.out`).
- **`args`**: 디버깅 중 프로그램에 전달할 명령행 인자.
- **`environment`**: 디버깅할 때 필요한 환경 변수 설정.
- **`stopAtEntry`**: 디버깅 시작 시 프로그램의 시작 지점에서 중단할지 여부.
- **`MIMode`**: 디버거 모드 설정 (예: `gdb`).
- **`sourceFileMap`**: 원격 디버깅 시 원격 서버의 소스 파일 경로와 로컬 경로를 매핑.

```
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "C++ Debug",
      "type": "cppdbg",
      "request": "launch",
      "program": "${workspaceFolder}/a.out",
      "args": [],
      "stopAtEntry": false,
      "cwd": "${workspaceFolder}",
      "environment": [],
      "externalConsole": false,
      "MIMode": "gdb",
      "miDebuggerPath": "/usr/bin/gdb",
      "setupCommands": [
        {
          "description": "Enable pretty-printing for gdb",
          "text": "-enable-pretty-printing",
          "ignoreFailures": true
        }
      ],
      "preLaunchTask": "build",
      "targetArchitecture": "x86_64"
    }
  ]
}

```




#### 배운 점
> 과거에 당연하게 검색해서 복붙해서 사용했던 vscode 설정 방법
> 그때 정리 안해놓고 다시 설정하려니 한시간 정도 삽질했네요 ㅎㅎ 이렇게 간단한걸..
> 앞으로 더 정보 추가하면서 vscode 설정 방법 꼼꼼하게 정리해보겠습니다!