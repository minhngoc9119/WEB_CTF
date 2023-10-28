# The application is using JWT based authentication. You can not brute the secret!

> Flag is located on admin account\
> Format FLAG: CHH{XXX}

- Dùng burpsuite discovery content tìm được đường dẫn bí mật /secret\
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/9d636d54-8d4f-42d1-8580-1744cf5e639b)
- Sau khi tìm kiếm trên mạng về googlebot: link(https://developers.google.com/search/docs/crawling-indexing/overview-google-crawlers#user_agent_version)\
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/b0a38fb8-c122-4652-8c58-98b579b9a31c)
- Thử chỉnh requets User-agent thành Googlebot:\
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/7cd760dd-8693-490f-82b5-c0221bba6dab)
- Dùng tài khoản tìm được đăng nhập vào trang ta được redirect sang trang /flag\
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/de0ef4c0-a9c8-446e-8145-20f6e5b414d7)
- Kiểm tra bằng burp ta thấy: web sửa dụng jwt để xác thực:\
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/a0bdac24-b957-4cb9-b535-7239f80fabf4)
- Thử đọc mã jwt này trên trang link(https://jwt.io/):\
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/b2948350-7919-4f2c-9592-83fdd0c031a2)
- NOTE: Tất cả Mã thông báo Web JSON phải chứa tham số tiêu đề "alg", chỉ định thuật toán mà máy chủ nên sử dụng để xác minh chữ ký của mã thông báo. Ngoài các thuật toán mã hóa mạnh, đặc tả JWT còn xác định thuật toán "none", có thể được sử dụng với JWT "không bảo mật" (không dấu). Khi thuật toán này được hỗ trợ trên máy chủ, nó có thể chấp nhận các mã thông báo không có chữ ký nào cả.
- Thử đổi giá trị alg thành none và đổi user thành admin:\
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/d560f80e-5d65-4af7-a47b-fc91339360bc)
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/ac0852cc-b165-40cb-add0-98197a1ea425)
- Dùng thông tin tìm được ta tìm được flag:\
![image](https://github.com/minhngoc9119/WEB_CTF/assets/34714073/48c90a1f-34a3-4c56-b67b-8915430808ac)
-Note: đã bỏ qua n bước tìm sai như chỉnh giá trị user-agent sai, kiểm tra jwt thấy nó giống giá trị có trong session nên cố chỉnh thử và thất bại.
