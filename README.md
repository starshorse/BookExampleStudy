# BookExampleStudy
책에 있는 내용을 실습한 내용을 정리.


# 예제 코드 다운로드 
https://github.com/Jpub/JSWebCrawler 

## VirtualBox 인스톨 ##
## Vagrant > Download ##
https://www.vagrantup.com/downloads.html 
## 가상 머신 추가 -> 디렉토리 만들기 ## 
vagrant init 
## Vagrantfile 편집 ##
#config.vm.box ="base"  
config.vm.box = "puphpet/centos65-x64" 
>vagrant up ( vagrant up --provider virtualbox ) 
>vagrant status
## default  ID/PW vagrant / vagrant ##   
vagrant ssh 
## Node.js 설치 
   1. nvm 설치 - 재 로그인 

##
$curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.25.3/install.sh | bash 
$nvm install v0.12.4 
$nvm alias default v0.12.4 
$node -v 
$node 
>.exit
## nvm 를 sudo 명령과 함께 사용하게 하기 
$sudo visudo 
## 환경 설정 파일 변경 ## 
## 첫번쨰 수정(env_reset 무효화 ) 
Default env_reset -> #Default env_reset
## 두번째 수정(HOME을 추가 ) 
#Default env_keep +="HOME" -> Default env_keep +="HOME"
### 세번쨰 수정( sudo 명령어 실행시 사용할 패스를 덮어 쓰지 않도록 주석 처리한다. ) 
Defaults secure_path = /sbin;/bin;/usr/sbin;/usr/bin -> # Defaults secure_path = /sbin;/bin;/usr/sbin;/usr/bin
## git 설치 ## 
$sudo yum install git 
## 가상 머신에서 웹서버를 사용하기 위한 설정 
   Vagrantfile에 다음 내용을 추가 한다.
##  
config.vm.network "forwarded_port", guest:80, host:8080
config.vm.network "private_network", "192.168.33.10"
config.vm.synced_folder "../data", "/vagrant_data"

$vagrant reload 

## 공 유 에러 발생시 ## 
$sudo /etc/init.d/vboxadd setup 
$vagrant plugin install vagrant-vbguest

## Node.js 모듈 설치 ## 
$npm install request 
## 모듈을 글로벌 하게 설치 
$ npm install -g ( 모듈 이름 ) 
## 관리자 권한으로 설치 
$sudo npm install -g ( 모듈 이름 ) 
## 글로벌 설치 경로 확인 
$npm root -g 
node -e "console.log(global.module.paths)"
## 환경 변수에 등록 하기 
   ~/.bash_profile  '/home/vagrant/.bash_profile' 편집한다.## 
export  NODE_PATH=/home/vagrant/.nvm/versions/node/v0.12.4/lib/node_modules 
$sudo yum install nano 
$nano ~/.bash_profile 
# 모듈 삭제 
$ npm uninstall ( 모듈이름 )  
