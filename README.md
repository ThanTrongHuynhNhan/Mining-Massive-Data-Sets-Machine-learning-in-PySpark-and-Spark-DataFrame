# Mining-Massive-Data-Sets-Machine-learning-in-PySpark-and-Spark-DataFrame
Learn about machine learning, the mllib library in pyspark, and the dataframe spark

## Phần 1: Spark DataFrame
### I.	Tổng quát về Spark DataFrame
<div align="justify">
<p align="center"><img src ="https://user-images.githubusercontent.com/77878466/116780466-3af00180-aaa7-11eb-88fc-f7b937db4e42.png" width="70%"/></p>
 &nbsp;&nbsp;&nbsp;&nbsp; DataFrame là một API bậc cao hơn RDD được Spark giới thiệu vào năm 2013 (từ Apache Spark 1.3). Tương tự như RDD, dữ liệu trong DataFrame cũng được quản lý theo kiểu phân tán và không thể thay đổi (immutable distributed). Tuy nhiên dữ liệu này được sắp sếp theo các cột, tương tự như trong Relation Database. DataFrame được phát triển để giúp người dùng có thể dễ dàng thực hiện các thao tác xử lý dữ liệu cũng như làm tăng đáng kể hiệu quả sử lý của hệ thống.</p>
</div>
<div align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Theo Databricks, DataFrame là một tập hợp dữ liệu phân tán được tổ chức thành các cột được đặt tên. Về mặt khái niệm, nó tương đương với một bảng trong cơ sở dữ liệu quan hệ hoặc một khung dữ liệu trong R / Python, nhưng với các tối ưu hóa phong phú hơn. DataFrames có thể được xây dựng từ nhiều nguồn như tệp dữ liệu có cấu trúc, Hive table, cơ sở dữ liệu bên ngoài hoặc RDD hiện có.<br><br>
  &nbsp;&nbsp;&nbsp;&nbsp; Dataframe thường đề cập đến một cấu trúc dữ liệu, có bản chất là dạng bảng. Nó đại diện cho các Hàng, mỗi hàng bao gồm một số quan sát. Các hàng có thể có nhiều định dạng dữ liệu khác nhau (Không đồng nhất), trong khi một cột có thể có dữ liệu có cùng kiểu dữ liệu (Đồng nhất). Khung dữ liệu thường chứa một số siêu dữ liệu ngoài dữ liệu; ví dụ, tên cột và hàng.<br>
<p align="center"><img src ="https://user-images.githubusercontent.com/77878466/106385587-a290a500-6403-11eb-94fc-bd770314e097.png" width="65%"/></p>
</div>

### II. Lợi ích mà DataFrame mang lại
<ul align="justify">
  <li><b><em>Xử lý dữ liệu có cấu trúc và bán cấu trúc</em></b>: DataFrames được thiết kế để xử lý một tập hợp lớn dữ liệu có cấu trúc cũng như bán cấu trúc . Các quan sát trong Spark DataFrame được tổ chức dưới các cột được đặt tên, giúp Apache Spark hiểu được lược đồ của Dataframe. Điều này giúp Spark tối ưu hóa kế hoạch thực thi trên các truy vấn này. Nó cũng có thể xử lý hàng petabyte dữ liệu.</li></br>
  
  <li><b><em></em>Slicing và Dicing</b>: API DataFrames thường hỗ trợ các phương pháp phức tạp để cắt và phân loại dữ liệu. Nó bao gồm các hoạt động như "selecting" hàng, cột và ô theo tên hoặc theo số, lọc ra các hàng, v.v. Dữ liệu thống kê thường rất lộn xộn và chứa nhiều giá trị bị thiếu và không chính xác cũng như vi phạm phạm vi. Vì vậy, một tính năng cực kỳ quan trọng của DataFrames là quản lý rõ ràng dữ liệu bị thiếu.</li></br>
  
  <li><b><em></em>Hỗ trợ nhiều ngôn ngữ</b>: Hỗ trợ API cho các ngôn ngữ khác nhau như Python, R, Scala, Java, giúp những người có nền tảng lập trình khác nhau sử dụng dễ dàng hơn.</li></br>
  
  <li><b><em>Nguồn dữ liệu</em></b>: DataFrames có hỗ trợ cho nhiều định dạng và nguồn dữ liệu, chúng ta sẽ xem xét vấn đề này sau trong hướng dẫn Pyspark DataFrames này. Họ có thể lấy dữ liệu từ nhiều nguồn khác nhau.</li></br>
