# edu kafka-StatefulSet

بعد از اجرا :
```
kubectl apply -f kafka-statefulset.yaml
```
3️⃣ بررسی وضعیت
```
kubectl get pods -l app=kafka
```
خروجی:

```
kafka-0   Running
kafka-1   Running
kafka-2   Running
```
4️⃣ تست Kafka
ورود به یکی از Brokerها:
```
kubectl exec -it kafka-0 -- bash
```
ساخت Topic:
```
kafka-topics.sh \
--create \
--topic test-topic \
--bootstrap-server kafka-0.kafka:9092 \
--replication-factor 3 \
--partitions 3
```
لیست Topicها:
```
kafka-topics.sh --list --bootstrap-server kafka-0.kafka:9092
```
5️⃣ نکات حرفه‌ای / مصاحبه‌ای 🔥
مورد	توضیح
```
StatefulSet	Kafka نیاز به identity ثابت
Headless Service	discovery نودها
Replication=3	High Availability
KRaft	حذف ZooKeeper
PVC	حفظ دیتا بعد از Restart
```
6️⃣ منابع حداقلی پیشنهادی
Resource	مقدار
CPU	1 core
RAM	2GB
Disk	10GB × 3
