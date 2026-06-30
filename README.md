# PHÂN TÍCH RỦI RO NỢ XẤU THẺ TÍN DỤNG Ở ĐÀI LOAN 4/2005 - 9/2005
## I. Tổng quan
- Công cụ sử dụng: R - Power BI
- Dữ liệu gốc: Default of Credit Card Clients Dataset
- Mục tiêu: Phân tích hành vi thanh toán và đặc điểm nhân khẩu học của khách hàng nhằm:
  + Xác định tỷ lệ nợ xấu tổng thể và theo từng nhóm phân loại
  + Tìm ra các yếu tố ảnh hưởng đến nguy cơ trở thành nợ xấu
  + Nhận diện nhóm khách hàng có rủi ro cao nhất
- Cấu trúc:
  + credit_card.Rmd:	Làm sạch dữ liệu và tạo biến bằng R
  + credit_card_Dashboard.pbix:	Dashboard tổng hợp kết quả
  + credit_card_Dashboard.pdf:	File PDF minh họa Dashboard

## II. Quy trình thực hiện
### 1. Làm sạch dữ liệu (R): Sử dụng package rio, dplyr, tidyr
- Dữ liệu ban đầu gồm có 30 000 quan sát với 25 biến. 
- Giá trị khuyết thiếu: Không có NA thực, NULL dạng chuỗi, hoặc chuỗi rỗng. Dữ liệu sạch về giá trị khuyết thiếu.
- Gía trị không hợp lệ:
  + Biến EDUCATION có mã 0, 5, 6 không có trong mô tả gốc, gộp vào nhóm 4 (Khác). 
  + Biến MARRIAGE có mã 0 không có trong mô tả gốc, gộp vào nhóm 3 (Khác). 

### 2. Tạo biến mới (R)
  + age_group:	Phân tổ tuổi thành 4 nhóm
  + limit_group:	Phân tổ hạn mức tín dụng thành 3 nhóm
  + late:	Đếm số tháng có trễ từ 2 tháng trở lên
  + ever_late:	Phân loại có từng trễ từ 2 tháng trở lên không
  + avg_pay_ratio:	Tỷ lệ thanh toán trung bình thực tế
  + pay_ratio_group:	Phân tổ tỷ lệ thanh toán trung bình
  + SEX_label:	Gắn nhãn cho biến SEX
  + EDUCATION_label:	Gắn nhãn cho biến EDUCATION
  + MARRIAGE_label:	Gắn nhãn cho biến MARRIAGE
  + DEFAULT_label:	Gắn nhãn cho biến default.payment.next.month
  + PAY_0_label:	Gắn nhãn cho biến PAY_0

### 3. Câu hỏi phân tích
Truy vấn phân tích theo:
- Đặc điểm nhân khẩu học:
  + Tỷ lệ nợ xấu chung
  + Nhóm tuổi nào có tỷ lệ nợ xấu cao hơn?
  + Trình độ học vấn và tình trạng hôn nhân có ảnh hưởng đến tỷ lệ nợ xấu không?
- Theo hạn mức tín dụng:
  + Khách hàng có hạn mức thấp có tỷ lệ nợ xấu cao hơn không?
- Theo hành vi thanh toán:
  + Khách hàng từng trễ thanh toán trên 2 tháng có nguy cơ nợ xấu cao hơn so với nhóm chưa từng trễ không?
  + Tình trạng thanh toán tháng gần nhất ảnh hưởng như nào đến tỷ lệ nợ xấu?
  + Khách hàng có tỷ lệ thanh toán thấp có dễ trở thành nợ xấu hơn không?
- Tổng hợp:
  + Nhóm khách hàng nào có kết hợp nhiều yếu tố rủi ro nhất?
 
### 4. Tạo Dashboard tổng hợp kết quả (Power BI)
- Sử dụng Power BI để tổng hợp dữ liệu theo từng chiều phân tích, sau đó tạo biểu đồ và tổng hợp vào Dashboard.

## III. Kết quả phân tích
-	Tỷ lệ nợ xấu chung: 22.12%, cứ 5 khách hàng thì có gần 1 người nợ xấu.
-	Theo đặc điểm nhân khẩu học:
    + Nhóm 50 tuổi trở lên có tỷ lệ nợ xấu cao nhất (25.43%), trong khi nhóm 30-40 tuổi có tỷ lệ thấp nhất (20.34%).
    + Trình độ trung học có tỷ lệ nợ xấu cao nhất (25.16%), nhóm sau đại học có tỷ lệ thấp hơn (19.23%). Học vấn càng cao, rủi ro nợ xấu càng thấp.
    + Tỷ lệ nợ xấu theo tình trạng hôn nhân không có sự khác biệt quá rõ ràng.
-	Theo hạn mức tín dụng:
    + Nhóm hạn mức thấp (dưới 50000) có tỷ lệ nợ xấu cao nhất (36.07%), cao gấp 2.5 lần nhóm hạn mức cao (14.73%). Khách hàng có lịch sử tín dụng kém thường có hạn mức thấp, rủi ro nợ xấu cao.
-	Theo hành vi thanh toán: 
    + Nhóm từng trễ từ 2 tháng trở lên có tỷ lệ nợ xấu 46.30%, cao gấp 3.6 lần nhóm chưa từng trễ (12.75%).
    + Tình trạng thanh toán tháng gần nhất phản ánh rõ ràng rủi ro nợ xấu. Trễ càng nhiều thì tỷ lệ nợ xấu càng cao.
    + Nhóm có tỷ lệ thanh toán trung bình dưới 20% có tỷ lệ nợ xấu cao nhất (26.67%), cao hơn đáng kể so với nhóm trả trên 50% (18.72%).
-	Tổng hợp:
    + Nhóm kết hợp có rủi ro nợ xấu cao nhất, cần ưu tiên kiểm soát (54.39%): Trên 50 tuổi, hạn mức tín dụng cao, từng trễ từ 2 tháng trở lên, tỷ lệ thanh toán dưới 20%.
