首先，先说一下，[Mac不能用su开root权限，只能用sudo su开启](https://www.xiebruce.top/601.html)  

然后，直观比较一下  

* sudo su  

![image](https://user-images.githubusercontent.com/74129445/141823418-7b6be4a0-dbb9-4dc8-9cf3-d8d68cb5b46e.png)  

* sudo su - 

![image](https://user-images.githubusercontent.com/74129445/141823481-2207eb0f-6935-43dd-b13f-e893309cebbd.png)  

明显可以看出来权限不一样，sudo su 是用来开本级用户的root的，sudo su - 是用来开整个电脑权限的
