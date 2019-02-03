# FlaskBlog
Tag 설명

**V1.0: Getting Started**
* flaskblog.py 생성 (플라스크 페이지에 있는 그 내용 그대로)
* venv에서 pip install flask 한 뒤 실행
* python3 flaskblog.py

**V2.0: Tempates**
* render_template 추가(templates 폴더에 html 추가)

**v2.1**
* tempate에 파라메터 추가
* if ~ endif / for ~ endfor 추가

**v2.2**
* template extends 추가(layout.html)
* css 추가(static 폴더에 추가)

**v3.0: Forms and User Input**
* flask-wtf 추가(pip install flask-wtf)
* forms.py 추가(RegistrationForm, LoginForm 추가)
    * validation 추가
* Registration / Login과 관련된 html, route 추가
* app.config['SECRET_KEY'] 추가 
    * import secrets
    * secrets.token_hex(16) -> 이 값으로 넣음
* message 알람 추가

**v4.0: Database with Flask-Alchemy**
* 주의: 실행 안됨!
* flask-sqlalchemy추가 (pip install flask-sqlalchemy)
* sqlite browser : https://sqlitebrowser.org/dl/
* flaskblog.py에
    * SQLAlchemy 추가
    * User class 추가
* 다음 작업을 순서대로 진행

```
from flaskblog import db #DB 접근
db.createall() #site.db 생성

from flaskblog import User, Post

#사용자생성
user1 = User(username='Corey', email='C@demo.com', password='password') 
user2 = User(username='JohnDoe', email='jd@demo.com', password='password') 

#DB에 저장
db.session.add(user1)
db.session.add(user2)
db.session.commit() 

#검색
User.query.all()
user = User.query.get(1)

#Post 생성
post1 = Post(title='Blog 1', content='First Post Content!', user_id=user.id)
post2 = Post(title='Blog 2', content='Second Post Content!', user_id=user.id)
db.session.add(post1)
db.session.add(post2)
db.session.commit()

#데이터베이스 삭제/재생성
db.drop_all()
db.create_all()
```
**v5.0: Package Structure**
* 주의: 실행 안됨!
* User, Post를 models.py로 이동
    * 하지만, flaskblog.py에서 호출하면 순환호출이 발생, 정리가 필요.

**v5.1**
* flaskblog폴더 추가 (모든 파일/폴더를 옮김 단, venv/__ pycache__ 제외 )
    * import / db 세팅 -> __ init__.py 로 이동
    * route 관련 -> routes.py로 이동
    * 위쪽 폴더에 run.py 추가



**:) 나를 위한 참고**

tag 추가
* git add .
* git commit -m "v0.0"
* git tag v0.0 -m "v0.0"
* git push origin v0.0

tag 삭제
* git tag -d v0.0 -> 로컬에서 삭제
* git push -d origin v0.0 -> 원격에서 삭제
