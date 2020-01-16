# facebook



1. flatten array, follow up是怎么用非递归完成，我答的是用 Array.prototype.splice，具体可以直接Google
2. 给你两个object然后要根据第二个排除第一个，具体看glassdoor或者地里
3. emitter
4. 如何批量移除所有setInterval 把原来的函数替换掉套一层自己的就完了
5. 在两个不用的dom树里面找相同的node 具体看glassdoor有题目源代码



1. call是什么 - 我直接答完并且说了和apply区别 他就没再问apply了
2. 什么是closure
3. closure就是一个function 这个function可以access parent scope的variable
4. 一个html image怎么知道他load了还是没load - 加个onload 没call就是没load完
5. stack和queue的区别 - 不就是 FILO FIFO 的区别嘛
6. var和let/const有什麽区别 - var有变量提升 会有奇怪的bug var没有block scope let没有这些奇奇怪怪的feature let不可以declare twice in same scope 而且有block scope const就是let的immutable version
7. how to simulate a stack data structure in js - Array .push\(\) .pop\(\)
8. dom是什么data structure 如果complete binary DOM tree depth是多少 - 当然是tree啦 就是log\(n\)

   他还问我爲什麽 我有点懵比 我说那你都说是complete binary DOM tree那不就本质上是一个complete binary tree 然后by definition depth就是log\(n\) 似乎他也就是想问这个答案

9. 一個星期之後終於想起來那一題了 問我什麼是event delegation  **补充内容 \(2019-11-20 13:01\):** 又想起來一個 Array和Object的區別
10. 上周五的四轮面试，基本挂了 第一轮： 算法：一个BST和一个Target，找出closest node to the target，要求logN复杂度 算出岛的个数， 利口200 然后是算面积和周长，没做完时间就到了，算法基础较弱。。。

    第二轮：BQ 感觉回答的不好，很多题都没准备到，回答的有些犹豫和慌张，比如 和同事的最大conflict，和leader的最大conflict，和其他组合作的最大confilct，别人一直拖着活不完成导致你没发开始改怎么处理， 用户紧急的需求和 你不做其他team member就会被block的情况，改怎么处理（假设都只有你能完成）

    吃饭，周五的伙食还不错，有酸奶，中餐做的不错，还有两种点心，和面试官聊了聊项目组业务和项目的发展方向。

    第三轮： UX + 前端的项目设计：很新颖的方式，感觉面试官很有水平，只画了图，没有要求写代码，很考验知识点宽度和深度。 提出了一些需求，根据要求画出大致的UX wireframe 然后该怎么设计这个项目，问了怎么配置LESS，怎么配置Redux，和后端怎么配合，怎么做到前后端分离。。。 前端怎么优化项目，针对React有哪些优化方式 中间穿插了很多的前端基础面试题，和React面试题。还聊了React16的源码优化，异步渲染，fiber原理。源码我只看了fiber部分，其他主要是听面试官说，时不时插上两句自己的想法。 这一轮面完感觉以后面试可以从很多方面去扩展，收获很多。

    第四轮： 前端面试，地里基本都有的（html+css+js） [https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=549730&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3088%5D%5Bvalue%5D%3D11%26searchoption%5B3088%5D%5Btype%5D%3Dradio%26searchoption%5B3046%5D%5Bvalue%5D%3D2%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline](https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=549730&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3088%5D%5Bvalue%5D%3D11%26searchoption%5B3088%5D%5Btype%5D%3Dradio%26searchoption%5B3046%5D%5Bvalue%5D%3D2%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline) 我被问了2，5 写autoComplete的时候主动加上了debounce和infinite scroll，把cache给忘了。。。 然后就聊天



