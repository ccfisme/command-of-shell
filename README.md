首先，先说一下，[Mac不能用su开root权限，只能用sudo su开启](https://www.xiebruce.top/601.html)  

然后，我感觉，看哪个命令权限大，看的是他们的环境变量，也就是谁能够操作的文件多  


然后，直观比较一下  

* sudo su  

![image](https://user-images.githubusercontent.com/74129445/141875526-eecfcc78-a6ea-460f-8b9c-a71c6190273e.png)  



* sudo su -   



![image](https://user-images.githubusercontent.com/74129445/141875607-74ce5250-fb4f-471f-bd6d-40693d790a8f.png)  

* sudo -i  


![image](https://user-images.githubusercontent.com/74129445/141875747-8c591e37-3996-4a93-972d-899d2c11d80b.png)  

* sudo -s  

![image](https://user-images.githubusercontent.com/74129445/141875863-cc4f828e-f929-4046-8591-115425f98275.png)


