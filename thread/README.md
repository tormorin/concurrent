# 线程操作
## 1.创建线程
```c++
#include <iostream>
#include <thread>
using namespace std;
void threadFunc() {
    cout << "Hello from thread" << endl;
}
int main() {
    thread t(threadFunc); // 创建线程
    t.join(); // 等待线程结束
    return 0;
}
```
## 2.线程同步
```c++
#include <iostream>
#include <thread>
#include <mutex>
using namespace std;
int x = 0;
mutex mtx;
void threadFunc() {
    for (int i = 0; i < 10; i++) {
        mtx.lock(); // 加锁
        x++;
        cout << "x = " << x << endl;
        mtx.unlock(); // 解锁
    }
}
int main() {
    thread t1(threadFunc);
    thread t2(threadFunc);
    t1.join();
    t2.join();
    return 0;
}
```