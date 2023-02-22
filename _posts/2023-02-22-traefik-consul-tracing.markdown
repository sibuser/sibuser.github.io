---
layout: post
title:  "Enabling tracing in Traefik with Consul"
date:   2023-02-22 14:50:30 +0000
tags: traefik consul tracing
---
{% highlight yaml %}
tracing:
  serviceName: traefik
  spanNameLimit: 50
  jaeger:
    localAgentHostPort: {% raw %}{{ range service "tempo-jaeger-thrift" }}{{ .Address }}:{{ .Port }}{{ end }}{% endraw %}
    gen128Bit: true
    traceContextHeaderName: "X-Trace-Id"
    propagation: "jaeger"
    samplingType: const
{% endhighlight %}