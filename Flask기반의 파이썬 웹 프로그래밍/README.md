//Python Web Programming with Flask.

/* 파이썬 통합 개발 환경 구성 Python 3.6 기준 * /
https://www.jetbrains.com/pycharm/

/* 가상 환경 구성 */ 
C:\>pip install virtualenv   /* 설치 */
C:\>workspace\python>virtualenv ProjectEnv  /* 구동하기 */ 
C:\>workspace\python>cd ProjectEnv\Scripts   <br> 
C:\>workspace\python\ProjectEnv\Scripts>activate <br> 
D:\#Python\tstprj\Scripts>activate <br> 

(tstprj) D:\#Python\tstprj\Scripts>python
Python 3.6.4 (v3.6.4:d48eceb, Dec 19 2017, 06:54:40) [MSC v.1900 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> ^Z
(tstprj) D:\#Python\tstprj\Scripts>deactivate
D:\#Python\tstprj\Scripts>

/* Flash 설치 */ 
D:\#Python>pip install flask
Collecting flask
  Downloading Flask-0.12.2-py2.py3-none-any.whl (83kB)  <br> 
    100% |████████████████████████████████| 92kB 456kB/s  <br> 
Collecting Werkzeug>=0.7 (from flask)
  Downloading Werkzeug-0.14.1-py2.py3-none-any.whl (322kB)  <br> 
    100% |████████████████████████████████| 327kB 1.0MB/s  <br> 
Collecting Jinja2>=2.4 (from flask)
  Downloading Jinja2-2.10-py2.py3-none-any.whl (126kB  <br> 
    100% |████████████████████████████████| 133kB 2.4MB/s  <br> 
Collecting itsdangerous>=0.21 (from flask)
  Downloading itsdangerous-0.24.tar.gz (46kB  <br> 
    100% |████████████████████████████████| 51kB 1.6MB/  <br> 
Collecting click>=2.0 (from flask)  <br> 
  Downloading click-6.7-py2.py3-none-any.whl (71kB  <br> 
    100% |████████████████████████████████| 71kB 1.1MB/s  <br> 
Collecting MarkupSafe>=0.23 (from Jinja2>=2.4->flask)  <br> 
  Downloading MarkupSafe-1.0.tar.gz
Installing collected packages: Werkzeug, MarkupSafe, Jinja2, itsdangerous, click, flask
  Running setup.py install for MarkupSafe ... done
  Running setup.py install for itsdangerous ... done
Successfully installed Jinja2-2.10 MarkupSafe-1.0 Werkzeug-0.14.1 click-6.7 flask-0.12.2 itsdangerous-0.24
/* PostgreSQL 9.4 설치 */ 
/* GitLab 설치 */ 


/* 파이썬 내장 웹서버 구동하기 */ 
D:\#Python>python -m http.server 8080
Serving HTTP on 0.0.0.0 port 8080 (http://0.0.0.0:8080/) ...


http://localhost:8080/ /* 웹 브라이우저에서 확인하기 */ 
