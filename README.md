### stuff-classifier
---
https://github.com/alexandru/stuff-classifier

```
gem install stuff-classifier
```

```ruby
require 'stuff-classifier'
cls = StuffClassifier::Bayes.new("Cats or Dogs")
cls = StuffClassifier::TfIdf.new("Cats or Dogs")
cls = StuffClassifier::TfIdf.new("Cats or Dogs", :stemming => false)
cls.ignore_words = [ 'the', 'my', 'i', 'dont' ]

cls.train(:dog, "Dogs are awesome, cats too. I love my dog")
cls.train(:cat, "Cats are more preferred by software develpers. I never could stand cats.")

cls.classify("This test is about cats.")
# => :cat
cls.classify("Cats or Dogs?")
# => :dog

store = StuffClassifier::RedisStorage.new(@key)
store = StuffClassifier::RedisStorage.new(@key, {host: 'my.redis.server.com', port: 4829})

store = StuffClassifier::FileStorage.new(@storage_path)
StuffClassifier::Base.storage = store
cls = StuffClassifier::Bayes.new("Cats of Dogs", :storage => store)
cls.save_state
StuffClassifier::Bayes.open("Cats or Dogs") do |cls|
end
StuffClassifier::Bayes.new("Cats or Dogs", :purge_state => true)

cls1 = StuffClassifier::Bayes.new("Cats or Dogs")
cls2 = StuffClassifier::Bayes.new("True or False")
cls3 = StuffClassifier::Bayes.new("Span or Ham")
```

