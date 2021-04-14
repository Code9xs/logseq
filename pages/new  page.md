---
title: new  page
---

## 二分查找（O(log n)）

**BinarySearch**

> 一般而言，对于包含n 个元素的**有序**列表，用二分查找最多需要log2 n 步，而简单查找最多需要n 步。

二分查找仅仅对有序列表有效

```java
// 二分查找对应数字索引
public class BinarySearch {
    public static String binarySearch(int[] list,int item){
        int low = 0;
        int high = list.length;

        while (low <= high){
            int mid = (low + high) / 2;
            int guess = list[mid];
            if (guess == item){
                return String.valueOf(mid);
            } else if (guess > item){
                high = mid -1;
            } else {
                low = mid + 1;
            }
        }
        return "不存在该值";
    }

    public static void main(String[] args) {
        int[] myList = {1, 3, 5, 7, 9};
        System.out.println(binarySearch(myList,6));
    }
}
```





练习
1.1 假设有一个包含128个名字的有序列表，你要使用二分查找在其中
查找一个名字，请 问最多需要几步才能找到？

log~2~128 = 7步

1.2 上面列表的长度翻倍后，最多需要几步？

log~2~256 = 8步



**一些常见的大O运行时间**

- O (log n )，也叫对数时间 ，这样的算法包括二分查找。
- O (n )，也叫线性时间 ，这样的算法包括简单查找。
- O (n * log n )，这样的算法包括第4章将介绍的快速排序——一种速度较快的排序算法。
- O (n 2 )，这样的算法包括第2章将介绍的选择排序——一种速度较慢的排序算法。
- O (n !)，这样的算法包括接下来将介绍的旅行商问题的解决方案——一种非常慢的算法。







- 算法的速度指的并非时间，而是操作数的增速。
- 谈论算法的速度时，我们说的是随着输入的增加，其运行时间将以什么样的速度增加。
- 算法的运行时间用大O表示法表示。
- O (log n )比O (n )快，当需要搜索的元素越多时，前者比后者快得越多。



**小结**

- 二分查找的速度比简单查找快得多。
- O (log n )比O (n )快。需要搜索的元素越多，前者比后者就快得越多。
- 算法运行时间并不以秒为单位。
- 算法运行时间是从其增速的角度度量的。
- 算法运行时间用大O表示法表示。



# 选择排序（O(n^2^)）

**SelectionSort**

**链表**

链表优势在于随机插入元素，但是链表不擅长随即查找元素，我需要查看链表最后一个元素，我就需要查看倒数第二个元素来得到最后一个元素的存储地址。

**数组**

数组的优势在于随机查找元素



![image-20210401103806279](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113236.png)

![image-20210401104024506](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113237.png)



>需要指出的是，仅当能够立即访问要删除的元素时，删除操作的运行时间才为O (1)。通常我们都记录了链表的第一个元素和最后一个元素，因此删除这些元素时运行时间为O (1)。-------> 不考虑链表查找到需要删除元素的步骤，删除操作，链表优于数组



```java
package com.code9xs.datastruct;


import java.util.ArrayList;

// 选择排序
public class SelectionSort {
    static int findSmallest(ArrayList<Integer> arr){
        int smallest = arr.get(0);
        int smallestIndex = 0;
        for (int i = 0;i < arr.size();i++){
            if (arr.get(i) < smallest){
                smallest = arr.get(i);
                smallestIndex = i;
            }
        }
        return smallestIndex;
    }

    static ArrayList<Integer> selectionSort(ArrayList<Integer> arr){
        ArrayList<Integer> newArr = new ArrayList<Integer>();
        int size = arr.size();
        for (int i = 0;i<size;i++){
            int smallestIndex = findSmallest(arr);
            newArr.add(arr.get(smallestIndex));
            arr.remove(smallestIndex);

        }
        return newArr;
    }

    public static void main(String[] args) {
        ArrayList<Integer> arr = new ArrayList<Integer>(){{
            add(99);
            add(32);
            add(85);
            add(44);
            add(20);
        }};
        System.out.println("arr:"+arr);
        ArrayList<Integer> selectionSort = selectionSort(arr);
        System.out.println("newArr"+selectionSort);
    }
}
```