</ul>

### III.	Các tính năng của DataFrame, nguồn dữ liệu PySpark và các định dạng tệp được hỗ trợ
#### 1.	Các tính năng
<p align="center"><img src ="https://user-images.githubusercontent.com/77878466/106385562-81c84f80-6403-11eb-9a1d-37f785ef7d23.png" width="50%"/></p>
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; DataFrame được phân phối trong tự nhiên, làm cho nó trở thành một cấu trúc dữ liệu có khả năng chịu lỗi và có tính khả dụng cao.</p>

<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Đánh giá lười biếng là một chiến lược đánh giá giữ việc đánh giá một biểu thức cho đến khi giá trị của nó là cần thiết. Nó tránh đánh giá lặp lại. Đánh giá lười biếng trong Spark có nghĩa là quá trình thực thi sẽ không bắt đầu cho đến khi một hành động được kích hoạt. Trong Spark, bức tranh về sự lười biếng xuất hiện khi các phép biến đổi Spark xảy ra.</p>

<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; DataFrame là bất biến trong tự nhiên. Bởi bất biến, ý tôi là nó là một đối tượng có trạng thái không thể sửa đổi sau khi nó được tạo. Nhưng chúng ta có thể biến đổi các giá trị của nó bằng cách áp dụng một phép biến đổi nhất định, như trong RDD.</p>

#### 2. Nguồn dữ liệu PySpark
<p align="center"><img src ="https://user-images.githubusercontent.com/77878466/106385563-85f46d00-6403-11eb-916a-5bbcb6e25131.png" width="50%"/></p>
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Dữ liệu có thể được tải vào thông qua tệp CSV, JSON, XML  hoặc tệp Parquet. Nó cũng có thể được tạo bằng cách sử dụng RDD hiện có và thông qua bất kỳ cơ sở dữ liệu nào khác, như Hive hoặc Cassandra . Nó cũng có thể lấy dữ liệu từ HDFS hoặc hệ thống tệp cục bộ.</p>

#### 3. Các định dạng tệp được hỗ trợ
<div align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; DataFrame là một bộ API có bậc cao hơn RDD, khá đa dạng và phổ biến hỗ trợ việc đọc và ghi một số định dạng tệp như:
 <ul align="justify">
  <li>csv</li>
  <li>tsv</li>
  <li>xml</li>
  <li>Avro</li>
  <li>Parquet</li>
  <li>text - txt,...</li></ul>
</div>

### IV. Cách create một dataframe và một số thao tác đơn giản
<div align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Dữ liệu có thể được tải vào thông qua tệp CSV, JSON, XML hoặc tệp Parquet. Nó cũng có thể được tạo bằng cách sử dụng RDD hiện có và thông qua bất kỳ cơ sở dữ liệu nào khác, như Hive Table hay Apache Cassandra . Nó cũng có thể lấy dữ liệu từ HDFS hoặc hệ thống tệp cục bộ. Nhưng thông thường để load được dữ liệu từ một datasets có sẵn, người ta thường dùng<em> createDataFrame()</em> để có thể load dữ liệu được khởi tạo hoặc từ datasets kết hợp với <em>show()</em> để hiển thị kết quả. <br><br></div>
<p><b>&nbsp;&nbsp;&nbsp;&nbsp; *<u>Ví dụ </u>: <em>Với dữ liệu được người dùng tạo trực tiếp</em></b></p>

```python
import pyspark
from pyspark import SparkConf, SparkContext
from pyspark.sql import SparkSession
import collections

data = [('51800574','Nhan','Trong Huynh','Than','2000-10-18','M',2000),
  ('51800903','Minh','Nhat','Pham','2000-02-12','M',2200),
  ('51800886','Linh','Nhat','Nguyen','2000-09-01','M',2200),
  ('51800904','Nam','Van','Ho','2000-05-01','M',1980),
  ('51800631','Thong','Huy','Luu','2000-12-24','M',1900)
]

columns = ["id","firstname","middlename","lastname","birth","gender","salary"]
df = spark.createDataFrame(data=data, schema = columns)
df.show()
```
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Sau khi thực hiện xong đoạn code trên, chương trình sẽ in ra màn hình kết quả sau:</p>

