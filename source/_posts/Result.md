---
title: Result
date: 2020-11-06 20:32:02
tags:
- Swift
- iOS
- docs
- translation
---
## Result
原文：[Apple Developer Documentation](https://developer.apple.com/documentation/swift/result)
文档摘录翻译
### Result 定义
```Swift
@frozen enum Result<Success, Failure> where Failure : Error
```

### Result 应用
#### 编写可能失败`Failable`的异步API
编写可能失败的函数、方法或其他API时，可以在声明中使用throws关键字来标示此API可抛出异常。但是你不能将throws关键字用于异步返回的API，此时可用`Result`枚举来保存异步调用时的结果信息，并使用关联值来携带有关的值。
```Swift
let queue = DispatchQueue(label: “com.example.queue”)

enum EntropyError: Error {
    case entropyDepleted
}

struct AsyncRandomGenerator {
    static let entropyLimit = 5
    var count = 0
    
    mutating func fetchRemoteRandomNumber(
        completion: @escaping (Result<Int, EntropyError>) -> Void
    ) {
        let result: Result<Int, EntropyError>
        if count < AsyncRandomGenerator.entropyLimit {
            // Produce numbers until reaching the entropy limit.
            result = .success(Int.random(in: 1…100))
        } else {
            // Supply a failure reason when the caller hits the limit.
            result = .failure(.entropyDepleted)
        }
        
        count += 1
        
        // Delay to simulate an asynchronous source of entropy.
        queue.asyncAfter(deadline: .now() + 2) {
            completion(result)
        }
    }
}
```
#### 保存抛出异常函数的结果
有时，你需要保留函数或其他抛出异常表达式的整个结果。例如，你可能需要序列化结果或将其作为值传递给程序的其他部分。在这些情况下，请使用Result类型来捕获可能失败的操作的结果。
##### 转换抛出异常表达式为Result
你可以使用`Result`枚举的`init(catching:)`进行转换：
```Swift
let singleSample = Result { try UnreliableRandomGenerator().random() }
```

##### 转换Result到抛出异常表达式
```Swift
let integerResult: Result<Int, Error> = .success(5)
do {
    let value = try integerResult.get()
    print("The value is \(value).")
} catch error {
    print("Error retrieving the value: \(error)")
}

```
#blog/tech/Swift
