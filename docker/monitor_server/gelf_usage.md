To send logs to Logstash over GELF
curl -XPOST http://graylog.example.org:12202/gelf -p0 -d '{"short_message":"Hello there", "host":"example.org", "facility":"test", "_foo":"bar"}'

To send logs to Logstash over TCP
cat ~/access_log | nc localhost 5000
