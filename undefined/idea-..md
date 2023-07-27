# idea . 명령어 실행 불가

idea . 명령이 터미널에서 실행이 되지 않아서 시작됨

intellij에서 tools → create command line에서 터미널 명령어를 생성해야 하는데 이 작업 또한 ![](<../.gitbook/assets/스크린샷 2023-07-27 오후 12.19.39.png>)\
위와 같은 메세지가 뜨면서 생성 불가



해결법은 먼저 아래 명령어를 통해 intellij가 실행 되는지 확인 후

`open -na "IntelliJ IDEA CE.app"`



/usr/local/bin 에 idea 실행파일을 만들어야 함 그리고 그 파일 안에&#x20;

```
#!/bin/sh

open -na "IntelliJ IDEA CE.app" --args "$@"
```

를 써 넣어야 함 (학생용 이기 때문에 CE)



그리고 이렇게 했는데도 저 메세지가 계속 뜸

그래서 노아님께 도움 요청해서 해결 해주심 정확한 방법은 잘 모르겠는데 대략적인 방법은

실행 스크립트를 터미널에서 만들어서 터미널에서 명령어 입력하면 intellij가 작동됨

intellij내부에서 명령어 만들기는 계속해서 메세지 창이 뜨지만 결과적으로 터미널에서 명령어 실행은 되니 해결\
