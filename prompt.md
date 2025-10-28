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


---

1. 이전세션에서 devops_api/master_file/comment/20251028/phase1, phase2 수정내역이 있고,  폴더 구조 정리를 하고 있었고 phase3부터는 database layer 부터 시작해서 디렉토리를 git 관련  분리, client 끼리 분리, conifg 분리, ai 분리, 저장소(redis, postgres, vectordb 등) 분리 등으로 최대한 해줘. app 폴더의 root 경로는 main.py만 잇도록 해줘. 디버깅 할일 있으면 docker로 8000 port로 로드 되잇으니 그걸로 확인해



2. 내가 생각하는 흐름대로 가고 있는지 획인하고 아닐 경우 수정좀 해줘

이전 세션에서 devops_api/master_file/comment/20251028/flow_analysis_and_fix_plan.md로 분석을 claude가 해놓은 상황. 그리고 

- cicd jenkins를 통한 흐름은 에러 로그 발생 > 실패 및 에러 시 webhook으로 fastapi 전송 (repo, branch 정보 전달) > redis streams 로 적재 > worker가 일정 주기 큐 발생 > 로그 주요 내용 추출, 이때 repo, branch, 파일위치, 파일 라인등도 최대한 추출 > 에러 핑거프린트로 반복 로그일 경우 끝 > 임베딩을 통해 그 이후는 redis, qdrant 로 캐싱 조회 > 없을 경우 여러 agent 등을 통해 솔루션 생성 및 적재 (이때 나의 repo 및 브랜치 스캔하는 agent, java_spring, python_fastapi, js_express, 각 프레임쿼크 전문가로부터 받은 분석으로 솔루션을 생성하는 agent (해당 agent는 solution 재생산에도 관야) 등의 전문 agent  개입 )
- application log 흐름도 promtail를 제외하곤 유사할 듯.
- 이 과정에서 코드 리뷰, 코드 보안 체크 agent는 삭제 
- 그리고 front 빼고는 docker로 실행하고 있으니 devops_api와 example 쪽의 docker-compose 모두 고려해서 동작하도록 (애플리케이션 수집 promtail 도 devops_api로 잘 들어가는지도 확인)


---

1. hyde 기법을 활용해서 좀더 솔루션의 성능을 높이고 싶음 