**小结**

- 计算机内存犹如一大堆抽屉。
- 需要存储多个元素时，可使用数组或链表。
- 数组的元素都在一起。
- 链表的元素是分开的，其中每个元素都存储了下一个元素的地址。
- 数组的读取速度很快。
- 链表的插入和删除速度很快。
- 在同一个数组中，所有元素的类型都必须相同（都为int、double等）。





# 递归

编写递归函数时，必须告诉它何时停止递归。正因为如此，每个递归函 数都有两部分：**基线条件** （base case）和**递归条件** （recursive case）。递归条件指的是函数调用自己，而基线条件则指的是函数不再调用自己，从而避免形成无限循环。

```java
package com.code9xs.datastruct;

import java.util.Timer;

public class Recursive {
    static void countDown(int time){
        if (time <= 0){
            System.out.println("计时结束!!!");
            return;
        }
        System.out.println("倒计时:"+time);
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        countDown(time - 1);
    }

    static int fact(int basicNum){
        if (basicNum == 1)
            return 1;
        else
            return basicNum * fact(basicNum - 1);
    }

    public static void main(String[] args) {
//        countDown(5);
        System.out.println(fact(5));
    }
}

```



**小结**

- 递归指的是调用自己的函数。
- 每个递归函数都有两个条件：基线条件和递归条件。
- 栈有两种操作：压入和弹出。
- 所有函数调用都进入调用栈。
- 调用栈可能很长，这将占用大量的内存。





# 快速排序(O(nlog n))

- 学习分而治之。有时候，你可能会遇到使用任何已知的算法都无法解决的问题。优秀的算法学家遇到这种问题时，不会就此
  放弃，而是尝试使用掌握的各种问题解决方法来找出解决方案。分而治之是你学习的第一种通用的问题解决方法。
- 学习快速排序——一种常用的优雅的排序算法。快速排序使用分而治之的策略。



divide and conquer，D&C--------> 分而治之



**使用D&C解决问题的过程包括两个步骤。**

(1) 找出基线条件，这种条件必须尽可能简单。
(2) 不断将问题分解（或者说缩小规模），直到符合基线条件。



快速排序步骤：

(1) 选择基准值。
(2) 将数组分成两个子数组：小于基准值的元素和大于基准值的元素。
(3) 对这两个子数组进行快速排序。



```java
package com.code9xs.datastruct;

import java.util.ArrayList;

// 分治法------快速排序
public class QuickSort {
    // 循环
    static int sum(int[] arr){
        int total = 0;
        for (int i = 0;i < arr.length;i++){
            total += arr[i];
        }
        return total;
    }

    // 递推
    static int sum(ArrayList<Integer> arr){
        if (arr.size() == 0){
            return 0;
        }
        int firstNum = arr.get(0);
        arr.remove(0);
        return firstNum + sum(arr);
    }

    static int findMaxNum(int[] arr){
        int max = arr[0];
        for (int i = 1;i < arr.length;i++){
            if (arr[i] > max){
                max = arr[i];
            }
        }
        return max;
    }

    static ArrayList<Integer> quickSort(ArrayList<Integer> arr){
        ArrayList<Integer> result = new ArrayList<Integer>();
        if (arr.size() < 2)
            return arr;
        // 选定基准值
        int povit = arr.get(0);
        ArrayList<Integer> less = new ArrayList<Integer>();
        ArrayList<Integer> greater = new ArrayList<Integer>();
        for (int i = 1;i < arr.size();i++){
            // 小于基准值
            if (arr.get(i) < povit){
                less.add(arr.get(i));
             // 大于基准值
            } else {
                greater.add(arr.get(i));
            }
        }
        result.add(povit);
        quickSort(less);
        quickSort(greater);
        less.addAll(result);
        less.addAll(greater);
        return less;
    }

    public static void main(String[] args) {
        int[] numArr = {8,4,6};
//        System.out.println(sum(numArr));
        ArrayList<Integer> arr = new ArrayList<Integer>(){{
            add(9);
            add(3);
            add(7);
            add(12);
            add(33);
        }};
//        System.out.println(sum(arr));
//        System.out.println(findMaxNum(numArr));
        System.out.println(quickSort(arr));

    }
}
```



