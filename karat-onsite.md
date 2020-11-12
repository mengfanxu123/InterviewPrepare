# Karat - onsite

```javascript
const rawData = [
  {
    "title": "Animals",
    "children": [
      {
        "title": "Dogs",
        "children": [
          {
            "title": "Pitbull",
            "children": [
              {
                "title": "English Pitbull",
                "children": null
              },
              {
                "title": "American Pibull"
              }
            ]
          },
          {
            "title": "Chihuahua",
            "children": null
          }
        ]
      },
      {
        "title": "Cats",
        "children": [
          {
            "title": "Calico",
            "children": [
              {
                "title": "British Shorthair",
                "children": null
              },
              {
                "title": "Japenese Bobtail"
              }
            ]
          },
          {
            "title": "Scottish Fold",
            "children": null
          }
        ]
      }
    ]
  }
];
求输出是以下结果
/*
- Animals
   - Dogs
     - Pitbull
       - English Pitbull
       - American Pitbull
     - Chihuahua
   - Cats
     - Calico
       - British Shorthair
       - Japanese Bobtail
     - Scottish Fold
*/

const findCategory = (data, level) => {
  if (data.title != null) {
    let res = "";
    let space = level;
    while (space-- > 0) {
      res += " ";
    }
    res += `-${data.title}`;
    console.log(res);
  }
  if (data.children != null) {
    data.children.forEach((el) => {
      findCategory(el, level + 1);
    });
  }
};

const find = (array) => {
  array.forEach((el) => {
    findCategory(el, 0);
  });
};

const rawData = [
  {
    title: "Animals",
    children: [
      {
        title: "Dogs",
        children: [
          {
            title: "Pitbull",
            children: [
              {
                title: "English Pitbull",
                children: null,
              },
              {
                title: "American Pibull",
              },
            ],
          },
          {
            title: "Chihuahua",
            children: null,
          },
        ],
      },
      {
        title: "Cats",
        children: [
          {
            title: "Calico",
            children: [
              {
                title: "British Shorthair",
                children: null,
              },
              {
                title: "Japenese Bobtail",
              },
            ],
          },
          {
            title: "Scottish Fold",
            children: null,
          },
        ],
      },
    ],
  },
];

find(rawData);

```



1. BQ nice的国人manager，聊得很开心，做的东西很相符，manager也暗示问了下给什么样的package能接这种问题。。
2. nice的美国人，给一个templatestring，比如 "my name is ", 把替换成别的string
3. 不是很友好的美国人，题目是有个坐标系，坐标系里有一堆长方形，创建一个方法来返回一个在这些长方形里的点，这个点出现的概率必须和长方形本身的面积正相关，长方形的边长可以是double类型
4. nice的国人小伙，设计cloud storage system



1. tech deep dive - tell me what happened when a person send an get request. what's happening behind the scene? and work related question
2. house robber. a few lc hard questions. only explain them how you will solve them but don't require you to write code.
3. bq
4. design chat app
5. int to string

Onsite 2. 设计数据结构：假设一个Cloud，有三个method，分别是：添加Server、删除Server和随机返回一个Server，要求每个method的时间复杂度是O\(1\) at worst case。  
  
interface Clound {  
    void addServer\(Server s\)  
    void removeServer\(Server s\)  
    Server randomSelect\(\)  
}  
  
Onsite 3. 李口依伞酒，follow up是李口伊思林，但是只需要返回一个结果即可。  
  
