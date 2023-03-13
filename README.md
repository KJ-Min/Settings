# 개발환경 설정

### VSCode - Github 연동시키는 법
1. 폴더 만들기
2. vscode에서 폴더 열기
3. 왼쪽 사이드바 소스제어에서 git init시키기(버튼 눌러서)
4. 새 문서 만들기
5. README파일명은 "README.md" 로 해서 만들기
6. git add하기(+버튼눌러서) 
7. 커밋메시지 작성(체크 버튼 밑)하고 git commit 하기(체크버튼)
8. GitHub에서 저장소 만들기
9. VScode터미널을 이용해서 연동시키기
10. 마지막 git pull까지 하기
>파일에 한글이 쓰였다면 인코딩 꼭 UTF-8로 바꾸고 pull 하기

-----------------------------------------------------------------------------------

### VSCode - C/C++ 개발환경 구축
1. vscode실행 후,  EXTENSION에서 C/C++ 설치
2. MinGW 설치하기 [https://sourceforge.net/projects/mingw/files/](https://sourceforge.net/projects/mingw/files/)
>* mingw-developer-toolkit(msys-base), mingw32-base, mingw32-gcc-g++ 항목을 오른쪽클릭 후 Mark for Installation을 누르기
>*  오른쪽 위 Installation - Apply Changes - Apply - Close
>* 윈도우 검색에 시스템 환경 변수 편집 - 고급 - 환경변수 -  PATH선택 후 편집 - 새로만들기 - C:\MinGW\bin 추가
>* cmd에서 ```gcc-v``` ```gcc++ -v```로 설치 완료 확인
3. 터미널 > 기본 빌드 작업 구성(Ctrl + Shift + B) > 빌드 작업 구성
>* tasks.json 내용 복붙
```json
{
    "version": "2.0.0",
    "runner": "terminal",
    "type": "shell",
    "echoCommand": true,
    "presentation": {
        "reveal": "always"
    },
    "tasks": [
        {
            "label": "save and compile for C++",
            "command": "g++",
            "args": [
                "${file}",
                "-o",
                "${fileDirname}/${fileBasenameNoExtension}"
            ],
            "group": "build",
            "problemMatcher": {
                "fileLocation": [
                    "relative",
                    "${workspaceRoot}"
                ],
                "pattern": {
                    "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning error):\\s+(.*)$",
                    "file": 1,
                    "line": 2,
                    "column": 3,
                    "severity": 4,
                    "message": 5
                }
            }
        },
        {
            "label": "save and compile for C",
            "command": "gcc",
            "args": [
                "${file}",
                "-o",
                "${fileDirname}/${fileBasenameNoExtension}"
            ],
            "group": "build",
            "problemMatcher": {
                "fileLocation": [
                    "relative",
                    "${workspaceRoot}"
                ],
                "pattern": {
                    "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning error):\\s+(.*)$",
                    "file": 1,
                    "line": 2,
                    "column": 3,
                    "severity": 4,
                    "message": 5
                }
            }
        },
        {
            "label": "execute",
            "command": "cmd",
            "group": "test",
            "args": [
                "/C",
                "${fileDirname}\\${fileBasenameNoExtension}"
            ]
        },
        {
            "type": "cppbuild",
            "label": "C/C++: gcc.exe 활성 파일 빌드",
            "command": "C:\\MinGW\\bin\\gcc.exe",
            "args": [
                "-g",
                "${file}",
                "-o",
                "${fileDirname}\\${fileBasenameNoExtension}.exe"
            ],
            "options": {
                "cwd": "${fileDirname}"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": "build",
            "detail": "디버거에서 생성된 작업입니다."
        },
        {
            "type": "cppbuild",
            "label": "C/C++: g++.exe 활성 파일 빌드",
            "command": "C:\\MinGW\\bin\\g++.exe",
            "args": [
                "-g",
                "${file}",
                "-o",
                "${fileDirname}\\${fileBasenameNoExtension}.exe"
            ],
            "options": {
                "cwd": "${fileDirname}"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": "build",
//            "group": {
//               "kind": "build",
//                "isDefault": true
//            },
            
            "detail": "디버거에서 생성된 작업입니다."
        },
        {
            "type": "cppbuild",
            "label": "C/C++: gcc.exe 활성 파일 빌드",
            "command": "C:\\MinGW\\bin\\gcc.exe",
            "args": [
                "-g",
                "${file}",
                "-o",
                "${fileDirname}\\${fileBasenameNoExtension}.exe"
            ],
            "options": {
                "cwd": "${fileDirname}"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": "build",
              
            // "group": {
            //     "kind": "build",
            //     "isDefault": true
            // },

            "detail": "컴파일러: C:\\MinGW\\bin\\gcc.exe"
        }
    ]
}
```
4. 단축기 설정(파일 > 기본설정 > 바로가기 키> ctrl alt검색 > 오른쪽 위 바로가기 키 열기(JSON) > 아래 내용 복붙)
```json
[
    // 컴파일
    {
        "key": "ctrl+alt+c",
        "command": "workbench.action.tasks.build"
    },
    // 실행
    {
        "key": "ctrl+alt+r",
        "command": "workbench.action.tasks.test"
    }
]
```
5. 빌드(저장 및 컴파일) : `Ctrl + Alt + C` // 실행 `Ctrl + Alt + R`
