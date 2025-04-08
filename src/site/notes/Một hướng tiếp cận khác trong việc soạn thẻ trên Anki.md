---
{"dg-publish":true,"permalink":"/mot-huong-tiep-can-khac-trong-viec-soan-the-tren-anki/"}
---

[Link tải template mẫu](https://drive.google.com/file/d/1MxmBe2v4yMPBXh-Tf3E_nPz65Ily99lL/view?usp=sharing)
Mã addon: 1400986563

Thông thường, ít ai nhập từ vựng trực tiếp vào Anki mà thay vào đó, họ sử dụng AI để tạo một file CSV với các cột như "từ", "từ loại", "định nghĩa", "câu ví dụ", v.v. Sau đó, file CSV này được nhập vào Anki, tương ứng với các trường dữ liệu trong ứng dụng. Các trường này tiếp tục được hiển thị dưới dạng HTML và hiển thị trên hai mặt của flashcard.

Cách tiếp cận của mình đơn giản hơn: sử dụng AI để tạo trực tiếp định dạng HTML ngay trên Anki và lưu lại tại 2 trường tin `Front` và `Back`.

Trước tiên ta cần đi qua nguyên lý hoạt động của mẫu thẻ Langki. Mỗi mẫu thẻ Langki sẽ bao gồm 3 phần: `Front`, `Back`, và `Prompt`

![](https://i.imgur.com/rXRX3DT.png)

Đầu tiên, AI sẽ kiểm tra nội dung trong phần `Front` (phần màu xanh dương) và `Back` (phần màu xanh lá). Nếu 1 trong hai phần này bị để trống (trong trường hợp này là vì trường tin `{{Front}}` và `{{Back}}` không có nội dung), thì AI sẽ tiến hành tạo flashcard dựa trên nội dung trong phần `Prompt` (phần màu đỏ).

Vậy tại phần `Prompt` ta hãy viết câu lệnh cho AI tạo flashcard.

![](https://i.imgur.com/P8tsWwV.png)

```HTML
<div id="front" style="display: none">
<!-- ========= THE FRONT OF THE FLASHCARD ========= -->
{{Front}}
<!-- ========= THE END OF THE FRONT ========= -->
</div>

<div id="back" style="display: none">
<!-- ========= THE BACK OF THE FLASHCARD ========= -->
{{Back}}
<!-- ========= THE END OF THE BACK ========= -->
</div>

<div id="prompt" style="display: none">
<!-- ========= SET UP YOUR PROMPT HERE ========= -->
Hãy giúp tôi tạo một flashcard theo mẫu sau
Ví dụ với từ vựng chủ điểm "abandon" thì thẻ flashcard sẽ như sau:
Mặt trước
<div description="định nghĩa tiếng Anh">
to leave somebody, especially somebody you are responsible for, with no intention of returning
</div>
<div description="định nghĩa tiếng Việt">
từ bỏ
</div>
<div description="một câu ví dụ sử dụng từ vựng chủ điểm. Tuy nhiên từ vựng chủ điểm bị thay thế bởi cloze [...]">
How could she <b>[...]</b> her own child?
</div>
<div description="dịch nghĩa của câu ví dụ">
Làm sao cô ta có thể bỏ rơi con của mình?
</div>


Mặt sau:
<div description="từ vựng chủ điểm">
abandon
</div>
<div description="phiên âm">
...
</div>
<div description="audio của từ vựng chủ điểm">
((tts_autoplay:abandon))
</div>
<div description="định nghĩa tiếng Anh">
to leave somebody, especially somebody you are responsible for, with no intention of returning
</div>
<div description="định nghĩa tiếng Việt">
từ bỏ
</div>
<div description="câu ví dụ ở mặt trước kèm với audio">
((tts:How could she abandon her own child?)) How could she abandon her own child?
</div>
<div description="dịch nghĩa của câu ví dụ">
...
</div>

Tương tự tạo một thẻ flashcard theo mẫu trên với từ vựng chủ điểm là "{{Từ vựng}}".
{{Chú thích}}

<!-- ========= THE END OF THE PROMPT ========= -->
</div>
...
```

Vì ta cần AI tạo flashcard dưới định dang HTML nên mẫu thẻ ta làm mẫu cho AI cũng phải có định dạng HTML với cú pháp.
```html
<div description="miêu tả đữ liệu ta muốn AI tạo">
Dữ liệu mẫu (hoặc ...)
</div>
```

Cú pháp tạo audio bằng Langki.
`((tts:Nội dung bạn muốn chuyển thành giọng nói))`
`((tts_autoplay:Nội dung bạn muốn chuyển thành giọng nói. Nhưng ở phiên bản này audio sẽ tự động phát mà không cần nhấn))` 

AI lúc nãy sẽ đọc nội dung trong phần `Prompt`, tạo flashcard và lưu nội dung đã tạo vào hai trường `{{Front}}` và `{{Back}}`. Vì nội dung `Front` và `Back` chỉ bao gồm hai trường tin `{{Front}}` và `{{Back}}`, nên khi ta review lại flashcard này `Front` và `Back` đã không còn trống => AI sẽ không tạo lại flashcard. Do đó, khi sửa `Prompt` hay edit lại template, bạn cần xoá 2 trường tin `{{Front}}` và `{{Back}}` để AI tạo lại flashcard.

![](https://i.imgur.com/LuhJKaa.png)

Trong một số trường hợp, flashcard mà AI tạo có thể bị lỗi hoặc bị ngu (halluciation), bạn cần cung cấp thêm chú thích cho AI thông qua trường tin `{{Chú thích}}`. Còn không thì cứ để trống.

![](https://i.imgur.com/9mZot75.png)

Ví dụ với từ "national" này, nếu không ghi rõ chú thích, AI sẽ liên tục tạo flashcard với từ "national" (tính từ) hoặc đưa ra định nghĩa không chính xác.

![](https://i.imgur.com/7V7mBBU.png)

> [!Tip]
> Đừng cố gắng tạo một template hoàn hảo với description chi tiết. AI sẽ luôn có một tỉ lệ hallucination nhất định. Ví dụ, với 100 flashcard sẽ luôn có vài trường hợp AI cho ra kết quả không như ý. Trong những trường hợp này bổ sung thêm chú thích là sẽ hiệu quả hơn rất nhiều là tạo một template chính xác 100%. 