**Onsite 4.** [**system design**](https://link.1point3acres.com/?url=http%3A%2F%2Fwww.educative.io%2Fcourses%2Fgrokking-the-system-design-interview%3Faffiliate_id%3D5749180081373184%2F)**，设计一个简单的Search功能：用户输入Address，返回周边的房屋信息，涉及到了前端的User Experience和后端的Performance等细节。不需要在白板上写，口述+讨论即可。**  
  
面试体验还不错，但是自我感应该没戏。在第一轮和第三轮的聊天过程中，面试官心不在焉+东张西望，而且也很惊讶为何我作为前端要申请后端职位。  


第一题 OOD  设计一个类似于chess 的game;  
第二题 HM纯BQ，why compass之类的，五六个问题需要用它家的principle去回答；  
第三题 coding， 给定一个string和带有mapping关系的dictionary，然后要求用dictionary里的mapping替换掉string中出现的variable；  
比如 ab{c} c:hello --&gt; abhello  
第四题 [系统设计](https://link.1point3acres.com/?url=http%3A%2F%2Fwww.educative.io%2Fcourses%2Fgrokking-the-system-design-interview%3Faffiliate_id%3D5749180081373184%2F) 类似facebook messager， 着重考察db设计

\(1\) 不友善的白人大哥，遲到5分鐘，遭遇一些技術問題剛開始5分鐘他講話我完全聽不到，考了設計一個向zillow / redfin 搜尋存儲過後的 push notification system design spec: 1. 不需要考慮怎麼搜尋的，假設有個event service提供event stream 2. 要能夠客製化push notification在不同channel的發送頻率，比如送到SMS是daily，email是immediately，或什麼其他的channel是weekly之類的 3. 要能提供類似pinterest的collection功能，可以把親朋好友加進去某種儲存的搜尋然後有新的event都會接收到通知 過程之中大哥常常自己偏離主題，不友善，問了很多要是某系統出了error怎麼辦，我回答可以根據response message和exception存儲log或是retry，講得很仔細，但並不知道滿意與否，甚至還問到noSQL掛了該怎麼辦，我也都有給出答案，但過程中聽不出來他想要什麼答案

\(2\) 第二輪題目很冗長的算法題，給你兩個API，一個提供兩個定點\(可以是公車站or metro station\)之間trasportation的時間，一個提供兩個定點之間有什麼交通方式直達，可能是走路，地鐵或者是公車，題目很多都要自己定義 ，最後寫了一個DFS加上畫圖解釋

\(3\) 第三輪 李口 散久斯 \(4\) 第四輪 BQ半小時，不太記得問了什麼，一些以前做過的project之類的



第一轮: Manager轮，主要是BQ。面着面着才发现是General Interview，面完之后match组，白舔了半天😂  
第二轮: 面试官粘了一段巨长的代码，是Person和Name的一段逻辑，里面有六小问，比如找出出现频次最高的5个first name, last name，既是first name也是last name的name等等。难点在于快速理解代码的逻辑然后写出相应代码，要写的代码本身都很简单，要和面试官沟通快速理解代码才是核心。  
第三轮: 给一段range \[start, end\]，找到range里含prime factor数量最多的所有数字 \(一开始是说prime factor只考虑 2 3 5，后面的followup就是如果prime factor list变了，不是2 3 5了，代码是不是能根据任意的prime factor list work\)。比如range是\[2,6\]，输出list \[4,6\]，因为4=2\*2, 6=2\*3各自有两个prime factor。如果range是\[2,8\]，输出是list\[8\]，因为8=2\*2\*2有三个factor，是range里prime factor个数最多的。我是用memorization search/dp做的。  
第四轮: [系统设计](https://link.1point3acres.com/?url=http%3A%2F%2Fwww.educative.io%2Fcourses%2Fgrokking-the-system-design-interview%3Faffiliate_id%3D5749180081373184%2F)，设计一个Spotify，主要围绕在后端table的设计，搜索功能以及playlist功能。这轮是答得最好的，之前在工作中就用过lucidchart，画图画的很顺，面试官直接在面试中就给了positive feedback。



1.project dive，聊天 45分钟  
2.口定：散吧领 散吧要  
3.口定：叄就死  
4.[系统设计](https://link.1point3acres.com/?url=http%3A%2F%2Fwww.educative.io%2Fcourses%2Fgrokking-the-system-design-interview%3Faffiliate_id%3D5749180081373184%2F)：设计康帕斯的search



vo 4轮  
第一轮是印度姐姐  
input是 List&lt;Station&gt; , start, end  
有两个api 一个是getMethod \(start, end\)  会返回从start 到end 可乘坐的交通工具比如地铁公交走路  
另一个是getTime\(start, end, method\) 返回从start 到end 通过这个交通工具所需要的时间  
求start 到 end 需要的最短的时间。。。  
想了想本质是一个有权重无向图求shortest weighted path..  
写完了dryrun的时候发现有点问题。。印度姐姐说就这样吧我看差不多了你不用写print了。。后来面完仔细想了想不是问题啊只是print的时候需要处理下啊。。。  
  
第二轮是白人小哥  
压缩/解压 string 还没力扣上那么复杂 xxxyyy -&gt; 3x3y xyz-&gt; xyz  
  
第三轮亚裔小哥  
交流有点费劲， 设计一个**定时发邮件系统**  
  
第四轮 bq  
hm是ex[亚麻](https://link.1point3acres.com/?url=https%3A%2F%2Fwww.amazon.com%2F)某南亚大国人士。。。。就正常bq + 问问题  
问了问觉得在这个公司当老板和在亚麻当老板的区别。。 他说wlb好多了，理由是不用半夜oncall hmmmm

第一轮，国人大哥，coding  
说给个只有1和0组成的2d matrix, 1代表房子，0代表没有房子，房子之间需要修栅栏隔起来，房子跟空地之间不需要，求给一个点\(x, y\),问该点所在的小区（即所有连在一片的房子）有多少栅栏。  
follow up，如果房子和边界之间也要修栅栏怎么算。  
  
第二轮，国人大哥， coding  
刷题网而把而  
  
第三轮，国人大哥，[system design](https://link.1point3acres.com/?url=http%3A%2F%2Fwww.educative.io%2Fcourses%2Fgrokking-the-system-design-interview%3Faffiliate_id%3D5749180081373184%2F)  
大概就是设计一个网站，然后用户可以批量上传照片，后台会处理然后对图片进行标记，比如图片里有pizza，burger，之类的，花的时间会有几十秒，这期间要实时反馈给用户后台标记的进展。返回标记之后，用户可以修改标记，然后最后确认提交。  
  
第四轮，天竺director，bq  
主要问工作经历啊，各种bq  
  
第五轮，亚裔vp  
看面试安排上写着什么技术deep dive，但他太能说了，基本上都是在介绍自己公司，也不知道要考察啥。

第一轮coding, 白人小哥，给一个string pattern 和 一个string，要求替换掉string里面match pattern的sub-string

用matcher / pattern 做的

第二轮coding，calculator 只有加减，followup是有乘除

第三轮system design, Instgram

第四轮bq，日常问题

## Calculator 

```javascript
// just has "+" and "-"
class Solution {
    public int calculate(String s) {
        if(s == null || s.length() == 0) return 0;
        int num = 0;
        char sign = '+';
        int res = 0;
        for (int i = 0; i < s.length(); i++){
          if(Character.isDigit(s.charAt(i))){
            num = num*10 + s.charAt(i) - '0';
          }
          if(!Character.isDigit(s.charAt(i)) && s.charAt(i) != ' ' || i == s.length() - 1){
            if(sign == '+'){
              res += num;
            }
            if(sign == '-'){
              res -= num;
            }
            num = 0;
            sign = s.charAt(i);
          }
        }
      return res;
    }
}

// has + - * /
class Solution {
    public int calculate(String s) {
        if(s == null || s.length() == 0) return 0;
        int num = 0;
        char sign = '+';
        int res = 0;
        Stack<Integer> stack = new Stack<>();
        for (int i = 0; i < s.length(); i++){
          if(Character.isDigit(s.charAt(i))){
            num = num*10 + s.charAt(i) - '0';
          }
          if(!Character.isDigit(s.charAt(i)) && s.charAt(i) != ' ' || i == s.length() - 1){
            if(sign == '+'){
              stack.push(num);
            }
            if(sign == '-'){
             stack.push(-num);
            }
            if(sign == '*'){
              stack.push(stack.pop() * num);
            }
             if(sign == '/'){
              stack.push(stack.pop() / num);
            }
            num = 0;
            sign = s.charAt(i);
          }
        }
      while(!stack.isEmpty()){
        res += stack.pop();
      }
      return res;
    }
}
```

```javascript
class RandomizedSet {

    /** Initialize your data structure here. */
   List<Integer> nums;
   Map<Integer, Integer> map;
    Random rand = new Random();
    public RandomizedSet() {
        nums = new ArrayList<>();
        map = new HashMap<>();
    }
    
    /** Inserts a value to the set. Returns true if the set did not already contain the specified element. */
    public boolean insert(int val) {
        if(map.get(val) != null) return false;
        map.put(val, nums.size());
        nums.add(val);
      return true;
    }
    
    /** Removes a value from the set. Returns true if the set contained the specified element. */
    public boolean remove(int val) {
        if(map.get(val) == null) return false;
        // swap if not last;
        if(map.get(val) < nums.size() - 1){
          int last = nums.get(nums.size() - 1);
          nums.set(map.get(val), last);
          map.put(last, map.get(val));
        }
      nums.remove(nums.size() - 1);
      map.remove(val);
      return true;
    }
    
    /** Get a random element from the set. */
    public int getRandom() {
        return nums.get(rand.nextInt(nums.size()));
    }
}

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet obj = new RandomizedSet();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
 
 class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        List<Integer> res = new ArrayList<>();
        if(nums == null || nums.length == 0) return res;
        Map<Integer, Integer> map = new HashMap<>();
        for (int num : nums){
            int count = map.getOrDefault(num, 0) + 1;
            map.put(num, count);
        }
        PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> map.get(a) - map.get(b));
        for (int num : map.keySet()){
            pq.add(num);
            if(pq.size() > k){
                pq.poll();
            }
        }
        while(!pq.isEmpty()){
            res.add(pq.poll());
        }
        Collections.reverse(res);
        return res;
    }
}
```

