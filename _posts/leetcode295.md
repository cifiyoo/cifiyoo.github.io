#### 数据流的中位数

中位数是有序列表中间的数。如果列表长度是偶数，中位数则是中间两个数的平均值。

例如，`[2,3,4]` 的中位数是` 3`；`[2,3]` 的中位数是` (2 + 3) / 2 = 2.5`

设计一个支持以下两种操作的数据结构：

`void addNum(int num) `- 从数据流中添加一个整数到数据结构中。
`double findMedian()` - 返回目前所有元素的中位数。
链接：https://leetcode-cn.com/problems/find-median-from-data-stream

##### 样例

```
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2
```

##### 题解

```c++
class MedianFinder {
public:
    /** initialize your data structure here. */
    priority_queue<int, vector<int>, less<int>> s;//降序
    priority_queue<int, vector<int>, greater<int>> q;//升序

    MedianFinder() {

    }
    void addNum(int num) {
        if(s.empty()) {
            s.push(num);
        }
        else if(num > s.top()) {
            q.push(num);
            if(q.size() == s.size()+2) {
                s.push(q.top());
                q.pop();
            }
        }
        else {
            s.push(num);
            if(s.size() == q.size()+2) {
                q.push(s.top());
                s.pop();
            }
        }
        return;
    }
    
    double findMedian() {
        if(q.size()<s.size()) {
            return s.top();
        }
        else if(q.size() >s.size()) {
            return q.top();
        }
        else{
            return (double(q.top()+s.top())/2);
        }
    }
};

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder* obj = new MedianFinder();
 * obj->addNum(num);
 * double param_2 = obj->findMedian();
 */
```

由于数据流输入，需要动态的数据结构维护。取中位数问题，直接`sort`超时。用两个优先队列完成大顶堆+小顶堆的结构，控制两个堆的元素数量相差不超过`1`。大顶堆`s.top()`为堆顶最大值，小顶堆`q.top()`为堆顶最小值，故对于一个升序序列，`s`维护前半段，`q`维护后半段，则可以使`s.top()`和`q.top()`为序列中位数。

基础的大顶堆+小顶堆问题，认为`CF ：B`题水平。

