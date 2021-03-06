회원관리 beta_2 release

배포처 : http://www.webweaver.pe.kr
배포일 : 2000년 8월 31일
개발자 : 김주원 (webweaver@webweaver.pe.kr)

#-----------------------------------------------------------------------------#
1. 기능소개
   1) 회원가입, 로그인, 로그아웃
   2) 메일링 리스트 기능이 있었으나, 배포버전에선 뺐음.

2. 라이센스
   1) 자유롭게 수정 재배포 가능하지만, 원작자님들의 허락을 받아야 함.
   2) 상업적인 용도로는 사용할 수 없음.
   3) 재 배포시는 반드시 하단의 라이센스 링크를 유지해야 함.

3. 알려진 문제점.
   1) 목록보기에서 검색시 이름으로 검색되지 않음..
      * 회원 id가 data파일 이름이어서 문제발생..
      * 기존의 프로그램은 회원이름을 data파일 이름으로 사용했음.
      * data파일을 각각 읽어서 이름으로 검색가능하지만 비효율적임.
   2) 보안문제가 많음.
      * 일부 검색엔진에서는 data 디렉토리의 내용들까지 긁어감.
      * 원래 개발자는 회원에게 날씨정보와 바이오리듬을 제공하기 위해 개발했기
        때문에 이로 인해 발생하는 문제에는 책임지지 않음.

