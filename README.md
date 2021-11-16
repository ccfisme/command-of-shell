# sudo后接su、su-、-i、-s登陆的区别

首先，先说一下，[Mac不能用su开root权限，只能用sudo su开启](https://www.xiebruce.top/601.html)  

然后，我感觉，看哪个命令权限大，看的是他们的环境变量，以及执行以后的位置，也就是谁能够操作的文件多  


然后，直观比较一下  

* 原生  

![image](https://user-images.githubusercontent.com/74129445/141876775-1e7adf3c-49c0-4faf-a822-beb20b6965ef.png)  


* sudo su  

![image](https://user-images.githubusercontent.com/74129445/141876425-83f1cd13-d17f-4f66-8c9e-7af1f5ca742b.png)  



* sudo su -   



![image](https://user-images.githubusercontent.com/74129445/141876510-71983332-2774-4b55-a3b3-0d82042719bb.png)  

* sudo -i  


![image](https://user-images.githubusercontent.com/74129445/141876561-4fe4e758-1413-4859-90a0-7ae820782b1f.png)  


* sudo -s  

![image](https://user-images.githubusercontent.com/74129445/141876609-3623b636-fcaf-4bc9-8f92-2b5fc32e3589.png)

> 结论：通过与原生的对比不难看出，sudo su与sudo -s一样，只是切换了用户，但环境变量与原用户相同；而sudo -i和sudo su -则是直接变成了超级用户登陆，环境变量也是超级用户的环境变量，不过两者环境变量有轻微的不同，猜测-i的权限更大。
> 影响：root环境变量是指系统环境变量，对所有用户起作用，而用户环境变量只对当前用户起作用。也就是说，root后可以修改系统环境变量，但改不了用户的环境变量；而用户root则是可以修改当前用户的环境变量，但改不了系统环境变量