```python
+--------+---------+-----------+--------+----------+------+------+
|      id|firstname| middlename|lastname|     birth|gender|salary|
+--------+---------+-----------+--------+----------+------+------+
|51800574|     Nhan|Trong Huynh|    Than|2000-10-18|     M|  2000|
|51800903|     Minh|       Nhat|    Pham|2000-02-12|     M|  2200|
|51800886|     Linh|       Nhat|  Nguyen|2000-09-01|     M|  2200|
|51800904|      Nam|        Van|      Ho|2000-05-01|     M|  1980|
|51800631|    Thong|        Huy|     Luu|2000-12-24|     M|  1900|
+--------+---------+-----------+--------+----------+------+------+
```
<p align="justify"><b>&nbsp;&nbsp; *<u>Ví dụ </u>: <em>Với dữ liệu được load từ dataset (file dữ liệu có sẵn)</em></b> - <em> link datasets: https://archive.ics.uci.edu/ml/machine-learning-databases/car/ </em></p>

<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Đọc dữ liệu từ file <em>ecoli.data</em> dưới dạng csv thông qua câu lệnh <em>spark.read.csv()</em>

```python
import pyspark
import os
from pyspark import SparkConf, SparkContext
from pyspark.sql import SparkSession
import collections

path = str(os.getcwd()) + "/car.data"
data_car = spark.read.csv(path, header = False, inferSchema = True)

data_car.show()
```
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Sau khi thực hiện xong đoạn code trên, chương trình sẽ in ra màn hình kết quả sau:</p>

```python
+-----+-----+---+----+-----+----+-----+
|  _c0|  _c1|_c2| _c3|  _c4| _c5|  _c6|
+-----+-----+---+----+-----+----+-----+
|vhigh|vhigh|  2|   2|small| low|unacc|
|vhigh|vhigh|  2|   2|small| med|unacc|
|vhigh|vhigh|  2|   2|small|high|unacc|
|vhigh|vhigh|  2|   2|  med| low|unacc|
|vhigh|vhigh|  2|   2|  med| med|unacc|
|vhigh|vhigh|  2|   2|  med|high|unacc|
|vhigh|vhigh|  2|   2|  big| low|unacc|
|vhigh|vhigh|  2|   2|  big| med|unacc|
|vhigh|vhigh|  2|   2|  big|high|unacc|
|vhigh|vhigh|  2|   4|small| low|unacc|
|vhigh|vhigh|  2|   4|small| med|unacc|
|vhigh|vhigh|  2|   4|small|high|unacc|
|vhigh|vhigh|  2|   4|  med| low|unacc|
|vhigh|vhigh|  2|   4|  med| med|unacc|
|vhigh|vhigh|  2|   4|  med|high|unacc|
|vhigh|vhigh|  2|   4|  big| low|unacc|
|vhigh|vhigh|  2|   4|  big| med|unacc|
|vhigh|vhigh|  2|   4|  big|high|unacc|
|vhigh|vhigh|  2|more|small| low|unacc|
|vhigh|vhigh|  2|more|small| med|unacc|
+-----+-----+---+----+-----+----+-----+
only showing top 20 rows
```

<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Để có một cái nhìn vào lược đồ tức là cấu trúc của DataFrame, ta sẽ sử dụng phương thức <em>printSchema()</em> . Điều này sẽ cung cấp cho ta các cột khác nhau trong khung dữ liệu của chúng tôi cùng với kiểu dữ liệu và điều kiện có thể null cho cột cụ thể đó:</p>

```python
data_car.printSchema()
```
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Sau khi thực hiện xong câu lệnh trên, chương trình sẽ in ra màn hình kết quả sau:</p>

```python
root
 |-- _c0: string (nullable = true)
 |-- _c1: string (nullable = true)
 |-- _c2: string (nullable = true)
 |-- _c3: string (nullable = true)
 |-- _c4: string (nullable = true)
 |-- _c5: string (nullable = true)
 |-- _c6: string (nullable = true)
```

<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Ngoài ra, DataFrame còn cung cấp một số câu lệnh khác khá hữu dụng cho việc thao tác trên dữ liệu và xử lý dữ liệu như</p>

 - <em>describe()</em>: cung cấp cho chúng ta một tóm tắt thống kê của cột nhất định, nếu không được chỉ định, nó cung cấp tóm tắt thống kê của khung dữ liệu.
 - <em>select()</em>: cho phép chọn các cột cụ thể từ khung dữ liệu.
 - ...

