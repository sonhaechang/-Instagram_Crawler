## <center>Description</center>
**Instagram Crawler**는 Instagram을 크롤링하여 해쉬태그 추출합니다.

인스타그램에서 일정 수 이상의 게시물에 접근하면 게시물이 더 이상 로드되지 않습니다. (약 100~300개의 게시물을 크롤링 가능)

따라서 검색된 모든 게시글에서 해쉬태그를 추출 가능하도록 2번의 과정을 걸쳐 크롤링을 진행하게 됩니다.

1. Selenium으로 해쉬태그를 검색하고 맨 아래까지 스크롤하여 모든 게시글의 url을 추출해 엑셀로 저장합니다.  
ex) [검색한 해쉬태그]_[날짜].xlsx의 post_url이라는 sheet에 저장됨

2. 엑셀에 저장된 url을 list형식으로 가져와 Selenium로 게시물에 하나씩 접근하여 해쉬태그를 추출, 엑셀로 저장합니다.  
이때 게시글 url에 접근할때마다 횟수를 카운트해 url 엑셀(1.에서 저장한 엑셀)에 업데이트하여 게시물이 더 이상 로드되지 않아 크롤링을 못하게 되더라도 이어서 해쉬태그를 추출이 가능합니다.  
ex) [검색한 해쉬태그]_[날짜].xlsx의 tag_name이라는 sheet에 저장됨

한번에 해쉬태그를 크롤링 하는것이 아닌 2번에 걸쳐 크롤링을 하기에 시간이 좀 걸립니다.

** 2번 과정으로 일정 수 이상 게시물 접근시 429 오류 처리되어서 한동안 해쉬태그 추출이 안됩니다. 429 오류를 방지하기 위해서 한번에 최대 100개의 개시글만 접근해서 해쉬태그 추출이 됩니다.  
** 시간이 좀 걸리고 번거로워도 사용할때 2번 과정을 시간을 두고 여러번 2번 방식을 돌리는 것을 권장합니다. (만약 429 오류가 발생하면 시간을 두고 기다렸다가 다시 시도헤보세요.)

## <center>Get Started</center>

`pip install -r requirements.txt` 로 패키지를 설치
(Python 3.10.0 사용)

본인이 사용하는 크롬 버전을 확인 후 동일한 버전의 크롬 드라이버를 설치해서 driver 폴더에 추가해주세요.  
[크롬 드라이버 다운로드](https://chromedriver.chromium.org/downloads)

그리고 2가지 방법중 하나를 선택해서 Instagram Crawler 실행합니다.

1. 게시물 url 추출부터 해쉬태그까지 추출하기  
`python main.py --id=[user_id] --password=[user-password] --hash_tag=[hash_tag]`

2. 저장된 url에서 해쉬태그만 추출하기  
`python main.py --id=[user_id] --password=[user-password] --crawling_option=2 --file_name=[file_name]`

좀 더 자세한 실행 옵션 확인을 원하시면 `python main.py -h` 확인해주세요.

** 인스타그램에서 주기적으로 html 구조나 css 변경 및 크롤링을 막기위한 패치 및 업데이트를 하는 것 같습니다. 해서 사용중 문제가 생겨서 안되는 경우가 종종 발생 할 것으로 예상됩니다.
** 문제를 발경하면 최대한 다시 사용 가능하게 코드 수정을 하겠지만 자주 확인은 못하기 때문에 사용중 문제가 발생하면 알려주세여.