
# Monitoring System
## Khái niệm
* Monitoring system là một hệ thống theo dõi, ghi lại các trạng thái, hoạt động của máy tính hay ứng dụng một cách liên tục

## Tại sao cần Monitoring system?
* Dựa vào kết quả của hệ thống monitoring chúng ta có thể điều chỉnh việc sử dụng tài nguyên (cpu,ram,disk,....) sao cho phù hợp
* Ngăn chặn các sự cố có thể xảy ra, nếu có xảy ra chúng ta có thể phát hiện sớm hơn.
* Giảm thiểu thời gian quản lý hệ thống

**=> Một hệ thống Monitoring tốt sẽ giúp tăng năng suất, chất lượng sản phẩm**
## Các đặc điểm của một hệ thống monitoring
* Xử lí real time
* Có hệ thống cảnh báo
* Visualization
* Có khả năng tạo reports
* Có khả năng cài cắm các plugins
## Thành phần

![](/image/grafana2.png)

Thông thường một hệ thống monitoring thường có 4 thành phần chính:

**Collector**: Được cài trên các agent (các máy muốn monitor), có nhiệm vụ collect metrics của host và gửi về database. Ví dụ: Cadvisor, Telegraf, Beat,...

**Database**: Lưu trữ các metrics mà collector thu thập được, thường thì chúng ta sẽ sử dụng các time series database. Ví dụ như ElasticSearch, InfluxDB, Prometheus, Graphite.

**Visualizer**: Có nhiệm vụ trực quan hóa các metrics thu thập được qua các biểu đồ bảng,...Ví dụ: Kibana, Grafana, Chronograf.

**Alerter**: Gửi thông báo đến cho sysadmin khi có sự cố xảy ra

**Có rất nhiều stack phổ biến như:**

* Logstash-Elasticsearch-Kibana
* Prometheus-Node Exporter-Grafana
* Telegraf-InfluxDB-Grafana
## Telegraf - InfluxDB - Grafana Stack
![](/image/grafana3.png)

**Telegraf** và **Influxdb** đều là sản phẩm của InfluxData, cả hai đều mà mã nguồn mở và được viết bởi Go. Mặc dù InfluxData cung cấp một stack hoàn chỉnh để monitor với Chronograf để visualize và Kapacitor để alerting (TICK stack) nhưng chúng ta có thể sử dụng Grafana để thay thế cho cả Chronograf lẫn Kapacitor.
## Telegraf
* Telegraf là một agent để collecting và reporting metrics và data được viết bởi Go.
* Nó có thể tích hợp để collect nhiều loại nguồn dữ liệu khác nhau của metrics, events, và logs trực tiếp từ containers và system mà nó chạy trên đó. Nó cũng có thể pull metrics từ các third-party APIs, Kafka. Nó cũng có nhiều output plugin để gửi metrics thu thập được tới nhiều dạng datastores, services, message queues khác nhau như  InfluxDB, Graphite, OpenTSDB, Datadog, Librato, Kafka, ...

## InfluxDB
* InfluxDB là một Time Series Database (là database được tối ưu hóa để xử lý dữ liệu chuỗi thời gian, các dãy số được lập chỉ mục theo thời gian. )
* InfluxDB được sử dụng để lưu các dữ liệu cho các trường hợp liên quan đến một lượng lớn time-stamped data, bao gồm DevOps monitoring, log data, application metrics, IoT sensor data, và real-time analytics. Nó có thể tự động xóa các dữ liệu cũ, không cần thiết và cung cấp một ngôn ngữ giống SQL để tương tác với dữ liệu.
* Data trong InfluxDB được tổ chức dưới dạng time series. Time series có thể có một hoặc nhiều points, mỗi point là một mẫu rời rạc các số liệu. Point gồm:

    * Time (timestamp)
    * Một measurement (ví dụ "cpu_load")
    * Ít nhất một key-value field (giá trị đo được, ví dụ "value=0.64", hoặc "temperature=21.2")
    * Không hoặc nhiều key-value tags chứa metadata của value (ví dụ “host=server01”, “region=EMEA”, “dc=Frankfurt”)
    
## Grafana
* Grafana là một công cụ mã nguồn mở cho phép chúng ta truy vấn, hiển thị, cảnh báo các số liệu thu thập được

## Tính năng
* Hiển thị số liệu theo nhiều dạng biểu đồ khác nhau

* Cảnh báo qua nhiều kênh như Email, telegram, slack

* Hỗ trợ nhiều loại Database như InfluxDB, Graphite, ElasticSearch,...

* Cung cấp nhiều Plugin, nhiều Dashboard template.

* Khi lấy được metric từ các thiết bị, Grafana sẽ sử dụng metric đó để phân tích và tạo ra Dashboard mô tả trực quan các metric cần thiết cho việc monitoring ví dụ như : Ram, Disk, Network, Session.

![](/image/grafana1.png)