## Phần 2: Machine Learning và thư viện <em>mllib</em> trong PySpark
### I. Đôi nét về Machine Learning
<div align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Học máy là một phần của một phần mở rộng hơn được gọi là Trí tuệ nhân tạo. Học máy đề cập đến việc nghiên cứu các mô hình thống kê để giải quyết các vấn đề cụ thể với các mẫu và suy luận. Các mô hình này được “huấn luyện” cho một vấn đề cụ thể bằng cách sử dụng dữ liệu huấn luyện rút ra từ không gian bài toán.</div>

#### 1. Các phạm trù phân loại của học máy (Machine learning)
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Theo một cách tiếp cận, thì thông thường học máy được phân loại thành hai mục là supervised learning và unsupervised learning.</p>

- <em>Supervised learning</em> là việc hoạt động với một tập dữ liệu chứa cả đầu vào và đầu ra mong muốn. <em>Ví dụ</em>:tập dữ liệu chứa các đặc điểm khác nhau của bất động sản và thu nhập cho thuê dự kiến. Học tập có giám sát được chia thành hai tiểu loại lớn được gọi là phân loại và hồi quy:

  - Các thuật toán phân loại có liên quan đến đầu ra phân loại, chẳng hạn như việc một thuộc tính có bị chiếm dụng hay không
  
  - Thuật toán hồi quy có liên quan đến phạm vi đầu ra liên tục, như giá trị của thuộc tính.

- <em>Unsupervised learning</em> hoạt động với một tập hợp dữ liệu chỉ có các giá trị đầu vào . Nó hoạt động bằng cách cố gắng xác định cấu trúc vốn có trong dữ liệu đầu vào. Ví dụ: tìm kiếm các kiểu người tiêu dùng khác nhau thông qua tập dữ liệu về hành vi tiêu dùng của họ.

#### 2. Quy trình học máy
<p align="center"><img src ="https://user-images.githubusercontent.com/77878466/116784048-37b34080-aabc-11eb-993a-b01a64332b65.png" width="70%"/></p>
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Học máy thực sự là một lĩnh vực nghiên cứu liên ngành. Nó yêu cầu kiến thức về lĩnh vực kinh doanh, thống kê, xác suất, đại số tuyến tính và lập trình. Vì điều này rõ ràng có thể trở nên quá tải, tốt nhất nên tiếp cận điều này một cách có trật tự. Mọi dự án học máy nên bắt đầu với một câu lệnh vấn đề được xác định rõ ràng. Việc này phải được thực hiện theo một loạt các bước liên quan đến dữ liệu có thể giải đáp vấn đề. Sau đó, chọn một mô hình xem xét bản chất của vấn đề. Tiếp theo là một loạt quá trình đào tạo và xác nhận mô hình, được gọi là tinh chỉnh mô hình. Cuối cùng, chúng tôi kiểm tra mô hình trên dữ liệu chưa từng thấy trước đó và triển khai nó vào sản xuất nếu đạt yêu cầu.</p>

### II. Thư viện <em>mllib</em> trong PySpark
#### 1. Vài điều về Spark MLlib
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Spark MLlib là một mô-đun nằm trên Spark Core cung cấp các nguyên bản về máy học dưới dạng API. Học máy thường xử lý một lượng lớn dữ liệu để đào tạo mô hình.</p>

<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Khung máy tính cơ sở từ Spark là một lợi ích to lớn. Trên hết, MLlib cung cấp hầu hết các thuật toán thống kê và học máy phổ biến. Điều này giúp đơn giản hóa đáng kể nhiệm vụ làm việc trên một dự án máy học quy mô lớn.</p>

<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Spark MLlib được sử dụng để thực hiện học máy trong Apache Spark. MLlib bao gồm các thuật toán và tiện ích phổ biến. MLlib trong Spark là một thư viện mở rộng của học máy để thảo luận về các thuật toán chất lượng cao và tốc độ cao.</p>

#### 2. Một số công cụ sử dụng Spark.Mllib
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Spark.Mllib là API học máy chính cho Spark. Thư viện Spark.Mllib cung cấp một API cấp cao hơn được xây dựng trên DataFrames để xây dựng các pipeline cho machine learning. Một số công cụ như:</p>

 - Thuật toán ML
 - Featurization
 - Pipelines
 - Persistence
 - Utilities

