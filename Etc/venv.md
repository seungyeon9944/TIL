# 가상환경 venv
- 독립적인 파이썬 환경 제공
- 간단한 명령어 사용
- 시스템 파이썬과의 분리

1) 가상환경 생성

        python -m venv 가상환경이름
        # 가상환경이 잘 만들어졌다면 루트 디렉토리에 .venv가 생성, 안에 Include, Lib, Scripts, pyvenv.cfg로 구성
    
2) 가상환경 활성화

        call 가상환경이름/Scripts/activate

3) 가상환경 모듈 설치

        pip install reqests