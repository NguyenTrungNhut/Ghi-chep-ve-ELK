# Ghi-chep-ve-ELK

Khi cài đặt ELK trong một mạng có nhiều máy chủ log server mình gặp một trường hợp sau:

Các Elastic mặc định tự móc nối với nhau tạo thành 1 cluster, điều này sẽ có thể gây ra một số vấn đề không mong muốn, Ví dụ khi mình chỉ muốn lấy dữ liệu từ một Elastic duy nhất thôi.

=> Cấu hình lại như sau

- **Đối với Elasticsearch**

`vi /etc/elasticsearch/elasticsearch.yml`

```sh
cluster.name: VDC-IT-Cluster #Tên cluster
node.name: "Elasticsearch_1"   #Tên node trong cluster
```

`service elasticsearch restart`

- **Đối với Logstash**

```sh
output {
  elasticsearch {       node_name => "VDC-IT-Cluster"
                        cluster => "Elasticsearch_1"
                        host => localhost }
  stdout { codec => rubydebug }
}
```

`service logstash restart`

---

Tham khảo

- http://logstash.net/docs/1.4.0/outputs/elasticsearch
- https://github.com/huytm/Cai-dat-rieng-cac-thanh-phan-cho-ELK-va-Cai-dat-Cluster-cho-Elastisearch
