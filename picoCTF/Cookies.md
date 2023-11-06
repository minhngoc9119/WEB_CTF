# Description
Who doesn't love cookies? Try to figure out the best one.

# Kiểm tra thử bằng 1 request:
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/b50068e9-b3fb-4ffc-b8e5-62cb0cd9dd21)
-> Ta thấy Cookie có tham số name=-1 thử thay đổi giá trị này sang 1 số khác vd 1:
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/2146eea7-8d7a-4bd0-acb3-b3da014d033c)
-> Thử follow redirect ta được:
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/02906a14-670a-428e-90c0-9291eee2b636)
-> Thử thay đổi các giá trị khác của name bằng Intruder:
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/95fbf867-c9f9-4a88-ad40-89d2278516da)
-> Ta đã tìm được giá trị flag.
