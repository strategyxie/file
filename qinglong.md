# 青龙安装代码

docker run -dit -v $PWD/ql/data:/ql/data -p 5700:5700 --name qinglong --restart unless-stopped whyour/qinglong:latest
