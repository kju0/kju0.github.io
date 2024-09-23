ufw 는 inactive

ufw
iptables
firewalld


nginx을 이용해서 포트포워딩을 할 때 만약 연결이 안된다?
1. listen 여부 확인
	`sudo netstat -tuln | grep 1236`
2. nginx 로그 확인
	`/var/log/nginx/error.log` `/var/log/nginx/access.log`
	`/usr/local/nginx/logs/error.log` `/usr/local/nginx/logs/error.log` 
3. 현재 서버로 연결 잘 들어오는지 확인
	```shell
	sudo tcpdump -i any port 1236
	```
4. 잘 들어온다면 이제 방화벽 의심하기
	- firewalld, iptables 시도했던 기록
	```shell
	sudo iptables -L
	sudo iptables -A INPUT -p tcp --dport 1236 -j ACCEPT

	#firewalld 작동 중이면 적용 안될 수 있음
	sudo systemctl stop firewalld
	sudo systemctl disable firewalld
	sudo iptables-save
	sudo apt-get install iptables-persistent
	sudo service iptables-persistent save

	#firewalld 다시 실행
	sudo systemctl start firewalld
	sudo systemctl enable firewalld
	
	sudo firewall-cmd --permanent --add-port=1236/tcp
	sudo firewall-cmd --reload
```