**练习**

4.8 根据数组包含的元素创建一个乘法表，即如果数组为[2, 3, 7, 8,10]，首先将每个元素 都乘以2，再将每个元素都乘以3，然后将每个元
素都乘以7，以此类推。



**小结**

- D&C将问题逐步分解。使用D&C处理列表时，基线条件很可能是空数组或只包含一个元素的数组。
- 实现快速排序时，请**随机**地选择用作基准值的元素。快速排序的平均运行时间为O (n log n )。
- 大O表示法中的常量有时候事关重大，这就是快速排序比合并排序快的原因所在。
- 比较简单查找和二分查找时，常量几乎无关紧要，因为列表很长时，O (log n )的速度比O (n )快得多。





# 散列表

> 散列函数是这样的函数，即无论你给它什么数据，它都还你一个数字。



如果用专业术语来表达的话，我们会说，散列函数“将输入映射到数字”。你可能认为散列函数输出的数字没什么规律，但其实散列函数必
须满足一些要求。

- 它必须是一致的。例如，假设你输入apple时得到的是4，那么每次输入apple时，得到的都必须为4。如果不是这样，散列表将毫无用
  处。
- 它应将不同的输入映射到不同的数字。例如，如果一个散列函数不管输入是什么都返回1，它就不是好的散列函数。最理想的情况是，将不同的输入映射到不同的数字。



> 散列表也是使用数组来存储数据，所以其获取元素的速度和数组一样快。



**小结**

- 模拟映射关系；
- 防止重复；
- 缓存/记住数据，以免服务器再通过处理来生成它们。



![image-20210401155357810](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113238.png)





散列表的填装因子

![image-20210401155821351](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113239.png)



一个不错的经验规则是：一旦填装因子大于0.7，就调整散列表的长度。





**小结**

- 你可以结合散列函数和数组来创建散列表。
- 冲突很糟糕，你应使用可以最大限度减少冲突的散列函数。
- 散列表的查找、插入和删除速度都非常快。
- 散列表适合用于模拟映射关系。
- 一旦填装因子超过0.7，就该调整散列表的长度。
- 散列表可用于缓存数据（例如，在Web服务器上）。
- 散列表非常适合用于防止重复。







# 广度优先搜索O (V + E )





> O (V + E )，其中V 为顶点（vertice）数，E 为边数。
>
> 解决最短路径问题（shorterst-path problem）的算法被称为**广度优先搜索** 。





队列是一种先进先出 （First In First Out，**FIFO**）的数据结构，而栈是一种后进先出 （Last In First Out，**LIFO**）的数据结构。





![image-20210402171344777](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113240.png)



**Person.java**

```java
package com.code9xs.datastruct;

public class Person {
    private String name;
    private String professional;

    public Person() {
    }

    public String getName() {
        return name;
    }

    public Person(String name, String professional) {
        this.name = name;
        this.professional = professional;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getProfessional() {
        return professional;
    }

    public void setProfessional(String professional) {
        this.professional = professional;
    }
}
```



BreadthFirstSearch.java

