# Refactoring Notes

## Banlence encapsulation and  flexiablity
 Do you try to encapsulate everything, trust the user.  Encapsulating too much can make the design more complex. 
 
 ## Do not over refactoring 
 Do know plan too much on what might be used in the future.



## 敢于放弃
重构前， 可能不了解代码的每个细节，重构中发现了潜在的问题，增加了重构的难度和测试的代价。此时当有壮士断腕的决心， 放弃重构，重回正轨

## 有限test下的重构 
由于测试资源不宜获取，只能进行有限的测试，这种情况西下，应该只保留最基本的逻辑在 HAL实现层

## Short Tips
   * Do not do two irrelevant tasks in the same loop
      * Split them into two.  Performance is usually not a problem. 