#### 2.1 Thuật toán Mechine Learning (ML)
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Các thuật toán ML chính là cốt lõi của MLlib. Chúng bao gồm các thuật toán học tập phổ biến như phân loại, hồi quy, phân cụm và lọc cộng tác. MLlib chuẩn hóa các API để giúp kết hợp nhiều thuật toán vào một đường dẫn hoặc quy trình làm việc dễ dàng hơn. Các khái niệm chính là API đường ống, trong đó khái niệm đường ống được lấy cảm hứng từ dự án scikit-learning.</p>

 - <em>Transformer</em>: là một thuật toán biển đổi một Dataframe thành một Dataframe khác. Về mặt lý thuyết nó thực hiện một phương thức transform() dùng để chuyển đỏi một Dataframe thành một Dataframe khác bằng cách thêm một hoặc nhiều cột.

 - <em>Estimator</em>: là một thuật toán phù hợp trên Dataframe để tạo Transformer. Về mặt kỹ thuật, Estimator triển khai phương thức <em>fit()</em> và chấp nhận DataFrame tạo ra một mô hình là một transformer.

#### 2.2 Featurization
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Featurization bao gồm trích xuất, biến đổi, giảm kích thước và lựa chọn:</p>

 - Tính năng trích xuất sẽ được trích xuất từ dữ liệu thô.
 - Tính năng biến đổi bao gồm mở rộng, tái tạo và chỉnh sửa.
 - Tính năng lựa chọn liên quan đến việc chọn một tập hợp con các tính năng cần thiết từ một tập hợp lớn các tính năng.

#### 2.3 Pipelines
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Pipelines giúp kết nối các Estimator và Transformer lại với nhau theo một quy trình của làm việc của ML. Đồng thời nó cũng cung cấp công cụ để đánh giá, xây dựng và điều chỉnh ML pipelines.</p>

#### 2.4 Persistence
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Persistence giúp kết nối các Estimator và Transformer lại với nhau theo một quy trình của làm việc của ML. Đồng thời nó cũng cung cấp công cụ để đánh giá, xây dựng và điều chỉnh ML pipelines.

#### 2.5 Utilities
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Các Utility cho đại số tuyến tính, thống kê và xử lý dữ liệu. Ví dụ mllib.linalg hỗ trợ cho đại số tuyến tính.

#### 3. Các phương thức thư viện mllib cung cấp
<p align="center"><img src ="https://user-images.githubusercontent.com/77878466/116785066-cd050380-aac1-11eb-82eb-84910acdf77b.png" width="90%"/></p>

### III. Sử dụng thư viện Mllib với ngôn ngữ python
#### 1. Hồi quy tuyến tính
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Minh họa cách load dữ liệu training, phân tích cú pháp nó dưới dạng RDD của LabeledPoint. Sau đó chúng ta sẽ sử dụng LinearRegressionWithSGD để xây dựng một mô hình tuyến tính đơn giản để dự đoán các giá trị label. Chúng ta sẽ tính toán sai số trung bình bình phương (Mean Squared Error) ở cuối để đánh giá mức độ phù hợp (goodness of fit)</p>

```python
from pyspark.mllib.regression import LinearRegressionWithSGD
from numpy import array

# Load and phân tích data
data = sc.textFile("mllib/data/ridge-data/lpsa.data")
parsedData = data.map(lambda line: array([float(x) for x in line.replace(',', ' ').split(' ')]))

# Xây dựng mô hình
model = LinearRegressionWithSGD.train(parsedData)

# Đánh giá mô hình trên tập dữ liệu train
valuesAndPreds = parsedData.map(lambda point: (point.item(0),
        model.predict(point.take(range(1, point.size)))))
MSE = valuesAndPreds.map(lambda (v, p): (v - p)**2).reduce(lambda x, y: x + y)/valuesAndPreds.count()
print("Mean Squared Error = " + str(MSE))
```

#### 2. Phân loại nhị phân
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Ví dụ sau đây sẽ hướng dẫn chúng ta load tập dữ liệu, xây dựng mô hình hồi quy Logistic và đưa ra dự đoán kết quả mô hình để tính toán lỗi huấn luyện.</p>

```python
from pyspark.mllib.classification import LogisticRegressionWithSGD
from numpy import array

# Load và phân tích data
data = sc.textFile("mllib/data/sample_svm_data.txt")
parsedData = data.map(lambda line: array([float(x) for x in line.split(' ')]))
model = LogisticRegressionWithSGD.train(parsedData)

# Xây dựng mô hình
labelsAndPreds = parsedData.map(lambda point: (int(point.item(0)),
        model.predict(point.take(range(1, point.size)))))

# Đánh gia mô hình trên tập dữ liệu train
trainErr = labelsAndPreds.filter(lambda (v, p): v != p).count() / float(parsedData.count())
print("Training Error = " + str(trainErr))
```

