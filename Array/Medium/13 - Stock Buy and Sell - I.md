
https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/

```java
class Solution {
    public int maxProfit(int[] prices) {
        int minPrice=prices[0];
        int maxProfit=0;

        for(int i=1; i<prices.length; i++) {
            int profit = prices[i]-minPrice;
            minPrice = Math.min(minPrice, prices[i]);

            if(profit > maxProfit) {
                maxProfit = Math.max(profit, maxProfit);
            }
        }

        return maxProfit;
    }
}
```
