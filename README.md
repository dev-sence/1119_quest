# 학교 급식 정보 웹 애플리케이션 개발하기

## 문제 설명
학교 급식 정보를 조회할 수 있는 웹 애플리케이션을 개발하려고 합니다. 
나이스 교육정보 개방 포털의 API를 사용하여 급식 정보를 가져오고, 이를 웹 페이지에 표시하는 Flask 애플리케이션을 작성하시오.

## 기능
1. Flask를 사용하여 웹 서버를 구축
2. 나이스 교육정보 개방 포털 API를 사용하여 급식 정보를 가져오고
3. 가져온 정보를 HTML 템플릿을 통해 표시
4. 메뉴 항목을 구분하여 리스트 형태로 보여줍니다.(가능하면)

## 기본 코드
```python
from flask import Flask, render_template
import requests
import json

app = Flask(__name__)

def get_meal_info():
    # API URL과 파라미터를 설정
    url = "______"  # TODO: API URL을 입력하세요
    params = {
        'KEY': '______',  # TODO: 발급받은 API 키를 입력
        'Type': '______',  # TODO: 응답 형식을 지정
        'pIndex': 1,
        'pSize': 10,
        'ATPT_OFCDC_SC_CODE': 'F10', # 교육청 코드 고정
        'SD_SCHUL_CODE': '7380042', # 학교 코드 고정
        'MLSV_YMD': '' # TODO : 날짜 date 사용하여 당일 급식 가져오게 가능하게 할것
    }
    response = requests.get(url, params=params)
    if response.status_code == 200:
        data = response.json()
        print(data)
        return data['mealServiceDietInfo'][1]['row'][0]
    return None
    # TODO: API 요청을 보내고 결과를 처리하는 코드 (이미 적어둠 작동 원리 분석해서 이해할것)

@app.route('/')
def home():
    # TODO: 급식 정보를 가져오고 템플릿에 전달하는 코드 작성 필요
    pass

if __name__ == '__main__':
    app.run(debug=True)
```

## 템플릿 코드 (meal.html)
```html
<!DOCTYPE html>
<html>
<head>
    <title>급식 정보</title>
</head>
<body>
    <h1>{{ date }} 급식 메뉴</h1>
    <!-- TODO: 메뉴 항목을 표시하는 코드를 작성하세요 -->
</body>
</html>
```

## 해결 방법
1. API URL과 필요한 파라미터를 설정 <-- 이미 해뒀음
2. requests 라이브러리를 사용하여 API 요청 전송
3. 응답 데이터를 파싱하여 필요한 정보를 추출
4. 추출한 정보를 템플릿에 전달하여 화면에 표시

## 참고
- API 응답은 JSON 형식입니다.
- 메뉴 항목은 '<br/>' 문자열로 구분되어 있습니다.

## 출력 예시
```
2024년 11월 12일 급식 메뉴
- 백미밥
- 미역국
- 제육볶음
- 김치
- 요구르트

칼로리: 738 Kcal
```