```java
package com.code9xs.datastruct;

import java.util.*;

// 广度优先搜索
public class BreadthFirstSearch {


    public static void main(String[] args) {
        Person you = new Person("you","farmer");
        Person bob = new Person("bob","farmer");
        Person alice = new Person("alice","farmer");
        Person claire = new Person("claire","farmer");
        Person anuj = new Person("anuj","farmer");
        Person peggy = new Person("peggy","mangoDealers");
        Person thom = new Person("thom","farmer");
        Person jonny = new Person("jonny","farmer");
// mangoDealers

        Map<String, List<Person>> graph = new HashMap<>();
        graph.put("you",new ArrayList<Person>(){{
            add(alice);
            add(bob);
            add(claire);
        }});
        graph.put("bob",new ArrayList<Person>(){{
            add(anuj);
            add(peggy);
        }});
        graph.put("alice",new ArrayList<Person>(){{
            add(peggy);
        }});
        graph.put("claire",new ArrayList<Person>(){{
            add(thom);
            add(jonny);
        }});
        graph.put("anuj",new ArrayList<Person>());
        graph.put("peggy",new ArrayList<Person>(){{
            add(you);
        }});
        graph.put("thom",new ArrayList<Person>());
        graph.put("jonny",new ArrayList<Person>());


        Queue<Person> person = new LinkedList<Person>();
        person.offer(you);
        // 创建列表保存已检查过的盆友
        List<Person> checkedPerson = new ArrayList<Person>();
        while (!person.isEmpty()){
            Person p = person.peek();
            if (p.getProfessional().equals("mangoDealers")){
                System.out.println(p.getName() + "是芒果经销商");
                break;
            } else {
                checkedPerson.add(p);
                for (Person p1:graph.get(p.getName())){
                    if (!checkedPerson.contains(p1)){
                        System.out.println(p.getName() +"的朋友"+p1.getName()+"入队");
                        person.offer(p1);
                    } else {
                        System.out.println(p1.getName() + "已检查过，不再入队");
                    }
                }
            }
            System.out.println(p.getName() + "出队");
            person.poll();
            // 如果队列为空，输出结果，while判断为false，循环结束
            if (person.isEmpty())
                System.out.println("没有人是芒果经销商");
        }
    }
}
```



**小结**

- 广度优先搜索指出是否有从A到B的路径。
- 如果有，广度优先搜索将找出最短路径。
- 面临类似于寻找最短路径的问题时，可尝试使用图来建立模型，再使用广度优先搜索来解决问题。
- 有向图中的边为箭头，箭头的方向指定了关系的方向，例如，rama→adit表示rama欠adit钱。
- 无向图中的边不带箭头，其中的关系是双向的，例如，ross - rachel表示“ross与rachel约会，而rachel也与ross约会”。
- 队列是先进先出（FIFO）的。
- 栈是后进先出（LIFO）的。
  你需要按加入顺序检查搜索列表中的人，否则找到的就不是最短路径，因此搜索列表必须是队列。
- 对于检查过的人，务必不要再去检查，否则可能导致无限循环。





# 狄克斯特拉算法



> Dijkstra's algorithm 狄克斯特拉算法只适用于有向无环图（directed acyclic graph，DAG）
>
> 如果有负权边，就不能使用狄克斯特拉算法 。
>
> 在包含负权边的图中，要找出最短路径，可使用另一种算法——贝尔曼-福德算法 （Bellman-Ford algorithm）





狄克斯特拉算法包含4个步骤。

1. 找出“最便宜”的节点，即可在最短时间内到达的节点。
2. 更新该节点的邻居的开销，其含义将稍后介绍。
3. 重复这个过程，直到对图中的每个节点都这样做了。
4. 计算最终路径。



1. 从开始节点出发，选择开销最小的一个点B
2. 找出B点的所有"邻居"，计算从起点经过B点到"邻居"的开销，与开销表中从起点到该点的开销对比
   1. 前者小于后者，更新开销表，并更新邻居点父节点为B
   2. 前者大于后者，一切不变
3. 记录已经处理过的点
4. 重复如此，直到处理完所有点

