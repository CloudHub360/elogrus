# ElasticSearch Hook for [Logrus](https://github.com/Sirupsen/logrus) <img src="http://i.imgur.com/hTeVwmJ.png" width="40" height="40" alt=":walrus:" class="emoji" title=":walrus:"/>

Elasticsearch version | Elastic version -| Package URL
----------------------|------------------|------------
5.x                   | 5.0              | [`gopkg.in/sohlich/elogrus.v2`](http://gopkg.in/sohlich/elogrus.v2)
2.x                   | 3.0              | [`gopkg.in/sohlich/elogrus.v1`](http://gopkg.in/sohlich/elogrus.v1)


## Usage

```
go get gopkg.in/sohlich/elogrus.v2
```



```go
package main

import (
	"github.com/sirupsen/logrus"
	"gopkg.in/sohlich/elogrus.v2"
	"gopkg.in/olivere/elastic.v5"
)


func main() {
	log := logrus.New()
	client, err := elastic.NewClient(elastic.SetURL("http://localhost:9200"))
	if err != nil {
		log.Panic(err)
	}	
	hook, err := elogrus.NewElasticHook(client, "localhost", logrus.DebugLevel, "mylog")
	if err != nil {
		log.Panic(err)
	}	
	log.Hooks.Add(hook)

	log.WithFields(logrus.Fields{
		"name": "joe",
		"age":  42,
	}).Error("Hello world!")
}
```
