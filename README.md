# FlaskBlog
Tag 설명

**V1.0**
* flaskblog.py 생성 (플라스크 페이지에 있는 그 내용 그대로)
* venv에서 pip install flask 한 뒤 실행
* python3 flaskblog.py

**V2.0**
* render_template 추가(templates 폴더에 html 추가)

**v2.1**
* tempate에 파라메터 추가
* if ~ endif / for ~ endfor 추가

--------------
css 제거한 내용 추가

**v2.2-css**
* template extends 추가(layout.html)

**v3.0-css**
* flask-wtf 추가(pip install flask-wtf)
* forms.py 추가(RegistrationForm, LoginForm 추가)
    * validation 추가
* Registration / Login과 관련된 html, route 추가
* app.config['SECRET_KEY'] 추가 
    * import secrets
    * secrets.token_hex(16) -> 이 값으로 넣음