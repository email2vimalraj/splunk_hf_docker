docker run --platform linux/amd64 -d --name splunk-hf \
 -p 8000:8000 \
 -p 8088:8088 \
 -p 9997:9997 \
 -e SPLUNK_START_ARGS="--accept-license" \
 -e SPLUNK_PASSWORD="changeme" \
 -e SPLUNK_HEC_TOKEN="testtoken" \
 -e SPLUNK_ENABLE_HEC=true \
 -v /Users/vimalrajselvam/development/playground/splunk-hf/etc:/opt/splunk/etc \
 splunk/splunk:latest

curl -k https://localhost:8088/services/collector/event \
 -H "Authorization: Splunk testtoken" \
 -H "Content-Type: application/json" \
 -d '{
"event": "Test log from CatA via HEC",
"sourcetype": "custom_type",
"host": "testhost",
"index": "CatA"
}'