#### 3. Phân cụm
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Sau khi tải và phân tích dữ liệu, chúng ta sử dụng đối tượng KMeans để phân cụm dữ liệu thành hai cụm. Số lượng các cụm được chuyển đến thuật toán. Sau đó, chúng ta tính toán (Within Set Sum of Squared Error - WSSSE). Ta có thể giảm số đo sai số này bằng cách tăng k.</p>

<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Ngoài ra, chúng ta cũng có thể sử dụng RidgeRegressionWithSGD hoặc LassoWithSGD và so sánh các lỗi trung bình bình phương (Mean Squared Error) khi huấn luyện.</p>

```python
from pyspark.mllib.clustering import KMeans
from numpy import array
from math import sqrt

# Load và phân tích data
data = sc.textFile("kmeans_data.txt")
parsedData = data.map(lambda line: array([float(x) for x in line.split(' ')]))

# Xây dựng mô hình (phân cụm data)
clusters = KMeans.train(parsedData, 2, maxIterations=10,
        runs=30, initialization_mode="random")

# Đánh giá phân cụm dựa trên Within Set Sum of Squared Errors
def error(point):
    center = clusters.centers[clusters.predict(point)]
    return sqrt(sum([x**2 for x in (point - center)]))

WSSSE = parsedData.map(lambda point: error(point)).reduce(lambda x, y: x + y)
print("Within Set Sum of Squared Error = " + str(WSSSE))
```

### 4. Naive Bayes
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; MLlib hỗ trợ Bayes ngây thơ đa thức , thường được sử dụng để phân loại tài liệu. NaiveBayes thực hiện Bayes ngây thơ đa thức. Nó lấy một RDD của LabeledPoint và một tham số làm mịn tùy chọn làm lambdađầu vào và xuất ra một NaiveBayesModel , có thể được sử dụng để đánh giá và dự đoán.</p>

```python
from pyspark.mllib.regression import LabeledPoint
from pyspark.mllib.classification import NaiveBayes

# an RDD of LabeledPoint
data = sc.parallelize([
  LabeledPoint(0.0, [0.0, 0.0])
  ... # more labeled points
])

# Train a naive Bayes model.
model = NaiveBayes.train(data, 1.0)

# Make prediction.
prediction = model.predict([0.0, 0.0])
```

## Phần 3: Tài liệu tham khảo
&nbsp;&nbsp;&nbsp;&nbsp; 1.	http://itechseeker.com/tutorials/apache-spark/lap-trinh-spark-voi-scala/spark-sql-dataset-va-dataframes/

&nbsp;&nbsp;&nbsp;&nbsp; 2.	https://dzone.com/articles/pyspark-dataframe-tutorial-introduction-to-datafra

&nbsp;&nbsp;&nbsp;&nbsp; 3.	https://codetudau.com/xu-ly-du-lieu-voi-spark-dataframe/index.html

&nbsp;&nbsp;&nbsp;&nbsp; 4. https://helpex.vn/article/huong-dan-pyspark-dataframe-gioi-thieu-ve-dataframes-5c6b21e6ae03f628d053c29e

&nbsp;&nbsp;&nbsp;&nbsp; 5. https://www.edureka.co/blog/pyspark-dataframe-tutorial/#what

&nbsp;&nbsp;&nbsp;&nbsp; 6. https://sparkbyexamples.com/pyspark-tutorial/

&nbsp;&nbsp;&nbsp;&nbsp; 7. https://www.analyticsvidhya.com/blog/2020/11/introduction-to-spark-mllib-for-big-data-and-machine-learning/?fbclid=IwAR2jdRLGb1hKqsuHrmOYDCiGTpdbD20VWrSMAjSVxUlwbPmIl3s0RaApaUw

&nbsp;&nbsp;&nbsp;&nbsp; 8. https://ichi.pro/vi/spark-for-machine-learning-su-dung-python-va-mllib-74075263465224?fbclid=IwAR1mcgL68P3_A3ywD1-PhKNTAbnhCQO1mtsdJJgCLIJzhDjzovJBmKVDNus

&nbsp;&nbsp;&nbsp;&nbsp; 9. https://spark.apache.org/docs/0.9.0/mllib-guide.html

&nbsp;&nbsp;&nbsp;&nbsp; 10. https://www.baeldung.com/spark-mlib-machine-learning
