# Mining-Massive-Data-Sets-Machine-learning-in-PySpark-and-Spark-DataFrame
Learn about machine learning, the mllib library in pyspark, and the dataframe spark

## Phần 1: Spark DataFrame
### I.	Tổng quát về Spark DataFrame
<p align="center"><img src ="https://user-images.githubusercontent.com/77878466/106385587-a290a500-6403-11eb-94fc-bd770314e097.png" width="70%"/></p>
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; DataFrame là một API bậc cao hơn RDD được Spark giới thiệu vào năm 2013 (từ Apache Spark 1.3). Tương tự như RDD, dữ liệu trong DataFrame cũng được quản lý theo kiểu phân tán và không thể thay đổi (immutable distributed). Tuy nhiên dữ liệu này được sắp sếp theo các cột, tương tự như trong Relation Database. DataFrame được phát triển để giúp người dùng có thể dễ dàng thực hiện các thao tác xử lý dữ liệu cũng như làm tăng đáng kể hiệu quả sử lý của hệ thống.</p>

<div align="justify">Theo Databricks, DataFrame là một tập hợp dữ liệu phân tán được tổ chức thành các cột được đặt tên. Về mặt khái niệm, nó tương đương với một bảng trong cơ sở dữ liệu quan hệ hoặc một khung dữ liệu trong R / Python, nhưng với các tối ưu hóa phong phú hơn. DataFrames có thể được xây dựng từ nhiều nguồn như tệp dữ liệu có cấu trúc, Hive table, cơ sở dữ liệu bên ngoài hoặc RDD hiện có.
Dataframe thường đề cập đến một cấu trúc dữ liệu, có bản chất là dạng bảng. Nó đại diện cho các Hàng, mỗi hàng bao gồm một số quan sát. Các hàng có thể có nhiều định dạng dữ liệu khác nhau (Không đồng nhất), trong khi một cột có thể có dữ liệu có cùng kiểu dữ liệu (Đồng nhất). Khung dữ liệu thường chứa một số siêu dữ liệu ngoài dữ liệu; ví dụ, tên cột và hàng.</div>

### II. Lợi ích mà DataFrame mang lại
<ul align="justify">
  <li><b><em>Xử lý dữ liệu có cấu trúc và bán cấu trúc</em></b>: DataFrames được thiết kế để xử lý một tập hợp lớn dữ liệu có cấu trúc cũng như bán cấu trúc . Các quan sát trong Spark DataFrame được tổ chức dưới các cột được đặt tên, giúp Apache Spark hiểu được lược đồ của Dataframe. Điều này giúp Spark tối ưu hóa kế hoạch thực thi trên các truy vấn này. Nó cũng có thể xử lý hàng petabyte dữ liệu.</li></br>
  
  <li><b><em></em>Slicing và Dicing</b>: API DataFrames thường hỗ trợ các phương pháp phức tạp để cắt và phân loại dữ liệu. Nó bao gồm các hoạt động như "selecting" hàng, cột và ô theo tên hoặc theo số, lọc ra các hàng, v.v. Dữ liệu thống kê thường rất lộn xộn và chứa nhiều giá trị bị thiếu và không chính xác cũng như vi phạm phạm vi. Vì vậy, một tính năng cực kỳ quan trọng của DataFrames là quản lý rõ ràng dữ liệu bị thiếu.</li></br>
  
  <li><b><em></em>Hỗ trợ nhiều ngôn ngữ</b>: Hỗ trợ API cho các ngôn ngữ khác nhau như Python, R, Scala, Java, giúp những người có nền tảng lập trình khác nhau sử dụng dễ dàng hơn.</li></br>
  
  <li><b><em>Nguồn dữ liệu</em></b>: DataFrames có hỗ trợ cho nhiều định dạng và nguồn dữ liệu, chúng ta sẽ xem xét vấn đề này sau trong hướng dẫn Pyspark DataFrames này. Họ có thể lấy dữ liệu từ nhiều nguồn khác nhau.</li></br>
</ul>

### III.	Các tính năng của DataFrame và nguồn dữ liệu PySpark
#### 1.	Các tính năng
<p align="center"><img src ="https://user-images.githubusercontent.com/77878466/106385562-81c84f80-6403-11eb-9a1d-37f785ef7d23.png" width="50%"/></p>
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; DataFrame được phân phối trong tự nhiên, làm cho nó trở thành một cấu trúc dữ liệu có khả năng chịu lỗi và có tính khả dụng cao.</p>

<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Đánh giá lười biếng là một chiến lược đánh giá giữ việc đánh giá một biểu thức cho đến khi giá trị của nó là cần thiết. Nó tránh đánh giá lặp lại. Đánh giá lười biếng trong Spark có nghĩa là quá trình thực thi sẽ không bắt đầu cho đến khi một hành động được kích hoạt. Trong Spark, bức tranh về sự lười biếng xuất hiện khi các phép biến đổi Spark xảy ra.</p>

<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; DataFrame là bất biến trong tự nhiên. Bởi bất biến, ý tôi là nó là một đối tượng có trạng thái không thể sửa đổi sau khi nó được tạo. Nhưng chúng ta có thể biến đổi các giá trị của nó bằng cách áp dụng một phép biến đổi nhất định, như trong RDD.</p>

#### 2. Nguồn dữ liệu PySpark
<p align="center"><img src ="https://user-images.githubusercontent.com/77878466/106385563-85f46d00-6403-11eb-916a-5bbcb6e25131.png" width="50%"/></p>
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Dữ liệu có thể được tải vào thông qua tệp CSV, JSON, XML  hoặc tệp Parquet. Nó cũng có thể được tạo bằng cách sử dụng RDD hiện có và thông qua bất kỳ cơ sở dữ liệu nào khác, như Hive hoặc Cassandra . Nó cũng có thể lấy dữ liệu từ HDFS hoặc hệ thống tệp cục bộ.</p>
