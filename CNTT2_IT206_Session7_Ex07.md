# Bài thực hành 7: AI Gia sư giúp sinh viên hiểu và sửa lỗi code (C)

**Họ tên:** ........  **MSSV:** ........  **Mô hình AI dùng:** ........

## 1. Đề bài
Chương trình C tính điểm trung bình 3 môn nhưng kết quả không chính xác. Mình muốn tự hiểu lỗi chứ không nhờ AI viết lại.

## 2. Code gốc

```c
#include <stdio.h>

int main() {
    int a, b, c;
    float avg;

    printf("Nhap 3 diem: ");
    scanf("%d%d%d", &a, &b, &c);

    avg = (a + b + c) / 3;

    printf("Diem trung binh: %f", avg);
    return 0;
}
```

*(Nếu code trong đề khác thì dán code của đề vào đây.)*

## 3. Prompt của mình

```
# VAI TRÒ
Bạn là giảng viên lập trình C, dạy bằng câu hỏi gợi mở.

# LUẬT
- Không viết lại toàn bộ code ngay từ đầu.
- Không đưa đáp án hoàn chỉnh khi tôi đang thử giải thích.
- Mỗi lần chỉ đặt MỘT câu hỏi.

# QUY TRÌNH
1. Yêu cầu tôi dự đoán kết quả chương trình trước khi chạy.
2. Hỏi tôi vì sao kết quả lại như vậy.
3. Kiểm tra tôi có hiểu phép chia nguyên trong C không.
4. Gợi ý từng bước nhỏ, giúp tôi thấy khác nhau giữa int và float.
5. Yêu cầu tôi tự đề xuất cách sửa, rồi đánh giá.
6. Yêu cầu tôi giải thích lại bằng một ví dụ khác.
7. Chỉ đưa code tham khảo SAU KHI tôi đã tự sửa.
Phải có ít nhất 3 lượt tôi tự giải thích và điều chỉnh.

<code_C>
[dán code vào đây]
</code_C>
Bắt đầu bằng bước 1.
```

## 4. Hội thoại với AI
*(Dán hội thoại thật, ít nhất 6 lượt, có ≥ 3 lượt mình tự giải thích)*

(dán)

## 5. Phân tích lỗi
Dòng `avg = (a + b + c) / 3;` có `a`, `b`, `c` và số `3` đều là **số nguyên (int)**. Trong C, int chia int cho ra int, phần thập phân bị **cắt bỏ trước** rồi mới gán vào biến `float`. Nên `avg` là float nhưng giá trị đã bị mất phần lẻ từ trước.

**Ví dụ để thấy lỗi:**

| Nhập | Tổng | Máy tính ra | Đáng lẽ |
|---|---|---|---|
| 7, 8, 8 | 23 | 7.000000 | 7.666667 |
| 7, 8, 9 | 24 | 8.000000 | 8.000000 |

Với 7, 8, 9 thì chia hết nên nhìn không ra lỗi. Mình thử thêm 7, 8, 8 để thấy rõ. (Đề ghi "8 thay vì 8.0" là do int thì in ra 8, float in ra 8.000000.)

## 6. Code sau khi tự sửa

```c
// Cách 1: chia cho 3.0 (số thực)
avg = (a + b + c) / 3.0;

// Cách 2: ép kiểu
avg = (float)(a + b + c) / 3;
```

Chỉ cần một trong hai số là float thì phép chia sẽ là chia số thực.

## 7. Phép chia nguyên và phép chia số thực

| | Chia nguyên | Chia số thực |
|---|---|---|
| Điều kiện | cả hai số là int | ít nhất một số là float |
| Ví dụ | `7 / 2` = 3 | `7 / 2.0` = 3.5 |
| Phần lẻ | bị cắt bỏ | được giữ |

## 8. Ví dụ mới của mình
Chia 10 cái kẹo cho 4 bạn:
- `10 / 4` = 2 (mỗi bạn 2 cái, phần dư bị bỏ)
- `10 / 4.0` = 2.5 (mỗi bạn 2.5 cái)

## 9. Checklist
- [ ] Prompt hoàn chỉnh
- [ ] Hội thoại ≥ 6 lượt, ≥ 3 lượt tự giải thích
- [ ] Phân tích lỗi ban đầu
- [ ] Code sau khi tự sửa
- [ ] Giải thích chia nguyên và chia số thực
- [ ] Ví dụ mới

## 10. Nhận xét
- Cách hỏi từng bước giúp mình hiểu vì sao lỗi xảy ra, nhớ lâu hơn là chép đáp án.
- Mình dự đoán kết quả trước khi chạy nên thấy rõ chỗ mình đoán sai.
- Chỗ chưa tốt: (viết theo thực tế, ví dụ AI có lỡ đưa đáp án sớm không).