4. 설치법
   1) 압축을 푼다. 
   2) 펄경로를 수정한다.
   3) member.cgi파일을 열어서 수정부분을 수정한다. 
   4) mailer.config 파일을 수정한다. (폼메일 사용하실 분만...)
   5) 서버에 업로드한다.
   6) 퍼미션 지정
      chmod 777 member
      cd member
      chmod 777 data
      chmod 777 data/*
      chmod 777 photos
      chmod 777 *.txt
      chmod 777 *.config
      chmod 755 *.cgi
      chmod 755 *.pl
      chmod 777 *.config
   7) 제공한 login_form.htm 파일을 열어서 로그인 폼을 넣을 페이지에 삽입한다.
****중요****
   8) 이미 개발자가 관리자 id : admin pass : 1234로 관리자 정보를 만들어 놓았다.
      로그인한다. 여기에 회원가입을 한 관리자의 id 는 member.cgi에서의 $admin_id = "admin";
      와 일치해야 한다. 그렇지 않으면 회원리스트를 볼 수 없다.
   9) success.htm 파일이 나오면 회원관리를 클릭하여 관리자 정보를 변경한다.
   10) success.htm 파일의 내용을 적당한 페이지에 붙여 넣는다.

5. 이상, 허접한 회원관리 프로그램 설명이었습니다.

6. 수정할 내용이나 버그등은 알려 주시면 수정 재배포하겠습니다.

7. 설치에 문제가 있으신 분은 제홈페이지 묻고 답하기 게시판을 이용해 주세요.


###########     주소록 family.cgi ver1.0.4 & KnDolMailer Ver 1.0    ###########
###                                                                         ###
### 배포자 : 김대석 (kndol@kndol.sarang.net)                                ###
###                                                                         ###
### 주소록 스크립트는 sepal님이 만드신 스크립트를 수정한 것입니다.          ###
### 세팔님의 원본은 http://sepal.woorizip.com/ 에서 찾으실 수 있습니다.     ###
### 이 스크립트는 원본과 데이터 구조나 많은 부분이 다르기 때문에 호환이     ###
### 되지 않습니다. 기존 세팔님의 소스를 사용하시던 분들은 유의하시기        ###
### 바랍니다.                                                               ###
###                                                                         ###
###############################################################################
###                                                                         ###
### 메일러 스크립트에 사용된 이미지의 대부분은 위키 소프트의                ###
### WeekyMailer에서 가져 왔습니다.                                          ###
### 레이아웃은 위키 메일러를 참조하였습니다.                                ###
### 이미지와 레이아웃을 사용할 수 있도록 허락해 주신 위키 소프트 측에       ###
### 감사 드립니다.                                                          ###
### 위키 소프트의 주소는 http://weeky.pr.co.kr 입니다.                      ###
###                                                                         ###
###############################################################################
###                                                                         ###
### 알려진 문제 :                                                           ###
###     NT서버에서 EMWAC의 IMS를 SMTP 서버로 사용시 가끔씩 소켓 연결에      ###
###   실패했다는 에러가 납니다. 이유는 제가 SMTP 서버의 프로토콜을 깊게     ###
###   연구해 보지 못한 관계로 아직 찾지 못했습니다.                         ###
###   이 문제에 대한 해결 방안을 아시는 분은 연락 주시기 바랍니다.          ###
###                                                                         ###
###############################################################################
###                                                                         ###
### 이 스크립트는 http://kndol.sarang.net/~CgiMaker/ 에서 다운로드          ###
### 받으실 수 있습니다.                                                     ###
###                                                                         ###
### 상업적 목적이 아니라면 수정 및 재배포는 자유입니다.                     ###
### 수정 및 재배포시 가급적이면 원본을 밝혀주시면 감사하겠습니다.           ###
### 그리고, 에러 수정이나 개선 시에는 제가 참고할 수 있도록 알려 주시면     ###
### 아주 고맙지요.                                                          ###
###                                                                         ###
###############################################################################
###                                                                         ###
###            *************************************************            ###
###            *          Fight and Posses the Land!           *            ###
###            *                - Deut 2:24 -                  *            ###
###            *************************************************            ###
###            * Homepage : http://kndol.sarang.net/           *            ###
###            *          : http://kndol.sarang.net/~CgiMaker/ *            ###
###            * e-mail   : kndol@kndol.sarang.net             *            ###
###            *************************************************            ###
###            *                                               *            ###
###            *   ______ __        ________        ______     *            ###
###            *   ___  //_/_______ ___  __ \______ ___  /     *            ###
###            *   __  ,<   __  __ \__  / / /_  __ \__  /      *            ###
###            *   _  /| |  _  / / /_  /_/ / / /_/ /_  /       *            ###
###            *   /_/ |_|  /_/ /_/ /_____/  \____/ /_/        *            ###
###            *                                               *            ###
###            *************************************************            ###
###                                                                         ###
###                                                  2000. 4. 18, KnDol     ###
###                                                                         ###
###############################################################################

##[ 간편 버전 ]################################################################
간편 버전은 아무 생각 없이 업로드와 권한 설정만 해서 쓸 수 있도록 한 것입니다.
만약 자동 설정이 잘 안되거나 수동으로 설정해야 할 사항이 있으면 이 파일이 있는
디렉토리의 설정 파일(family.config, KnDolMailer.config)를 적절히 수정해서 상위
디렉토리로 복사하시면 됩니다.
스크립트 자체는 일반 버전과 같습니다. 다만 설치하기 쉽도록 디렉토리 구조만
정리한 것입니다.

##[ 달라진 점 ]################################################################
** 버전 1.0.4 (2000. 4. 20)
아주 약간의 기능 추가와 버그 때치가 있습니다. 좀더 많은 기능의 개선이 있은 후에
배포하려고 했으나 치명적인 버그로 새로 올립니다.
(치명적인 버그는 여러 배포본을 관리하다보니 쉬운 설치 버전에 들어 있는 큰돌
메일러가 이전 버전이 들어있는 문제입니다. 죄송합니다.

** 버전 1.0.2 (2000. 4. 18) : 배포 하루도 안 되서 새버전을 만들었습니다.

1. 학번을 4자리 또는 2자리로 표시할 수 있도록 했습니다.

2. family.config가 없거나 내용 중 설정하지 않은 항목이 있을 때는 자동 선택되도록 했습니다.

3. 특수 학번(교수 등) 설정 기능 추가

4. 작은 버그들을 수정했습니다.

** 버전 1.0.1 (2000. 4. 17)
1. 세팔님의 소스를 수정한 버전 첫 릴리즈

2. 사진 올리기 기능

3. 프로필 상세 보기 기능


##[  설치법  ]#################################################################

압축을 푸신후 cgi-bin 디렉토리의 family.config를 수정하세요.
그런 다음 전체를 홈디렉토리에 올리시고 퍼미션을 수정하시면 됩니다.
그림 파일들은 Binary모드로 txt파일과 cgi, pl, db파일은 ascii모드로 올리셔야 합니다.

가능하면 cgi-bin 밑의 디렉토리에 있는 파일들은 홈디렉토리/cgi-bin 에 설치하시길 권합니다.
이건 강요는 아니지만 제 CGI들은 이 룰에 따르도록 기본 설계되어 있습니다.

1. family.config 설명
	$gMainDir  = "/..../홈디렉토리/web-home/family";
			-> family 디렉토리의 절대 경로입니다. 절대 경로를 정확히 모르면
			   cgi-bin 디렉토리의 pwd.cgi를 브라우저에서 실행해 보세요.
			   설정하지 않으면, 스크립트가 있는 위치를 사용
	$gMainUrl  = "http://myhome/family";
			-> 위 family 디렉토리의 URL입니다.
			   설정하지 않으면, 스크립트가 있는 위치를 사용
	$gImageUrl = "$gMainUrl/images";
			-> 아이콘 및 이미지가 있는 위치의 URL입니다. 일반적으로 수정할 필요 없습니다.
			   설정하지 않으면 스크립트가 있는 디렉토리 및의 images로 간주


2. KnDolMailer.config 설명
		$gMailOS = "UNIX";
			-> NT 또는 UNIX로 이 CGI가 설치된 서버의 OS 종류를 적습니다. 만약 $gMailOS = ""; 로 하면 자동 선택을 합니다.
			   자동 선택이 지원되지 않는 서버도 가끔 있으므로 서버의 OS 종류를 정확히 안다면 적으시는 것이 좋습니다.

		$gMailUrl = "http://yourhome/KnDolMailer";
			-> KnDolMailer의 그림 파일들이 있는 곳의 URL

		$gMailDir = "/..../홈디렉토리/web-home/KnDolMailer";
			-> KnDolMailer의 환경 설정 파일이 저장될 디렉토리의 절대 경로를 적습니다.

		$gRootMail = 'webmaster@yourhost';
			-> 이 부분은 중요한 부분은 아닙니다.
			   서버 에러시 서버 관리자에게 통보하라는 메시지를 내보낼 때 사용됩니다.
			   서버의 관리자(보통 root나 webmaster의 계정을 가집니다.)의 메일을 적으시면 됩니다.
			   잘 모르면 자기의 메일 주소를 적으셔도 무방합니다.


3. 파일 퍼미션: (NT에서는 필요 없음)
		chmod 777 data       (data 디렉토리)
		chmod 777 photos     (사진 저장 디렉토리)
		chmod 755 images     (그림 파일이 있는 디렉토리)
		chmod 755 *.cgi *.pl *.pm
		chmod 644 *.db


4. 업로드 후, data 디렉토리와 photos 디렉토리의 '업로드 후 반드시 지우세요.txt' 파일을
   반드시 지우셔야 합니다.


5. http://myhome/family_ez/family.cgi 해서 불러 보시면 됩니다.


6. 메일러는 http://myhome/family_ez/KnDolMailer.cgi 입니다.


7. 주소록은 로고를 클릭하시면 관리자 모드로 접속하실 수 있습니다.


  *****************************************[광고]*****************************************
  이 소스를 수정하여 자기홈에 올리시려면 분명히 출처를 밝히셔야 합니다.
  그게 원작자에 대한 예의죠... ^.^
  또한 부족한 실력으로 완전치 못한 부분이 있을수 있으니 그러한 점을 발견하신 분이나
  더 좋게 소스를 수정하신 분은 꼭 연락해 주세요... 서로 좋게 좋게 만들어 가자 구요... ^.^
  *****************************************************************************************
