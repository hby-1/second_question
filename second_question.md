# 两个列表的最小索引总和

假设 Andy 和 Doris 想在晚餐时选择一家餐厅，并且他们都有一个表示最喜爱餐厅的列表，每个餐厅的名字用字符串表示。

你需要帮助他们用**最少的索引**和找出他们**共同喜爱的餐厅**。 如果答案不止一个，则输出所有答案并且不考虑顺序。你可以假设答案总是存在。

## 示例 1:

>### 输入: 
>list1 = ["Shogun", "Tapioca Express", "Burger King", "KFC"]
list2 = ["Piatti", "The Grill at Torrey Pines", "Hungry Hunter Steakhouse", "Shogun"]
>### 输出: 
>["Shogun"]
>### 解释:
>他们只能选择其中一种餐厅，Shogun

## 示例 2:

>### 输入:
>list1 = ["Shogun", "Tapioca Express", "Burger King", "KFC"]    
list2 = ["KFC", "Shogun", "Burger King"]
>### 输出:
>["Shogun"]
>### 解释:
> 他们都只喜欢其中一种餐厅，并且这道题的答案是 ["Shogun"]

## 代码:

1.

    public class Solution {
        public string[] FindRestaurant(string[] list1, string[] list2) {
            List<string> L=new List<string>{};
            List<int> Num=new List<int>{};
            List<string> bothList=new List<string>{};
            int minSum=-1;
            int count=0;
            for(int i=0;i<list1.Length;i++){
                for(int n=0;n<list2.Length;n++){
                    if(list1[i]==list2[n]){
                        L.Add(list1[i]);
                        Num.Add(i+n);
                        if(minSum==-1){
                            minSum=i+n;
                        }
                        else{
                            if(minSum>(i+n)){
                                minSum=i+n;
                            }
                        }
                        break;
                    }
                }
            }
            for(int i=0;i<Num.Count;i++){
                if(Num[i]==minSum){
                    bothList.Add(L[i]);
                }
            }
            string[] ourList=bothList.ToArray();
            return ourList;
        }
    }

2.

    public class Solution {
        public string[] FindRestaurant(string[] list1, string[] list2) {
            Dictionary<string, int> dict = new Dictionary<string, int>();
            for (int i = 0; i < list1.Length; i++) {
                dict[list1[i]] = i;
            }

            List<string> result = new List<string>();
            int minIndexSum = int.MaxValue;

            for (int j = 0; j < list2.Length; j++) {
                if (dict.ContainsKey(list2[j])) {
                    int indexSum = dict[list2[j]] + j;
                    if (indexSum < minIndexSum) {
                        minIndexSum = indexSum;
                        result.Clear();
                        result.Add(list2[j]);
                    } else if (indexSum == minIndexSum) {
                        result.Add(list2[j]);
                    }
                }
            }

            return result.ToArray();
        }    
    }

3.

    public class Solution {
        public string[] FindRestaurant(string[] list1, string[] list2) {
            int minSum = int.MaxValue;
            IDictionary<string, int> indices1 = new Dictionary<string, int>();
            IDictionary<string, int> indices2 = new Dictionary<string, int>();
            int length1 = list1.Length, length2 = list2.Length;
            for (int i = 0; i < length1; i++) {
                indices1.Add(list1[i], i);
            }
            for (int i = 0; i < length2; i++) {
                indices2.Add(list2[i], i);
                if (indices1.ContainsKey(list2[i])) {
                    minSum = Math.Min(minSum, indices1[list2[i]] + i);
                }
            }
            return indices1.Count <= indices2.Count ? FindMinSumstrings(minSum, indices1, indices2) : FindMinSumstrings(minSum, indices2, indices1);
        }

        public string[] FindMinSumstrings(int minSum, IDictionary<string, int> small, IDictionary<string, int> large) {
            IList<string> minSumstringsList = new List<string>();
            foreach (KeyValuePair<string, int> pair in small) {
                string key = pair.Key;
                if (large.ContainsKey(key)) {
                    int sum = pair.Value + large[key];
                    if (sum == minSum) {
                        minSumstringsList.Add(key);
                    }
                }
            }
            return minSumstringsList.ToArray();
        }
    }


