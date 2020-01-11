# Tyk - Elasticsearch - Kibana example

This repository serves as accompaniment or TLDR to https://medium.com/@ahmet_19567/observing-your-api-metrics-with-tyk-elasticsearch-kibana-74e8fd946c39 blog post showing the power of putting an API Gateway
solution in-front of your services, and using in conjunction with a powerful search-engine like Elasticsearch & 
viewing in Kibana.

## Usage

```
docker-compose up -d
```

## Services Exposed

- `localhost:8080` - Tyk Gateway
- `localhost:5601` - Kibana Dashboard

## Examples

Keyless

```shell script
curl -i http://localhost:8080/httpbin/get
HTTP/1.1 200 OK
Access-Control-Allow-Credentials: true
Access-Control-Allow-Origin: *
Content-Length: 207
Content-Type: application/json
Date: Fri, 10 Jan 2020 20:18:53 GMT
Server: gunicorn/19.9.0
X-Ratelimit-Limit: 0
X-Ratelimit-Remaining: 0
X-Ratelimit-Reset: 0

{
  "args": {},
  "headers": {
    "Accept": "*/*",
    "Accept-Encoding": "gzip",
    "Host": "httpbin",
    "User-Agent": "curl/7.67.0"
  },
  "origin": "172.22.0.1",
  "url": "http://httpbin/get"
}
```

JWT Auth Example

```shell script
curl http://localhost:8080/httpbin-jwt/post -d '{"hello":"world"}' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJmb29AYmFyLmNvbSIsIm5hbWUiOiJBaG1ldCBTb29ybWFsbHkiLCJpYXQiOjE1MTYyMzkwMjJ9.8E-X89YnHe6m_jV4Lmyy487VnkCpzuYlsLDceCz4ScU' \
  -H 'content-type: application/json'

{
  "args": {},
  "data": "{\"hello\":\"world\"}",
  "files": {},
  "form": {},
  "headers": {
    "Accept": "*/*",
    "Accept-Encoding": "gzip",
    "Content-Length": "17",
    "Content-Type": "application/json",
    "Host": "httpbin.org",
    "User": "foo@bar.com",
    "User-Agent": "curl/7.67.0"
  },
  "json": {
    "hello": "world"
  },
  "origin": "172.22.0.1, 151.224.16.210, 172.22.0.1",
  "url": "https://httpbin.org/post"
}
```
