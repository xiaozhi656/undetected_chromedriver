# undetected_chromedriver
本地自动化工具部署web网站镜像
# 使用方法  
## docker-compose.yml文件  
```version: '3'  
services:  
  auto-driver:  
    image: xiaozhi696/undetected_chromedriver:latest  
    volumes:  
      - "${APP_PATH}:/var/app"  
    ports:  
      - "6080:6080"  
    working_dir: /var/app  
    environment:  
      VNC_PASSWORD: ${VNC_PASSWORD}  
    networks:  
      - auto_network  

networks:  
  auto_network:  
    external: True  
```
## .env 文件

```
APP_PATH=你的程序地址  
VNC_PASSWORD=你的novnc密码  
```
## python 程序
### 指明chrome 运行窗口  
```os.environ["DISPLAY"] = ":99"```  
### 指明chromedriver地址 
``` 
import undetected_chromedriver as uc  
from selenium.webdriver.chrome.options import Options 
op = Options()  
driver = uc.Chrome(driver_executable_path='/usr/bin/chromedriver', options=op)  
```
## 创建网络  
```
docker network create auto_network 
```
## 运行容器  

```
docker-compose up -d
```  
## 运行程序  
```
docker-compose exec auto-driver xvfb-run -a python main.py  
```