```java
package com.code9xs.datastruct;

import java.util.*;

// 狄克斯特拉算法
public class DijkstraAlgorithm {
    // 记录已经处理过的节点
    private static List<String> processed = new ArrayList<String>();
    public static void main(String[] args) {
        Map<String,Map<String,Double>> graph = new HashMap<>();

        graph.put("start",new HashMap<String,Double>(){{
            put("a",6.0);
            put("b",2.0);
        }});
        graph.put("a",new HashMap<String,Double>(){{
            put("fin",1.0);
        }});
        graph.put("b",new HashMap<String,Double>(){{
            put("a",3.0);
            put("fin",5.0);
        }});
        graph.put("fin",new HashMap<String,Double>());

        Map<String,Double> costs = new HashMap<String,Double>();
        costs.put("a",6.0);
        costs.put("b",2.0);
        costs.put("fin",1.0/0.0);

        Map<String,String> parents = new HashMap<>();
        parents.put("a","start");
        parents.put("b","start");
        parents.put("fin",null);
        // 在未处理的节点中找出开销最小的节点
        String node = findLowestCostNode(costs);
        // 这个while循环在所有节点都被处理过后结束
        while (node != null){
            double cost = costs.get(node);
            Map<String,Double> neighbors = graph.get(node);
            // 遍历当前节点的所有邻居
            for (Map.Entry<String,Double> entry:neighbors.entrySet()){
                double newCost = cost + entry.getValue();
                // 如果经当前节点前往该邻居更近
                if (costs.get(entry.getKey()) > newCost){
                    // 就更新该邻居的开销
                    costs.put(entry.getKey(),newCost);
                    // 同时将该邻居的父节点设置为当前节点
                    parents.put(entry.getKey(),node);
                }
            }
            processed.add(node);
            node = findLowestCostNode(costs);
        }
        System.out.println(parents);
        System.out.println(costs);

    }

    static String findLowestCostNode(Map<String,Double> costs){
        String lowestCostNode = null;
        double lowestCost = 1.0/0.0;
        for (Map.Entry<String,Double> entry:costs.entrySet()){
            if (lowestCost > entry.getValue() && !processed.contains(entry.getKey())){
                lowestCost = entry.getValue();
                lowestCostNode = entry.getKey();
            }
        }
        return lowestCostNode;
    }
}
```





# 贪婪算法（O (n ^2^ )）

> 贪婪算法可以得到近似解，一般会用来解决目前没有很好的办法解决的NP完全问题

**判断问题为NP完全问题**

- 元素较少时算法的运行速度非常快，但随着元素数量的增加，速度会变得非常慢。
- 涉及“所有组合”的问题通常是NP完全问题。
- 不能将问题分成小问题，必须考虑各种可能的情况。这可能是NP完全问题。
- 如果问题涉及序列（如旅行商问题中的城市序列）且难以解决，它可能就是NP完全问题。
- 如果问题涉及集合（如广播台集合）且难以解决，它可能就是NP完全问题。
- 如果问题可转换为集合覆盖问题或旅行商问题，那它肯定是NP完全问题。

贪婪算法并非在任何情况下都行之有效，但它易于实现！

**集合覆盖问题**

