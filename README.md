# FlaskBlog
Tag 설명

**V1.0: Getting Started**
* flaskblog.py 생성 (플라스크 페이지에 있는 그 내용 그대로)
* <code>pip install flask</code> 한 뒤 실행
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
* flask-wtf 추가(<code>pip install flask-wtf</code>)
* forms.py 추가(RegistrationForm, LoginForm 추가)
    * validation 추가
* Registration / Login과 관련된 html, route 추가
* app.config['SECRET_KEY'] 추가 
    * import secrets
    * secrets.token_hex(16) -> 이 값으로 넣음
* message 알람 추가

**v4.0: Database with Flask-Alchemy**
* 주의: 실행 안됨!
* flask-sqlalchemy추가 (<code>pip install flask-sqlalchemy</code>)
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

**v6.0: User Authentication**
* password hashing function 라이브러리 추가 <code>pip install flask-bcrypt</code>
* 예시
<pre>
from flask_bcrypt import Bcrypt
bcrypt=Bcrypt()
hashed_pw = bcrypt.generate_password_hash('passwd')
bcrypt.check_password_hash(hashed_pw, 'passwd')
</pre>
* 위 내용을 __init __.py에 추가함
* 저장이 잘 되었는지 확인.(sqllite에서 확인)

**v6.1**
* 위내용으로 id, email 중복입력시 db 오류 발생(unique 에러)
* id, email 중복 체크(forms.py의 RegistrationForm/validate_field에 추가)

**v6.2: flask-login을 통한 확장**
* flask-login 라이브러리 사용 <code>pip install flask-login</code>
* __init __.py 에 LoginManager 추가
* models.py에 login_manager.user_loader 추가 : User를 가져오는 기준 방법 추가, User의 상위 Class 추가(UserMixin)
  * 참고: USerMixin
    * is_authenticated등의 함수를 기본적으로 제공함
* routes.py에 login route 변경
  * email 값으로 user 정보를 가져와
  * password 체크
  * 정상 로그인이 되면 -> remember 여부를 포함해서 로그인 처리

**v6.3**
* routes.py에 로그인 한 뒤에는 login, Register를 클릭하면 메인 페이지로 이동하도록 구성
  * logout 추가
* current_user.is_authenticated 추가(대상: routes.py, layout.html)
* account.html 추가
  * routes.py에도 추가
  * layout.html에 추가
* login하지 않아도 account에 접근 가능한 문제.

**v6.4**
* login_required 추가(account)
* login페이지, 메시지 정보 추가(__init __.py)
* login_required 페이지에서 권한이 없어 login페이지로 넘어갔을 때 처리(next_page)

**v7.0: User Account and Profile Picture**
* account페이지에 이미지 추가

**v7.1**
* UpdateAccountForm 추가(forms.py, routes.py)
* Account Info 추가(account.html, routes.py)

**v7.2**
* account 페이지에 이미지 업로드 추가(account.html, routes.py)
* 업로드 이미지 축소(<code>pip install Pillow</code>)

**v8.0: Create, Update, and Delete Posts**
* post 생성 추가
  * routes.py : route 추가
  * create_post.html : 폼 추가
  * forms.py : PostForm 클래스 추가 
  * layout.html : New Post 링크 추가

**v8.1**
* DB에 저장
* 저장한 post 가져오기.

**v8.2**
* 이름, 날짜 가독성 향상/ 이미지 추가(home.html)


------------

**:) 나를 위한 참고**

tag 추가
* git add .
* git commit -m "v0.0"
* git tag v0.0 -m "v0.0"
* git push origin v0.0

tag 삭제
* git tag -d v0.0 -> 로컬에서 삭제
* git push -d origin v0.0 -> 원격에서 삭제

특정한 tag만 가져오기
* git checkout tags/v0.0

이 프로젝트만 계정 세팅
* https://help.github.com/articles/setting-your-username-in-git/

-----

**사전 준비사항**

1. Python3 설치 : https://www.python.org/downloads/
2. Bash shell + git 클라이언트 : https://gitforwindows.org/
3. CMD 확장 : http://cmder.net/
4. 개발 디렉토리 + 가상환경 구성(설치 프로그램간 충돌 방지)
<pre>
~/DEV
❯ mkdir ducksung

~/DEV
❯ cd ducksung

~/DEV/ducksung
❯ mkdir flask-2019

~/DEV/ducksung
❯ cd flask-2019

~/DEV/ducksung/flask-2019
❯ python3 -m venv venv

source venv\bin\activate #mac
venv\Script\activate #windows
</pre>

5. VSCode 설치 + python 플러그인 설치 : https://code.visualstudio.com/

6. DB Browser for SQLite : https://sqlitebrowser.org/