<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>HR&#x7535;&#x8BDD;&#x804A;&#x5929;</b>
        <br />&#x548C;HR&#x804A;&#x5929;&#xFF0C;&#x4E86;&#x89E3;&#x80CC;&#xFF0C;&#x6BD4;&#x8F83;&#x8BE6;&#x7EC6;&#x7684;&#x4ECB;&#x7ECD;&#x4E86;&#x9879;&#x76EE;&#x7EC4;&#x3002;
        <br
        />&#x975E;&#x5E38;&#x5947;&#x602A;&#x7684;&#x662F;&#xFF0C;&#x804A;&#x5B8C;&#x5929;&#x4EE5;&#x540E;&#xFF0C;&#x76F4;&#x63A5;&#x544A;&#x8BC9;&#x6211;&#x5927;&#x6982;package&#xFF1A;base140k,
        stock 120k&#x56DB;&#x5E74;&#xFF0C;bonus&#x5927;&#x6982;&#x662F;base&#x7684;10%&#xFF0C;signon&#x4E0D;&#x786E;&#x5B9A;&#x3002;
        <br
        />
        <br /><b>&#x6280;&#x672F;&#x5E97;&#x9762;</b>
        <br />&#x804A;&#x5929;&#xFF0C;&#x4ECB;&#x7ECD;&#x81EA;&#x5DF1;&#x548C;&#x6700;&#x8FD1;&#x7684;&#x9879;&#x76EE;&#x3002;&#x95EE;&#x4E86;&#x4E00;&#x4E9B;&#x96BE;&#x70B9;&#x3002;
        <br
        />&#x63A5;&#x4E0B;&#x6765;&#x662F;coding
        <br />&#x7B2C;&#x4E00;&#x9898;&#xFF1A;function animateRight(elem, duration,
        distance){}
        <br />&#x8BA9;&#x4E00;&#x4E2A;dom&#x5143;&#x7D20;&#x5728;duration&#x7684;&#x65F6;&#x95F4;&#x4E4B;&#x5185;&#xFF0C;&#x5411;&#x53F3;&#x79FB;&#x52A8;distance&#xFF0C;&#x8981;smoothly&#x3002;
        <br
        />
        <br />&#x7B2C;&#x4E8C;&#x9898;&#xFF1A;&#x5229;&#x53E3; &#x8033;&#x4E45;
        <br />&#x7B2C;&#x4E09;&#x9898;&#xFF1A;&#x800C;&#x5C31;&#x53D8;&#x79CD;&#x9898;&#xFF0C;&#x548C;&#x7B2C;&#x4E8C;&#x9898;&#x5DEE;&#x4E0D;&#x591A;
        <br
        />&#x9762;&#x7B97;&#x6CD5;&#x6709;&#x70B9;&#x610F;&#x5916;&#xFF0C;&#x4E24;&#x9898;&#x90FD;&#x662F;&#x5728;&#x9762;&#x8BD5;&#x5B98;&#x63D0;&#x793A;&#x4E0B;&#x505A;&#x51FA;&#x6765;&#x7684;&#x3002;&#x770B;&#x5730;&#x91CC;&#x7684;&#x9762;&#x7ECF;&#x8FD8;&#x6CA1;&#x6709;&#x5728;&#x5E97;&#x9762;&#x9762;&#x7B97;&#x6CD5;&#x7684;&#x3002;
        <br
        />
        <br />&#x7136;&#x540E;&#x8BA9;&#x6211;&#x95EE;&#x95EE;&#x9898;&#xFF0C;&#x53D1;&#x73B0;&#x9762;&#x8BD5;&#x5B98;&#x5BF9;&#x524D;&#x7AEF;&#x4E0D;&#x592A;&#x719F;&#x6089;&#xFF0C;&#x4ED6;&#x4E5F;&#x8BF4;&#x5F88;&#x4E45;&#x6CA1;&#x505A;&#x524D;&#x7AEF;&#x4E86;&#xFF0C;&#x53EA;&#x662F;&#x88AB;&#x62C9;&#x6765;&#x9762;&#x8BD5;&#x3002;
        <br
        />&#x4F30;&#x8BA1;&#x56E0;&#x4E3A;&#x8FD9;&#x624D;&#x95EE;&#x4E86;&#x6211;&#x4E24;&#x9053;&#x7B97;&#x6CD5;&#x9898;&#x5427;&#x3002;
        <br
        />
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p></p>
        <ol></ol>
      </td>
    </tr>
  </tbody>
</table>