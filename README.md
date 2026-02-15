# Câu hỏi: 

## 1. Tại sao Vue cần chia ra Doc và Api 

<img width="2048" height="1207" alt="image" src="https://github.com/user-attachments/assets/d0fb0d6a-e0a0-4334-8cfd-94c597ec821b" />


<img width="2048" height="1207" alt="image" src="https://github.com/user-attachments/assets/b3c67d25-f6a4-431a-990e-483dc1b46f95" />

#### => Docs là bản đồ còn API là từ điển. (Lập trình là hiểu tư duy trước, thuộc api sau)


- Nếu bạn vào phần Introduction trong Docs, Vue đang kể một câu chuyện: Vue là gì, tư duy ra sao, component hoạt động thế nào, reactivity là cái quái gì. Nó dắt bạn đi từ tư tưởng → mô hình → cách dùng. Đây là hướng “hiểu để làm”.

- Còn API thì không kể chuyện. API nói thẳng như kỹ sư công trường: (api giúp developer kết nối với Vue)
`data(): object`
`watch(source, callback, options)`
Nó là đặc tả kỹ thuật. Không màu mè. Không dẫn dắt. Chỉ định nghĩa chính xác từng option, từng tham số, từng kiểu trả về.

**Vì sao phải tách?**

- Thứ nhất: mục đích khác nhau.
Docs dạy tư duy. API tra cứu chi tiết.

- Thứ hai: người đọc khác nhau.
Người mới cần Docs.
Người đã biết Vue nhưng quên tham số của `watch` thì nhảy thẳng vào API.

- Thứ ba: tránh nhiễu nhận thức.
Nếu trộn hết lại, bạn sẽ vừa đọc “Reactivity Fundamentals” vừa bị đập vào mặt bằng interface TypeScript dài 20 dòng. Não sẽ cháy.

- Thứ tư: tính chính xác.
API cần cực kỳ chặt chẽ và cập nhật theo version. Docs có thể diễn giải mềm hơn. Hai thứ có vòng đời chỉnh sửa khác nhau.

Nói cách khác:
Docs trả lời “Tại sao và dùng thế nào?”
API trả lời “Cụ thể từng dòng nghĩa là gì?”

**chú ý**
- Vue không mở ruột gan cho bạn xem. Nó chỉ cho bạn một số cửa chính thức để đi vào. Những cửa đó chính là API.
- Interface là khái niệm chung & API là một loại interface.
