vpc : 사용자가 정의하는 가상의 네트워크 (192.168.171.0/24)
- public subnet 1 : 192.168.171.0/26
- public subnet 2 : 192.168.171.64/26
- admin subnet 1 : 192.168.171.128/27
- private subnet 1 : 192.168.171.160/27

internet gateway : vpc 리소스와 인터넷 간 통신을 활성화하는 게이트웨이

route table : 네트워크 트래픽이 전달되는 위치 제어
- public : public 1, 2, admin 1 subnet 연결
- private : private 1 subnet 연결

security group : 인바운드/아웃바운드 트래픽을 제어하는 가상의 논리적 방화벽
- public
    - 모든 IP에 대해서 80번 포트 접속 허용
    - bastion으로부터 22번 포트 접속 허용
- private
  - public으로부터 3306번 포트 접속 허용
  - bastion으로부터 22번 포트 접속 허용
- bastion : 공인 IP 1개만 22번 포트 접속 허용

ec2 : 
- tasklet1579-ec2-web : 웹 서비스
- tasklet1579-ec2-nat : 소프트웨어 업데이트 또는 운영 체제 패치
- tasklet1579-ec2-mysql : 데이터베이스
- tasklet1579-ec2-bastion : 인스턴스 접근제어
