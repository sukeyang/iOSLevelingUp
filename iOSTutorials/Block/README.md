# Block


### 案例 1

```
@interface House ()

@property (nonatomic, strong) Person *person;

@end

@implementation House

- (instancetype)init {
    self = [super init];
    if (self) {
        
        // self 持有 person
        _person = [Person new];
        [_person setCallback:^(Person *person) {
            
//            _person.name = @"xxx"; // 这里会导致 block 持有 self，而 block 是 person 对象所持有的，这就导致了循环引用
            person.name = @"xxx";  // 但是这样就不会导致循环引用，因为这里是作为一个参数传进来的，不会捕获 self
        }];
        
    }
    return self;
}

@end
```

详见 demo 中的示例代码和 clang 重写后的 C++ 代码。
