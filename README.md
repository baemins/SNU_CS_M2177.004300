# 서울대학교 컴퓨터공학부 M2177.004300 딥러닝의 기초 실습

수업의 실습을 위한 딥러닝 Infrastructure의 설정과 MNIST 예제 실습을 다룹니다. 

수강생을 위한 Azure credit은 TA에게 문의하여 주십시오.

사전 설치 프로그램: Jupyter Nodebook

## 목차

Cloud 사용 / GPU Instance 설정 / MNIST 예제의 3부분으로 나뉘어 있습니다.

### Cloud 사용
[1. Azure 접속을 위한 Microsoft ID 생성](#Ch1)

[2. Azure 구독 확인](#Ch2)

[3. Azure 기초](Ch3)

### GPU Instance 설정
[4. Azure에서 Linux GPU Virtual Machine 생성 (Data Science Virtual Machine)](#Ch4)

[5. VM 접속 및 GUI 사용 설정 (Remote desktop client 설치 및 연결)](#Ch5)

[6. Jupyter Hub의 연결](#Ch8)

[7. GPU/CPU 비교](#Ch7)

[8. Python 버전 설정(Option)](#Ch6)

### MNIST 예제
[9. MNIST 예제 실습](#Ch9)

<a name="Ch1"></a>
## 1. Azure 접속을 위한 Microsoft ID 생성

(이미 계정이 있는 분들은 생략하여 주십시오.)

먼저, Microsoft의 Cloud서비스인 Azure를 사용하기 위한 계정생성이 필요합니다. [가입페이지](https://account.microsoft.com/account?lang=en-US)를 방문하여 계정을 생성하여 주시기 바랍니다.

![Microsoft Account Page](Images/Microsoft_signin.png)

'Sign in with Microsoft'를 클릭하십시오.

![Microsoft Account Creation](Images/CreateAccount.png)

'Create One'을 클릭하십시오.

Microsoft ID는 Microsoft의 서비스 이용을 위한 계정으로, outlook외에도 다른 이메일 계정(naver, gmail 등)으로 자유롭게 가입할 수 있습니다.

가입을 마치면, 구독을 부여받기 위해 TA에게 해당 계정을 제출하여 주십시오.

<a name="Ch2"></a>
## 2. Azure 구독 확인

Microsoft의 Cloud 서비스, Azure에 오신 것을 환영합니다. 여러분의 TA는 실습을 위해 사용할 수 있는 구독에 대한 접근을 부여해 주었을 것입니다. Azure의 Portal에서 이를 먼저 확인해 주십시오. 먼저 [Azure Portal](https://portal.azure.com)에 접속하여 주시기 바랍니다. 

왼쪽의 메뉴 하단에 '구독' 혹은 'Subscriptions' 메뉴를 확인하여 주십시오.
![Subscription Button](Images/subscriptionmenu.png)

구독명을 클릭하여 부여받은 credit을 확인하여 주십시오. **한정된 자원**을 사용해야 하기에 실습을 진행하실 때 항상 잔액을 확인하여 주시기 바랍니다.

이미 Azure를 사용해본 경험이 있으시다면, 다른 여러 가지의 구독명을 보시게 됩니다. 반드시 수업용으로 제공된 구독을 사용해 주시기 바랍니다. 다른 구독을 사용하는 경우 등록한 신용카드로 과금이 발생할 수 있습니다. 수업용으로 제공하는 구독은 과금이 발생하지 않습니다.

<a name="Ch3"></a>
## 3. Azure 기초

축하합니다. 이제 여러분은 Microsoft의 Azure의 다양한 리소스를 이용할 수 있는 구독의 사용권을 받았습니다. Azure Portal은 이러한 다양한 서비스를 이용하고 관리할 수 있는 툴입니다. 

좌측의 즐겨찾기 메뉴를 통해 자주 사용하는 리소스를 편하게 접근할 수 있습니다. 생성한 리소스를 대시보드화하여 한눈에 모니터링하는 편리한 기능도 지원합니다.
[Azure Portal Introduction](https://azure.microsoft.com/ko-kr/features/azure-portal/) 페이지를 방문하여 더 자세한 정보를 얻으실 수 있습니다.

<a name="Ch4"></a>
## 4. Azure에서 Linux GPU Virtual Machine 생성 (Data Science Virtual Machine)

이제 실습을 위해 많은 연산을 수행할 GPU가 탑재된 Virtual Machine을 Azure Data Center 내에 생성해보도록 하겠습니다. Azure에서는 Windows/Linux의 OS가 설치된 가상머신(Virtual Machine)을 쉽게 배포할 수 있습니다. 금번 수업을 위해서는 OS 외에 추가로 Machine Learning을 위한 다양한 툴킷을 포함하고 있는 [Data Science VM](https://azure.microsoft.com/ko-kr/services/virtual-machines/data-science-virtual-machines/) 이미지를 사용합니다. 이를 통해 툴킷 설치에 필요한 많은 시간을 절약할 수 있습니다. Data Science VM은 아래의 툴킷을 포함하고 있습니다.

Anaconda Python 2.7, 3.5 / Microsoft R Open / Jupyter Notebook Server / Jupyter Notebook Hub / Visual Studio Code / Atom / Vim / Git / Tensorflow / Caffe & Caffe2 / Torch / Keras / CUDA

Azure에서 새로운 리소스 생성을 위해서 좌상단의 'Create a resource'를 클릭하십시오. 이후 나오는 검색 창에 'data science virtual machine'을 타이핑하면 아래와 같이 옵션이 보일 것입니다. Data Science Virtual Machine for Linux(Ubuntu)를 선택하십시오. 

![vmcreation](Images/vmcreation.png)

해당 VM 이미지에 대한 설명이 나오고 하단의 'Create' 버튼을 클릭하여 다음 단계로 진행합니다.

1. Basics

해당 화면에서는 여러분의 VM의 기초 설정을 할 수 있습니다. 

Name은 앞으로 Azure 내에서 여러분의 VM을 식별하기 위한 이름입니다. 예제에서는 'MyFirstVM'으로 진행합니다. 

VM Disk Type: HDD로 변경하여 주십시오.

User Name: 여러분의 Ubuntu에 로그인하기 위한 사용자 계정입니다. 생성후 잘 기억해 두십시오.

Authentication type: SSH 방식과 Password방식을 모두 지원합니다. 실습시나리오에서는 Password방식을 사용합니다. 대문자/소문자/숫자/특수문자 중 3가지 이상으로 12자리 이상을 이용해야 합니다. 마찬가지로 생성후 잘 기억해 두십시오. 

Subscription: 반드시 TA에게 받은 구독이름이 맞는지 확인하여 주십시오.

Resource Group: 다양한 리소스를 한데 모아 관리할 수 있게 해주는 논리적 그룹입니다. 실습 편의를 위해 'create new' 선택후 'MyFirstRG'을 사용합니다.

Location: GPU 사용을 위해 'West US 2'를 선택하여 주십시오.

![VM Basic](Images/vmbasic.png)

2. Size

이 곳에서는 여러분이 사용할 VM의 크기를 고를 수 있습니다. Azure에서는 용도에 맞게 쓸 수 있도록 다양한 규격의 VM을 제공하고 있습니다. 

Compute Type: GPU를 선택하십시오.

이제 하단에 여러분이 사용가능한 GPU Instance의 목록이 보입니다. NC6를 선택한 후 하단의 'Select' 버튼을 클릭하여 주십시오. NC시리즈는 머신러닝을 위한 연산에 특화한 GPU를 사용하고 있으며, NV는 비전처리에 특화되어 있습니다. GPU에 대해 좀더 자세히 알고 싶으신 분은 [Nvidia](https://www.google.co.jp/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0ahUKEwir6fb9v4HaAhWMoZQKHR_DC2IQFggpMAA&url=http%3A%2F%2Fwww.nvidia.com%2Fobject%2Ftesla-k80.html&usg=AOvVaw2UM_jLQqiHuJCYjUPaO71G)의 홈페이지를 방문해보시기 바랍니다.

3. Settings

이 곳에서는 고급 활용을 위한 환경 설정을 합니다. 금번 실습에서는 필요하지 않은 설정이니 Default를 유지한채 하단의 'OK'를 클릭하여 주십시오.

- Availability Set: 복수의 Instance를 이용하여 항상성을 유지하기 위한 설정입니다.
- Virtual Network: 클라우드 내에 가상 네트워크를 구축합니다.
- Subnet: 가상 네트워크 내의 Subnet 설정입니다.
- Public IP address: 여러분의 VM에 공용 IP를 부여하기 위한 설정입니다.
- Network Security Group: 보안을 위한 방화벽 설정입니다.

4. Create 

이제 모든 과정을 마쳤으며, 하단의 동의 박스 체크와 Create 버튼 클릭을 통해 최종 작업을 수행합니다.
버튼 클릭후 우상단에서 과정을 안내하며 약 4-5분 정도후 여러분의 첫 번째 Virtual Machine이 준비됩니다.


<a name="Ch5"></a>
## 5. VM 접속 및 GUI 사용 설정

배포를 성공적으로 마치면 이제 여러분의 대시보드 바탕화면에 아래와 같이 생성한 VM이 나타납니다.해당 아이콘을 클릭하여 자세히 살펴봅니다.

![runningvm](Images/runningvm.png)

아이콘을 클릭하면 여러분의 VM에 대한 자세한 정보를 표시합니다. 상단에서는 VM의 상태를 control할 수 있습니다. 재시동을 위한 Restart버튼과 중지를 위한 Stop 버튼을 확인하여 주십시오. 중간의 Public IP에서 여러분의 VM이 할당받은 IP를 확인하십시오. 하단에서는 상태를 모니터링할 수 있습니다. 이제 상단의 Connect를 클릭하십시오.

-------------
## Credit 관리를 위한 VM 사용팁

GPU Instance는 고가의 자원이며, 수업용으로 제공하는 credit에는 제한이 있습니다. 딥러닝 연구 목적 특성 상 사용하지 않을 때는 반드시 Stop 버튼으로 VM의 사용을 중지하여 주십시오. Cloud 환경이기에 사용한 만큼만 지불을 하면 됩니다. Azure VM은 분당 과금체계이므로 사용한 분에 비례하여 credit이 차감됩니다. 따라서 실습을 마치면 반드시 Stop 버튼으로 VM의 시동을 꺼주십시오. 이후 다시 사용할때에는 Start 버튼을 통해 다시 시작할 수 있습니다. 

------------

VM에 대한 접근은 Putty나 Bash Shell 등을 이용할 수도 있습니다. 여기서는 Azure Portal내에서 제공하는 Cloud Shell을 통해 연결을 확인해봅니다.

![CloudShell](Images/cloudshell.png)

우상단의 '>_' 모양 아이콘을 클릭하여 Cloudshell을 실행합니다. 하단에서 Bash Shell과 Powershell 가운데 Bash Shell을 선택하고, Shell 작업을 저장할 저장소를 생성하여 주십시오. 이제 Portal 내에서 Shell 명령어를 실행할 수 있습니다.

하단의 Shell에서 이제 VM 접속을 위해 'ssh 생성한admin@부여받은IP'를 입력하십시오. (상단의 connect 버튼을 클릭하면 보입니다.) 비밀번호 입력을 거치고 나면 이제 Ubuntu 머신을 이용할 수 있습니다.

### Linux Virtual Machine 사용시 주의사항

Azure 상의 Linux Virtual Machine을 사용시에 temporary disk (/dev/sdb1)에는 Data를 저장하지 마십시오. 해당 disk는 OS provision시 발생하는 temporary 파일을 저장하는 논리드라이브로써 VM을 끈 이후 새로 시작하는 경우 초기화될 수 있습니다. (Windows 머신의 D드라이브도 마찬가지입니다.)


### GUI 사용 설정

커맨드 사용보다 편리한 이용을 위해 GUI 환경설정을 합니다. 여러분의 로컬 환경에 Client 소프트웨어를 설치해야 합니다. [X2Go](https://wiki.x2go.org/doku.php/doc:installation:x2goclient) 홈페이지에서 사용하는 OS에 맞는 Client를 설치하여 주십시오.

이후 X2Go를 실행한 후 아래 설정을 진행하여 주십시오.

- New Session 생성
- Session탭에서 
- Host: VM의 IP
- Login: 여러분의 admin 계정
- SSH Port: 기본값 22를 사용합니다.
- Session Type: XFCE로 변경

이후 접속하고 비밀번호를 입력하고 나면, GUI 환경으로 Ubuntu를 이용할 수 있습니다. 

![Ubuntu](Images/ubuntu.png)


<a name="Ch6"></a>
## 6. Jupyter Hub 연결

DSVM을 설치한 후, 외부에서 바로 Jupyter Hub에 연결해서 사용할 수 있습니다. 기본으로 8000 포트가 제공되고 있으며

```https://해당VM의PublicIP/8000``` 으로 접속할 수 있습니다. 브라우저에서 인증문제가 발생하지만, 계속 실행시키면 로그인 창이 뜨게 됩니다.

Jupyter Hub의 ID/PW는 해당머신의 우분투에 설정했던 값을 사용하면 됩니다.

이후 Start MyServer를 클릭하면 사용할 수 있습니다.

----------------------
VM 상의 ipynb 파일의 제출/교환

Azure VM은 기본적으로 많은 보안 옵션이 설정되어 있어, 다른 서버로의 파일 전송에 또 다른 설정이 필요합니다. 가장 손쉬운 방법은 Jupyter에서 해당 파일을 로컬머신으로 다운로드하여 로컬머신에서 다른 email service 등을 이용하는 방법입니다.


<a name="Ch7"></a>
## 7. CPU/GPU 성능 비교

딥러닝에서의 GPU의 장점을 확인해보기 위하여 간단한 Python 예제코드를 실행해보고 결과를 비교해보도록 하겠습니다. 본 예제는 VM에서 직접 실행하지만, 8번의 과정 이후 Local Jupyter에서 실행해도 됩니다. 예제 실행을 통해 GPU 설정 및 인식도 함께 확인합니다.

Jupyter Hub 에서 New 선택후 'Python 3'으로 새로운 노트북을 생성합니다. 아래 코드를 붙여넣고 실행하여 주십시오.

[CPU/GPU 실행 속도 비교 코드](https://gist.github.com/3h4/f6e9cabbead201056c4705c2590d3d21#file-0-matrix-py)


<a name="Ch8"></a>
## 8. Python 버전 설정(option)

Azure의 Data Science VM은 2가지 버전의 Python을 제공하고 있으며, 사용자의 선택에 맞게 사용할 수 있습니다. 아래 설정은 2가지 버전 중 하나를 선택하여 편리하게 사용할 수 있도록 설정하는 방법을 안내합니다.

Python 2.7 버전은 /anaconda/bin에 설치되어 있습니다.

```source /anaconda/bin/activate root```

Python 3.5 버전은 /anaconda/envs/py35/bin에 설치되어 있습니다.

```source /anaconda/bin/activate py35```


<a name="Ch9"></a>
## 9. MNIST 예제 실습

![MNIST.ipynb](MNIST.ipynb)
