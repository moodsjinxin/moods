## python故障总结

### pip

- failed to create process

  - python文件目录修改过，打开pyhon目录下的Scripts文件夹找到pip—scripts.py文件，打开文件在文件的目录修改为当前目录

    ~~~python
    #!C:\Users\jinxin\jinxinpython\python.exe -x
    ~~~

    

- pip下载慢

  - 修改下载源

    ~~~
    pip3 install pac—name -i [国内镜像名]
    ~~~

    常用的镜像：

    清华：https://pypi.tuna.tsinghua.edu.cn/simple

    中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/

    华中理工大学：http://pypi.hustunique.com/

    山东理工大学：http://pypi.sdutlinux.org/

    豆瓣：http://pypi.douban.com/simple/