내 이미지 주소:ghcr.io/tngus1222/guestbook:v2

Dockerfile의 각 줄이 하는 일 설명
FROM python:3.12-slim
#python 3.12-slim 이미지를 기반 이미지로 사용

WORKDIR /app
#/app을  작업 디렉터리로 설정

COPY requirements.txt .
#현재 폴더의 requirements.txt를 /app으로 복사

RUN pip install --no-cache-dir -r requirements.txt
#requirements.txt에 적힌 Python 라이브러리를 설치하되 캐시 파일은 저장하지 않음

COPY . .
#현재 폴더의 모든 파일을 /app으로 복사

RUN useradd -m appuser
#appuer라는 이름의 사용자 계정을 생성

USER appuser
#appuser 사용자 계정을 사용하도록 설정

ENV APP_TITLE="고수현의 방명록" \
    THEME_COLOR="#ffffff"
#환경 변수를 설정함 app_title을 고수현 방명록으로 하고 theme_color를 ffffff로 설정

EXPOSE 5000
#포트 번호로 5000을 사용한다고 명시

CMD ["python", "app.py"]
#컨테이너 시작 시 python으로 app.py를 실행



설정을 넣는 세 가지 방법
코드 : 프로그램 코드에 기본값을 설정
ENV : 이미지를 빌드할 때 기본 환경 변수를 설정
-e : 컨테이너를 실행할 때 환경 변수를 설정
코드 < ENV < -e

실행 결과와 빌드 캐시 동작 로그는 캡쳐로 저장
