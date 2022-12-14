---
layout: post
title:  "Optimal Strategy"
date:   2022-12-14 14:31:49 +0900
tags: Optimal Strategy
categories: jekyll update
---

## 0번 idx부터 2번 idx까지
[2, 7, 40]<br>
{% highlight ruby %}
[ {7, 2}, {    } ]<br>
[ {    }, {40, 7}]
{% endhighlight %}

내가 40을 선택하면 상대방이 2, 7중에 최적 선택을 하는 경우와 같습니다. 그러므로 왼쪽칸 7, 2의 두번재 값을 내가 가지고 와야 합니다. 그래서 40+2 = 42가 됩니다.

내가 2를 선택하면 상대방이 40, 7중에 최적 선택을 하는 경우와 같습니다. 그러므로 아래칸 40, 7의 두번재 값을 내가 가지고 와야 합니다. 그래서 2 + 7 = 9가 됩니다.

`Math.max(coins의 right + dp[i][j-1].right, coins의 left + dp[i+1][j].right);`


## 1번 idx부터 3번 idx까지
[7, 40, 19]

내가 19를 선택하면 상대방이 7, 40중에 최적 선택을 하는 경우와 같습니다. 그러므로 왼쪽칸 40, 7의 두번재 값을 내가 가지고 와야 합니다. 그래서 19+7 = 26이 됩니다.

내가 7을 선택하면 상대방이 40, 19중에 최적 선택을 하는 경우와 같습니다. 그러므로 아래칸 40, 19의 두번재 값을 내가 가지고 와야 합니다. 그래서 7+19 = 26이 됩니다.

`Math.max(coins의 right + dp[i][j-1].right, coins의 left + dp[i+1][j].right);`

{% highlight ruby %}
[ {40, 7}, {    } ]<br>
[ {    }, {40, 19}]
{% endhighlight %}

왼쪽과 오른쪽 저장하기
Optimal Strategy에서 왼쪽과 오른쪽을 정하는 로직 또한 까다롭습니다.
<br>[2, 7, 40, 19]<br>
2,7<br>
7,40<br>
40,19

i, j i는 1개씩 늘고 j도 i따라 늘고

i = 1일때 j가 i만큼 늘어난다면<br>
0,1<br>
1,2<br>
2,3

i = 2일때 j가 i만큼 늘어난다면<br>
0, 2<br>

ex) for i { for j } 는 안됨<br>
0 0<br>
0 1<br>
0 2<br>
1 0<br>
1 1<br>
1 2

```java
public class OptStrategy {
    public static void main(String[] args) {
        int[] coins = new int[]{2, 7, 40, 19};
        int[][] dp = new int[coins.length][coins.length];
        for (int i = 0; i < coins.length; i++) {
            for (int j = i; j < coins.length; j++) {
                if(j==0)
                    dp[i][j] = coins[i];
                else
                    dp[i][j] = dp[i][j - 1] + coins[i];
            }
        }

        for (int j = 0; j < coins.length; j++) {
            System.out.println(Arrays.toString(dp[j]));
        }
    }
}
```
