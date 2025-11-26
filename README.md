### 1️、删除旧证书
certutil -d sql:$HOME/.pki/nssdb -D -n "AnyProxy Root CA"
###### 确认删除成功：

certutil -d sql:$HOME/.pki/nssdb -L

### 2、重新导入（正确的信任参数）
certutil -d sql:$HOME/.pki/nssdb \
  -A -t "CT,C,C" \
  -n "AnyProxy Root CA" \
  -i ~/.anyproxy/certificates/rootCA.crt
###### 再查一次：
certutil -d sql:$HOME/.pki/nssdb -L
###### 你应看到：
AnyProxy Root CA   CT,C,C 或 AnyProxy Root CA   u,u,u

### 3、启动Chrome
google-chrome --user-data-dir=/home/ubuntu/chrome-profile-anyproxy     --proxy-server="http://127.0.0.1:8001"

### 4、build web
```
cd web && npx webpack --config webpack.config.js
```