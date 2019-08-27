# Design Pattern
## Design principle 
  设计中不要一味追求封装， 如果两个相对独立的功能封装在一起， 满足不了“高内聚”的需求，反而，降低了调用时的灵活性。 合理的方式，把两个拆分的功能暴露出来。 
## Visitor 
通常的面向对象类的设计把对象的成员和方法封装在一起 如果在一个体系中 类上的方法经常发生添改的现象， 则可以把方法拿出来专门做成visitor类，本身仅仅留下一个Accept函数用来接收visitor的里面的方法


有点像体检， 体检的主体是“我们” ， 本来我们的方法有测血压/查B超/视力/...,  直接把这个方法绑定到体检者对象里，是常规的封装方式。 Visitor方式把这个方法提出来单独成立类，或者说医生，比方说测血压医生/B超医生，让各个医生去访问各个体检人员吧。


## offline notes of focade & stragy & bridge
https://raw.githubusercontent.com/garfielder/notes/master/attachment/stragy_bridge.jpg