```java
package com.code9xs.datastruct;

import java.util.*;

// 贪婪算法
public class GreedyAlgorithm {

    public static void main(String[] args) {
        Set<String> statesNeeded = new HashSet<String>(){{
            add("mt");
            add("wa");
            add("or");
            add("id");
            add("nv");
            add("ut");
            add("ca");
            add("az");
        }};
        Map<String, HashSet<String>> stations = new HashMap<String, HashSet<String>>(){{
            put("kone",new HashSet<String>(){{
                add("id");
                add("nv");
                add("ut");
            }});
            put("ktwo",new HashSet<String>(){{
                add("wa");
                add("id");
                add("mt");
            }});
            put("kthree",new HashSet<String>(){{
                add("or");
                add("nv");
                add("ca");
            }});
            put("kfour",new HashSet<String>(){{
                add("nv");
                add("ut");
            }});
            put("kfive",new HashSet<String>(){{
                add("ca");
                add("az");
            }});
        }};

        Set<String> finalStations = new HashSet<String>();
        while (!statesNeeded.isEmpty()){
            String bestStation = null;
            Set<String> statesCovered = new HashSet<String>();
            for (Map.Entry<String,HashSet<String>> entry:stations.entrySet()){
                Set<String> covered = intersection(statesNeeded,entry.getValue());
                if (covered.size() > statesCovered.size()){
                    bestStation = entry.getKey();
                    statesCovered = covered;
                    removeStates(statesNeeded, entry.getValue());
                    finalStations.add(bestStation);
                }
            }
        }
        System.out.println(finalStations);
    }

    private static Set<String> intersection(Set<String> l1,Set<String> l2){
        Set<String> set = new HashSet<String>();
        for (String s:l1){
            set.add(s);
        }
        set.retainAll(l2);
        return set;
    }

    private static boolean removeStates(Set<String> statesNeeded,HashSet<String> states){
        for (String s:states){
            statesNeeded.remove(s);
        }
        return true;
    }
}

```

![image-20210403120935143](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113241.png)

假设你办了个广播节目，要让全美50个州的听众都收听得到。为此，你需要决定在哪些广播台播出。在每个广播台播出都需要支付费用，因此你力图在尽可能少的广播台播出。现有广播台名单如下。

![image-20210403121000198](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113242.png)

每个广播台都覆盖特定的区域，不同广播台的覆盖区域可能重叠。

![image-20210403121022928](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113243.png)



**小结**

- 贪婪算法寻找局部最优解，企图以这种方式获得全局最优解。
- 对于NP完全问题，还没有找到快速解决方案。
- 面临NP完全问题时，最佳的做法是使用近似算法。
- 贪婪算法易于实现、运行速度快，是不错的近似算法。



# 动态规划

> 动态规划可以得到某些问题的最优解

假设你要去野营。你有一个容量为6磅的背包，需要决定该携带下面的哪些东西。其中每样东西都有相应的价值，价值越大意味着越重要：

- 水（重3磅，价值10）；
- 书（重1磅，价值3）；
- 食物（重2磅，价值9）；
- 夹克（重2磅，价值5）；
- 相机（重1磅，价值6）。



|                      | 1      | 2                   | 3             | 4                 | 5                   | 6                 |
| -------------------- | ------ | ------------------- | ------------- | ----------------- | ------------------- | ----------------- |
| 水（重3磅，价值10）  |        |                     |               |                   |                     |                   |
| 书（重1磅，价值3）   | 书/3   | 书/3                | 水/10         | 水，书/13         | 水，书/13           | 水，书/13         |
| 食物（重2磅，价值9） | 书/3   | 食物/9              | 水/10         | 水，书/13         | 水，食物/19         | 水，书，食物/22   |
| 夹克（重2磅，价值5） | 书/3   | 食物/9              | 食物，书/12   | 食物，夹克/14     | 水，食物/19         | 水，书，食物/22   |
| 相机（重1磅，价值6） | 相机/6 | 食物/9   相机，书/9 | 食物，相机/15 | 食物，相机，书/18 | 食物，相机，夹克/20 | 水，食物，相机/25 |



- 动态规划可帮助你在给定约束条件下找到最优解。在背包问题中，你必须在背包容量给定的情况下，偷到价值最高的商品。
- 在问题可分解为彼此独立且离散的子问题时，就可使用动态规划来解决。



- 每种动态规划解决方案都涉及网格。
- 单元格中的值通常就是你要优化的值。在前面的背包问题中，单元格的值为商品的价值。
- 每个单元格都是一个子问题，因此你应考虑如何将问题分成子问题，这有助于你找出网格的坐标轴。



**最长公共子串**

费曼算法 （Feynman algorithm）。这个算法是以著
名物理学家理查德·费曼命名的，其步骤如下。

1. 将问题写下来。
2. 好好思考。
3. 将答案写下来。



