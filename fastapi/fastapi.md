
# FastAPI 설치 및 사용 가이드 (Mac)

이 가이드는 Mac에서 FastAPI를 설치하고 간단한 애플리케이션을 실행하는 방법을 설명합니다.

## 1. Python 및 pip 확인

FastAPI는 Python 3.7 이상이 필요합니다. 터미널을 열고 다음 명령어를 실행하여 Python과 pip가 설치되어 있는지 확인합니다:

```sh
python3 --version
pip3 --version
```

만약 설치되어 있지 않다면, [Python 공식 웹사이트](https://www.python.org/downloads/)에서 최신 버전을 다운로드하여 설치합니다.

## 2. 가상 환경 설정 (선택 사항)

가상 환경을 사용하는 것은 프로젝트 간의 패키지 충돌을 방지하는 좋은 방법입니다. 다음 명령어로 가상 환경을 설정할 수 있습니다:

```sh
python3 -m venv myenv
source myenv/bin/activate
```

이 명령어는 `myenv`라는 이름의 가상 환경을 생성하고 활성화합니다.

## 3. FastAPI 및 Uvicorn 설치

이제 FastAPI와 Uvicorn을 설치합니다. Uvicorn은 ASGI 서버로, FastAPI 애플리케이션을 실행하는 데 사용됩니다.

```sh
pip install fastapi uvicorn
```

## 4. FastAPI 애플리케이션 작성

`main.py` 파일을 생성하고 다음과 같은 기본 FastAPI 애플리케이션 코드를 작성합니다:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello": "World"}

@app.get("/items/{item_id}")
def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "q": q}
```

## 5. 애플리케이션 실행

터미널에서 다음 명령어를 실행하여 애플리케이션을 실행합니다:

```sh
uvicorn main:app --reload
```

- `main:app`은 `main.py` 파일의 `app` 인스턴스를 의미합니다.
- `--reload`는 코드 변경 시 자동으로 서버를 다시 시작하게 합니다.

브라우저에서 `http://127.0.0.1:8000`에 접속하면 `{"Hello": "World"}`라는 응답을 볼 수 있습니다.

## 6. API 문서 확인

FastAPI는 자동으로 API 문서를 생성합니다. 다음 URL에 접속하여 각각의 문서화 도구를 확인할 수 있습니다:

- **Swagger UI**: `http://127.0.0.1:8000/docs`
- **ReDoc**: `http://127.0.0.1:8000/redoc`

## 7. 가상 환경 비활성화 (선택 사항)

작업이 끝난 후 가상 환경을 비활성화하려면 다음 명령어를 실행합니다:

```sh
deactivate
```

## 요약

이 문서에서는 Mac에서 FastAPI를 설치하고 간단한 애플리케이션을 실행하는 방법을 설명합니다. 가상 환경 설정부터 FastAPI와 Uvicorn 설치, 기본 애플리케이션 작성 및 실행까지의 과정을 다룹니다. 
