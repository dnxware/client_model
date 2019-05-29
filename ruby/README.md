# dnxware Ruby client model

Data model artifacts for the [dnxware Ruby client][1].

## Usage

Build the artifacts from the protobuf specification:

    make build

While this Gem's main purpose is to define the dnxware data types for the
[client][1], it's possible to use it without the client to decode a stream of
delimited protobuf messages:

```ruby
require 'open-uri'
require 'dnxware/client/model'

CONTENT_TYPE = 'application/vnd.google.protobuf; proto=io.dnxware.client.MetricFamily; encoding=delimited'

content = open('http://localhost:9100/metrics', 'Accept' => CONTENT_TYPE).read
buffer = Beefcake::Buffer.new(content)

while family = dnxware::Client::MetricFamily.read_delimited(buffer)
  puts family
end
```

[1]: https://github.com/dnxware/client_ruby