需要注意的一点是，这个问题的最终答案并不在最后一个单元格中！对于前面的背包问题，最终答案总是在最后的单元格中。但对于最长公共子串问题，答案为网格中最大的数字——它可能并不位于最后的单元格中。



![image-20210403135048726](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113244.png)

```java
package com.code9xs.datastruct;

// 动态规划算法
public class DynamicProgramming {
    public static void main(String[] args) {
        String longestString = findLongestString("hish", "fish");
        System.out.println(longestString);
    }

    static String findLongestString(String str1,String str2){
        char[] char1 = str1.toCharArray();
        char[] char2 = str2.toCharArray();
        String longestString = "";
        int[][] index = new int[str1.length()][str2.length()];
        for (int i = 0;i < char1.length;i++){
            for (int j = 0;j <= i;j++){
                if (String.valueOf(char1[i]).equals(String.valueOf(char2[j]))){
                    longestString += char1[i];
                    if (i > 0 && j > 0){
                        index[i][j] = index[i-1][j-1] +1;
                    } else {
                        index[i][j] = 0;
                    }
                }
            }
        }
        return longestString;
    }
}

```







**最长公共子序列**



![image-20210403135102035](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113245.png)



- 生物学家根据最长公共序列来确定DNA链的相似性，进而判断度两种动物或疾病有多相似。最长公共序列还被用来寻找多发性硬化症治疗方案。
- 你使用过诸如git diff 等命令吗？它们指出两个文件的差异，也是使用动态规划实现的。
- 前面讨论了字符串的相似程度。编辑距离 （levenshtein distance）指出了两个字符串的相似程度，也是使用动态规划计算得到的。编辑距离算法的用途很多，从拼写检查到判断用户上传的资料是否是盗版，都在其中。
- 你使用过诸如Microsoft Word等具有断字功能的应用程序吗？它们如何确定在什么地方断字以确保行长一致呢？使用动态规划！

练习：请绘制并填充用来计算blue和clues最长公共子串的网格。

|      |  b   |  l   |  u   |  e   |
| :--: | :--: | :--: | :--: | :--: |
|  c   |  0   |  0   |  0   |  0   |
|  l   |  0   |  1   |  0   |  0   |
|  u   |  0   |  0   |  2   |  0   |
|  e   |  0   |  0   |  0   |  3   |
|  s   |  0   |  0   |  0   |  0   |



**小结**

- 需要在给定约束条件下优化某种指标时，动态规划很有用。
- 问题可分解为离散子问题时，可使用动态规划来解决。
- 每种动态规划解决方案都涉及网格。
- 单元格中的值通常就是你要优化的值。
- 每个单元格都是一个子问题，因此你需要考虑如何将问题分解为子问题。
- 没有放之四海皆准的计算动态规划解决方案的公式。





# K最近邻算法



> K最近邻 （k-nearest neighbours，KNN）算法



假设你是Netflix，要为用户创建一个电影推荐系统。从本质上说，这类似于前面的水果问题！你可以将所有用户都放入一个图表中。

![image-20210413105537631](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113246.png)

这些用户在图表中的位置取决于其喜好，因此喜好相似的用户距离较近。假设你要向Priyanka推荐电影，可以找出五位与他最接近的用户。

![image-20210413105552831](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113247.png)

假设在对电影的喜好方面，Justin、JC、Joey、Lance和Chris都与Priyanka差不多，因此他们喜欢的电影很可能Priyanka也喜欢！
有了这样的图表以后，创建推荐系统就将易如反掌：只要是Justin喜欢的电影，就将其推荐给Priyanka。

![image-20210413105610674](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113248.png)

但还有一个重要的问题没有解决。在前面的图表中，相似的用户相距较近，但如何确定两位用户的相似程度呢？

**特征抽取**

在前面的水果示例中，你根据个头和颜色来比较水果，换言之，你比较的特征是个头和颜色。现在假设有三个水果，你可抽取它们的特征。

