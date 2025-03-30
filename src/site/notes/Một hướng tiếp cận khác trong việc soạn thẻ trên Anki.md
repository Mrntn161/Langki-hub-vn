---
{"dg-publish":true,"permalink":"/mot-huong-tiep-can-khac-trong-viec-soan-the-tren-anki/"}
---


Thông thường, ít ai nhập từ vựng trực tiếp vào Anki mà thay vào đó, họ sử dụng AI để tạo một file Excel chứa các cột như 'từ', 'từ loại', 'định nghĩa', 'câu ví dụ', v.v. Sau đó, file Excel này được nhập vào Anki, tương ứng với các trường dữ liệu trong ứng dụng. Các trường này tiếp tục được hiển thị dưới dạng HTML và hiển thị trên hai mặt của flashcard.

Cách tiếp cận của mình đơn giản hơn: sử dụng AI để tạo trực tiếp định dạng HTML ngay trên Anki và lưu lại tại 2 trường tin `Front` và `Back`

![](https://i.imgur.com/FrtPdUS.png)

![](https://i.imgur.com/2KFMqnH.png)

![](https://i.imgur.com/ww8rszB.png)

![](https://i.imgur.com/lt1XKAI.png)

Cú pháp để AI tạo mẫu thẻ cũng rất đơn giản, bạn chỉ cần cung cấp chú thích cho AI.
```HTML
<div description="chú thích miêu tả thông tin mà bạn muốn AI tạo">...</div>
```

Về phần audio, các bạn cũng không cần dùng HyperTTS để tải về hàng loạt audio file. Thay vào đó, AI sẽ tự động chuyển đổi văn bản thành giọng nói ngay trong quá trình tạo thẻ.

`((tts:...))` và `((tts_autoplay:...))` là hai cú pháp cho phép chuyển đổi văn bản sang audio.

![](https://i.imgur.com/AvvjUg4.png)

![](https://i.imgur.com/E7ORYiR.png)


