프로젝트 관련해서 api 쪽 수정이 필요할 것 같아.

1. devopi_api에서 multiagent는 아래와 같이 나눠야할 것 같아.
- 에러 분류 agent
- 자바 및 스프링 전문 agent (문제원인 및 해결책 제시)
- 파이썬 및 fastapi 전문 agent (문제원인 및 해결책 제시)
- js 및 express 전문 agent (문제원인 및 해결책 제시)
- git repo 조회하는 agent 

2. example api에서 에러 발생 시 스택 트레이스 를 발생시키는 10개와 파일명(위치까지), 메서드명에서 알려주는 예제 10개씩 각각 fastapi, express.js에 20개씩 40개 만들어줘. 

3. devops_api 폴더 정리도 좀 해줘 app 밑에 너무 많은 파일들이 있어서 분류는 해야할꺼같아.

---

1. git agent 는 문제가 발생한 repo 및 branch를 pull 또는 clone 하여서 문제의 파일을 활용하여 다른 분석 agent가 활용할 수 있도록 해줘

2. 그리고 해당 repo 및 branch를 가져와서 git agent 가 하는 경로를 devops_api/local_repo 로 가져와서 배치하도록 하는데 브랜치 이름에 해당경로로 만들어줘. 예를들어 A라는 repo에 master라는 브랜치이면 local/master/A로 해줘 