![image-20210413105650836](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113249.png)

再根据这些特征绘图。

![image-20210413105705651](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113250.png)

从上图可知，水果A和B比较像。下面来度量它们有多像。要计算两点的距离，可使用毕达哥拉斯公式。

![image-20210413105722045](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113251.png)

例如，A和B的距离如下。

![image-20210413105735693](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113252.png)

A和B的距离为1。你还可计算其他水果之间的距离。

![image-20210413105751096](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113253.png)

这个距离公式印证了你的直觉：A和B很像。



**回归**

- 分类就是编组；
- 回归就是预测结果（如一个数字）。





> **余弦相似度**
> 前面计算两位用户的距离时，使用的都是距离公式。还有更合适的公式吗？在实际工作中，经常使用余弦相似度 （cosinesimilarity）。假设有两位品味类似的用户，但其中一位打分时更保守。他们都很喜欢Manmohan Desai的电影Amar Akbar Anthony ，但Paul给了5星，而Rowan只给4星。如果你使用距离公式，这两位用户可能不是邻居，虽然他们的品味非常接近。



**OCR**

> OCR指的是光学字符识别 （optical character recognition），这意味着你可拍摄印刷页面的照片，计算机将自动识别出其中的文字。Google使用OCR来实现图书数字化。



**小结**

- KNN用于分类和回归，需要考虑最近的邻居。
- 分类就是编组。
- 回归就是预测结果（如数字）。
- 特征抽取意味着将物品（如水果或用户）转换为一系列可比较的数字。
- 能否挑选合适的特征事关KNN算法的成败。



# 二叉树查找（O(log n)）

> 在前面的二分查找示例中，每当用户登录Facebook时，Facebook都必须在一个庞大的数组中查找，核实其中是否包含指定的用户名。前面说过，在这种数组中查找时，最快的方式是二分查找，但问题是每当有新用户注册时，都必须将其用户名插入该数组并重新排序，因为二分查找仅在数组有序时才管用。如果能将用户名插入到数组的正确位置就好了，这样就无需在插入后再排序。为此，有人设计了一种名为二叉查找树 （binary search tree）的数据结构。

![image-20210414101447448](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113254.png)





# MapReduce

> 有一种特殊的并行算法正越来越流行，它就是分布式算法 。在并行算法只需两到四个内核时，完全可以在笔记本电脑上运行它，但如果需要
> 数百个内核呢？在这种情况下，可让算法在多台计算机上运行。MapReduce是一种流行的分布式算法，你可通过流行的开源工具Apache
> Hadoop来使用它。



**分布式算法为何很有用**
假设你有一个数据库表，包含数十亿乃至数万亿行，需要对其执行复杂的SQL查询。在这种情况下，你不能使用MySQL，因为数据表的行数超过数十亿后，它处理起来将很吃力。相反，你需要通过Hadoop来使用MapReduce！

又假设你需要处理一个很长的清单，其中包含100万个职位，而每个职位处理起来需要10秒。如果使用一台计算机来处理，将耗时数月！如果使用100台计算机来处理，可能几天就能完工。

分布式算法非常适合用于在短时间内完成海量工作，其中的MapReduce基于两个简单的理念：**映射（map ）函数和归并（reduce ）函数**。



**映射函数**
映射函数很简单，它接受一个数组，并对其中的每个元素执行同样的处理。例如，下面的映射函数将数组的每个元素翻倍。

```python
>>> arr1 = [1, 2, 3, 4, 5]
>>> arr2 = map(lambda x: 2 * x, arr1)
[2, 4, 6, 8, 10]
```



**归并函数**
归并函数可能令人迷惑，其理念是将很多项归并为一项。映射是将一个数组转换为另一个数组。

![image-20210414102616682](https://raw.githubusercontent.com/Code9xs/pic/main/note/20210414113255.png)

```python
>>> arr1 = [1, 2, 3, 4, 5]
>>> reduce(lambda x,y: x+y, arr1)
15
```
