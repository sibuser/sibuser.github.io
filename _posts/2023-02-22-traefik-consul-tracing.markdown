---
layout: post
title:  "How to configure tracing in Traefik"
date:   2023-02-22 22:00:00 +0000
categories: traefik consul tracing
---


{% highlight yaml %}
tracing:
  serviceName: traefik
  spanNameLimit: 50
  jaeger:
    localAgentHostPort: {{ range service "tempo-jaeger-thrift" }}{{ .Address }}:{{ .Port }}{{ end }}
    gen128Bit: true
    traceContextHeaderName: "X-Trace-Id"
    propagation: "jaeger"
    samplingType: const
{% endhighlight %}
