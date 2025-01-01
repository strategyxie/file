# docker版Chrome

## 样本1
第一步：docker pull overclockedllama/docker-chromium:latest

运行命令

docker run -itd \
    --restart=always \
    --name=chrome \
    -e TZ=Asia/Hong_Kong \
    -e DISPLAY_WIDTH=1900 \
    -e DISPLAY_HEIGHT=1080 \
    -e KEEP_APP_RUNNING=1 \
    -e ENABLE_CJK_FONT=1 \
    -e SECURE_CONNECTION=0 \
    -e VNC_PASSWORD=admin \
    -p 5800:5800 \
    -v /home/chrome_config:/config:rw \
    --security-opt seccomp=unconfined \
    --shm-size 1500m \
    langren1353/chrome-cn

停止容器：
docker stop chrome
启动容器
docker start chrome
重启容器
docker restart chrome
解释一下，
--restart=always \  ##docker重启时候自动启动容器，不要可以不添加
-e TZ=Asia/Hong_Kong \ ##这个是设置地区。
-e DISPLAY_WIDTH=1920 \
-e DISPLAY_HEIGHT=1080 \ ##设置显示的高宽
-e KEEP_APP_RUNNING=1 \ ##关闭了之后会自动重启，不然所有标签页关闭了，浏览器也就关了。
-e ENABLE_CJK_FONT=1 \ ##一定要加这个，不然中文显示乱码
-e SECURE_CONNECTION=1 \ ##启用 HTTPS，再绑定域名，安全一点点
e VNC_PASSWORD=xxxxxxxx \ ##访问密码，不然谁打开都能用了
-p 5800:5800 \ ##端口
-v /home/chrome_config:/config:rw \ ##数据，包括下载的东西，不然不好找，重装可以继续用这个目录。
--security-opt seccomp=/path/to/seccomp/profile.json \ ##配置文件默认情况下拒绝访问系统调用，不然网页会经常卡死崩溃，懒得弄的可以用 --security-opt seccomp=unconfined \，但是安全性差一些。
--shm-size 1500m \ ##内存使用，单位m或是g，建议是2g，但是500M的机器并不是不能试试看

## 样本2
docker run -itd \
    --restart=always \
    --name=chrome \
    -e USER_ID=0 \
    -e GROUP_ID=0 \
    -e TZ=Asia/Hong_Kong \
    -e DISPLAY_WIDTH=1900 \
    -e DISPLAY_HEIGHT=1080 \
    -e KEEP_APP_RUNNING=1 \
    -e ENABLE_CJK_FONT=1 \
    -e SECURE_CONNECTION=0 \
    -e VNC_PASSWORD=admin \
    -p 5800:5800 \
    -v /home/chrome_config:/config:rw \
    --security-opt seccomp=unconfined \
    --shm-size 1500m \
    --privileged=true \
    langren1353/chrome-cn

参数解释
-e USER_ID=0 \ ## 用户，用于文件权限读写-默认即可
-e GROUP_ID=0 \ ## 组，用于文件权限读写-默认即可
-e TZ=Asia/Hong_Kong \ ##这个是设置地区-默认即可
-e DISPLAY_WIDTH=1920 \ ##设置显示的高宽
-e DISPLAY_HEIGHT=1080 \ ##设置显示的高宽
-e KEEP_APP_RUNNING=1 \ ##关闭了之后会自动重启，不然所有标签页关闭了，浏览器也就关了。
-e ENABLE_CJK_FONT=1 \ ##一定要加这个，不然中文显示乱码
-e SECURE_CONNECTION=1 \ ##启用 HTTPS，再绑定域名，安全一点点，不建议开启，开启后，初始化很慢
e VNC_PASSWORD=xxxxxxxx \ ##访问密码，不然谁打开都能用了
-p 5800:5800 \ ##端口
-v /home/chrome_config:/config:rw \ ##数据，包括下载的东西、插件，不然不好找，重装可以继续用这个目录
--security-opt seccomp=/path/to/seccomp/profile.json \ ##配置文件默认情况下拒绝访问系统调用，不然网页会经常卡死崩溃，懒得弄的可以用 --security-opt seccomp=unconfined \，但是安全性差一些。
--shm-size 1500m \ ##内存使用，单位m或是g，建议是2g，但是500M的机器并不是不能试试看

## 实践
在甲骨文AMD小鸡测试，可以安装并打开。但慢到不能使用。小内存的机子基本用不上。
在甲骨文ARM上有良好的体验。适合在外需要翻墙浏览信息。
'''
docker run -itd --restart=always --name=chrome -e USER_ID=0 -e GROUP_ID=0 -e TZ=Asia/Hong_Kong -e DISPLAY_WIDTH=1024 -e DISPLAY_HEIGHT=768 -e KEEP_APP_RUNNING=1 -e ENABLE_CJK_FONT=1 -e SECURE_CONNECTION=0 -e VNC_PASSWORD=litscorpi -p 5800:5800 -v /home/chrome_config:/config:rw --security-opt seccomp=unconfined --shm-size 500m langren1353/chrome-cn
'''
