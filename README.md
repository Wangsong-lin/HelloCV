<img width="1315" height="960" alt="image" src="https://github.com/user-attachments/assets/54daa947-7990-478f-9d70-7f4fcce426f5" /># HelloCV
全部语雀文档链接：https://www.yuque.com/guogios/br9hnh/yo8xglaansmu38i6
               https://www.yuque.com/guogios/br9hnh/eweuza2mn9tyggmw
               https://www.yuque.com/guogios/br9hnh/wouaroark6e5md6p
         额外文档（汉化VScode过程）：https://www.yuque.com/guogios/br9hnh/yxpat0ygnt0duhfi      
一、 现在我来详细介绍下ROS2的相关流程
这里我先介绍下我参考的文章，以下是链接：
https://blog.csdn.net/maizousidemao/article/details/144008825
据此，我整理了下具体的流程(最后我会附上语雀笔记链接作为补充以及可能问题的解答)：
Step 1、配置环境
打开终端并输入指令：sudo apt update && sudo apt install locales
                 sudo locale-gen en_US en_US.UTF-8
                 sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
                 export LANG=en_US.UTF-8
（版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。
原文链接：https://blog.csdn.net/maizousidemao/article/details/144008825，以下同此）
为了检验设置是否成功，有指令：locale
Step 2、添加ROS2库
同样：sudo apt install software-properties-common
     sudo add-apt-repository universe
可以一次性执行，或者依次执行
并且用apt添加 ROS 2 GPG 密钥：sudo apt update && sudo apt install curl -y
                           sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg                           
Step 3、 更新，安装
指令依次：sudo apt install ros-dev-tools    #更新
        sudo apt install ros-humble-desktop    # 1. 桌面安装（推荐）：ROS、RViz、演示、教程
        sudo apt install ros-humble-ros-base   # 2. ROS-Base 安装（基本配置）：通信库、消息包、命令行工具。无 GUI 工具
Step 4、 配置
指令：  echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
       source ~/.bashrc
 
至此结束安装
语雀链接：https://www.yuque.com/guogios/br9hnh/yo8xglaansmu38i6


二、安装VScode
使用浏览器搜索：VScode
然后点击官网
法一、   直接选择安装（注意要下Linux版）
        然后再从主文件夹处找到Downloads夹，找到VScode的安装包，右键鼠标点击安装即可
法二、   终端定位到Downloads
        用指令: sudo dpkg -i 加安装包名即可（一般这都是.deb的安装包）
语雀链接：https://www.yuque.com/guogios/br9hnh/eweuza2mn9tyggmw



三、安装 Open CV
我先声明下这里我参考了CSDN的博客文章，链接在此：
https://blog.csdn.net/BUBUBUBUBUBUBUB/article/details/128644982?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-2-128644982-blog-95520693.235%5Ev43%5Econtrol&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-2-128644982-blog-95520693.235%5Ev43%5Econtrol
(有点长哈）
流程如下：
一：安装Cmake
指令：bash
     sudo apt-get install cmake
二：安装依赖库
指令：sudo apt-get install build-essential libgtk2.0-dev libavcodec-dev libavformat-dev libjpeg-dev libswscale-dev libtiff5-dev
三、下载OpenCV源码
从OpenCV官网上下载源码，点击Source下载OpenCV源码
链接：https://opencv.org/releases/
下载文件为.zip格式,需要安装解压软件unzip
最后指令：sudo apt-get install unzip
使用以下命令解压OpenCV源码,其中-d表示指定解压路径，我这里解压到用户目录下
指令：unzip opencv-4.7.0.zip -d ~/
附图（解压效果）：<img width="1545" height="598" alt="image" src="https://github.com/user-attachments/assets/084c374c-80e3-4f66-ab0d-3ec6e644c654" />
注意请选择src后的“https://”请求打开。
四、编译OpenCV源码
指令：cd ~/opencv-4.7.0
     mkdir build && cd build
     sudo cmake -D CMAKE_BUILD_TYPE=Release -D OPENCV_GENERATE_PKGCONFIG=ON -D CMAKE_INSTALL_PREFIX=/usr/local ..
        （版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。
          原文链接：https://blog.csdn.net/BUBUBUBUBUBUBUB/article/details/128644982）
OPENCV_GENERATE_PKGCONFIG=ON 表示自动生成pkg-config文件，如果没有添加这一条指令，则需要手动添加。
CMAKE_INSTALL_PREFIX=/usr/local 指定OpenCV安装路径，这里是/usr/local
依次输入以下两条命令，耐心等待几分钟后OpenCV安装完成。-j8表示使用多线程编译，数字8表示8线程，这个数字不应超过CPU的核心数。
sudo make -j8
sudo make install
五、 环境配置
安装pkg-config，指令：sudo apt-get install pkg-config                      
执行下面命令更新配置 
sudo ldconfig
配置pkg-config
检查是否存在/usr/local/lib/pkgconfig/opencv4.pc文件，输入以下命令即可查看文件内容
cat /usr/local/lib/pkgconfig/opencv4.pc
之后操作如图：
<img width="1659" height="1050" alt="image" src="https://github.com/user-attachments/assets/5d42fefb-7ccf-4524-9eca-539bfe5b4f9d" />
<img width="1711" height="1064" alt="截图 2025-10-13 08-43-44" src="https://github.com/user-attachments/assets/2b0eeb2e-7ed0-404c-accd-613a9ccd04d8" />
这样于是便装好了
语雀链接：https://www.yuque.com/guogios/br9hnh/wouaroark6e5md6p

