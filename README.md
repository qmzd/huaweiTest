# huaweiTest
OD机试算法题

01 /*计算字符串最后一个单词的长度，单词以空格隔开，字符串长度小于5000。*/
import java.util.Scanner;

/**
 * @author Mr_zhao - 过河卒
 * @create 2021/7/4 14:33
 * @day 星期日
 */
    public class StringLength {

        /*计算字符串最后一个单词的长度，单词以空格隔开，字符串长度小于5000。*/

        public static void main(String[] args) {
            int  s = result02();
            System.out.println(s);
        }

        private static int result02(){
            Scanner scanner = new Scanner(System.in);
            String s = scanner.nextLine();
            String[] split = s.split("\\ ");
            int length = split.length;
            String s1 = split[length - 1];
            int i = s1.length();
            return i;
        }
    }

02  写出一个程序，接受一个由字母、数字和空格组成的字符串，和一个字母，
    然后输出输入字符串中该字母的出现次数。不区分大小写，字符串长度小于500。
    
    import java.util.Scanner;
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        String str1 = scan.nextLine();
        String str2 = scan.nextLine();
        String s1 = str1.toLowerCase();
        String s2 = str2.toLowerCase();
        
         if (str1.length()>=500 || str2.length() >=500){
            throw new Exception("str length too long");
        }

        Character c = s2.charAt(0);
        int count = 0;
        for (int i = 0; i < s1.length(); i++) {
            if (c==(s1.charAt(i))){
                count ++ ;
            }
        }
        System.out.println(count);
    }
  

03 明明想在学校中请一些同学一起做一项问卷调查，为了实验的客观性，他先用计算机生成了N个1到1000之间的随机整数（N≤1000），对于其中重复的数字，只保留一个，把其余相同的数去掉，不同的数对应着不同的学生的学号。然后再把这些数从小到大排序，按照排好的顺序去找同学做调查。请你协助明明完成“去重”与“排序”的工作(同一个测试用例里可能会有多组数据(用于不同的调查)，希望大家能正确处理)。


注：测试用例保证输入参数的正确性，答题者无需验证。测试用例不止一组。

当没有新的输入时，说明输入结束。

输入描述：
注意：输入可能有多组数据(用于不同的调查)。每组数据都包括多行，第一行先输入随机整数的个数N，接下来的N行再输入相应个数的整数。具体格式请看下面的"示例"。

输出描述：
返回多行，处理后的结果
输入：
3
2
2
1
11
10
20
40
32
67
40
20
89
300
400
15
输出：

1
2
10
15
20
32
40
67
89
300
400

    import java.util.Scanner;
    import java.util.Set;
    import java.util.TreeSet;

    public class Main{
        public static void main(String[] args){
            Scanner scan = new Scanner(System.in);
            while(scan.hasNext()){
                int size = scan.nextInt();
                Set<Integer> tree = new TreeSet<>();
                for(int i = 0; i < size ; i++){
                    tree.add(scan.nextInt());
                }
                for(Integer num : tree){
                    System.out.println(num);
                }
            }


        }
    }
                                                 
04 /*无重复字符的最长子串
        * 给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。
        * 输入: s = "abcabcbb", 输入："BBBBBBB"
          输出: 3,              输出：1  
          解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
        * */
        
        private static void lengthOfLongestSubstring(){
        Scanner scan = new Scanner(System.in);
            String longStr = scan.nextLine();
            int length = longStr.length();
            int maxLength = 0;
            int startIndex = 0;
            HashMap<Character, Integer> map = new HashMap<>();
            for (int i = 0; i < length; i++) {
                char ch = longStr.charAt(i);
                if (map.containsKey(ch)){
                    startIndex = Math.max(map.get(ch) + 1,startIndex);
                }
                maxLength = Math.max(maxLength,i - startIndex + 1);
                map.put(ch,i);
            }
            System.out.println(maxLength);
        }
        
        
 最长回文串：
      
            // 回文串
                public static String longestPalindrome(String s) {
                    if (s == null || s.length() < 1) {
                        return "";
                    }
                    int start = 0, end = 0;
                    for (int i = 0; i < s.length(); i++) {
                        // 奇数中点
                        // 以i作为回文子串的中心，向两边扩散得到的回文子串的长度
                        int oddPoint = expandAroundCenter(s, i, i);
                        // 偶数中点
                        // 以i 和 i+1作为回文子串的中心，向两边扩散得到的回文子串的长度
                        int evenPoint = expandAroundCenter(s, i, i + 1);
                        // 回文串的最大长度
                        int len = Math.max(oddPoint, evenPoint);

                        // 计算回文串的起止索引
                            // 根据i和maxLen算begin下标
                                       // 奇数：i-maxLen/2
                                       // 偶数：i-maxLen/2+1
                        // 统一：i-(maxLen-1)/2
                        if (len > end - start) {
                            start = i - (len - 1) / 2;
                            end = start + len - 1;
                        }
                    }
                    // end+1 是因为java的左闭右开的原则；
                    return s.substring(start, end + 1);
                }
      
      
               /**
             * 返回回文子串的长度
             * @param s 字符串
             * @param left 左边界
             * @param right 右边界
             * @return 回文串的长度
             */
            public static int expandAroundCenter(String s, int left, int right) {
                // 由中间向两边扩散的判断，若相等则左下标向左一位，右下标向右一位；
                while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
                    --left;
                    ++right;
                }
                // 回文串的长度为:
                return right - left - 1;
            }
      
                                                              
 05.  连续输入字符串，请按长度为8拆分每个字符串后输出到新的字符串数组；
        •长度不是8整数倍的字符串请在后面补数字0，空字符串不处理。*/
  
  
        public static void main(String[] args) {
                Scanner scanner = new Scanner(System.in);
                while (scanner.hasNext()){
                    String str = scanner.nextLine();
                    StringBuffer buffer = new StringBuffer();
                    buffer.append(str);
                    int length = str.length();
                    int addZero = 8 - length % 8;
                    while (addZero > 0 && addZero < 8){
                        buffer.append(0);
                        addZero--;
                    }
                    String s = buffer.toString();
                    while (s.length() > 0){
                        System.out.println(s.substring(0,8));
                         s = s.substring(8);
                    }
                }
            }


06. 给你一个 32 位的有符号整数 x ，返回将 x 中的数字部分反转后的结果。
    如果反转后整数超过 32 位的有符号整数的范围 [−231,  231 − 1] ，就返回 0。
    输入：x = 123 ； -123 ；  120 
    输出：321     ； -321 ；  21

     private static int reverse(int x){
        int rev = 0;
        while (x != 0) {
            if (rev < Integer.MIN_VALUE / 10 || rev > Integer.MAX_VALUE / 10) {
                return 0;
            }
            int digit = x % 10;
            x /= 10;
            rev = rev * 10 + digit;
        }
        return rev;
    }
                                                              
07.给你一个整数 x ，如果 x 是一个回文整数，返回 true ；否则，返回 false 。

回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。例如，121 是回文，而 123 不是。 -121 不是；

     // 是否为回文数
    private static boolean isPalindrome(int x){
        if(x < 0) {
            return false;
        }
        int tag = x;

        int vec = 0;
        while (x != 0){
            int dail = x % 10;
            x /= 10;
            vec = vec * 10 + dail;
        }
        if (vec == tag){
            return true;
        }
        return false;
    }
    
8.0 /* 给定一个罗马数字，转为整数，范围在 1 - 3399
     * 罗马数字包含以下七种字符: I， V， X， L，C，D 和 M
     * 通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，
     * 例如 4 不写做IIII，而是IV。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。
     * 同样地，数字 9 表示为IX。这个特殊的规则只适用于以下六种情况：
     * I可以放在V(5) 和X(10) 的左边，来表示 4 和 9。
       X可以放在L(50) 和C(100) 的左边，来表示 40 和90。
       C可以放在D(500) 和M(1000) 的左边，来表示400 和900。
     *  XXVII = 27
     * */
     
        解题思路：若左边的值大于右边则结果值 = 从左到右连续相加；
             若左边的值小于右边的值则将左边的值取反后。从左右到连续相加；
    
        private static int romanToInt(String s) {
            HashMap<Character, Integer> map = new HashMap<Character, Integer>() {
                {
                    put('I', 1);
                    put('V', 5);
                    put('X', 10);
                    put('L', 50);
                    put('C', 100);
                    put('D', 500);
                    put('M', 1000);
                }
            };
            int length = s.length();
            int sum = 0;
            for (int i = 0; i < length; i++) {
                // 当前罗马数字代表的数；
                Integer code = map.get(s.charAt(i));
                if (i < length-1 && code < map.get(s.charAt(i+1))){
                    sum -= code;
                }else {
                    sum += code;
                }
            }
            return sum;
        }
    
9.0 /* 数字转罗马数字；
    解题思路：罗马数字总共是7个字符，再加上特殊情况的6个字符总共是13个字符；
            所以，转换时只需每次从左向右取最大罗马字符拼接即可；*/
            
        private static String intToRoman(int number) {
            int[] values = {1000,900,500,400,100,90,50,40,10,9,5,4,1};
            String[] ramoFormat = {"M","CM","D","DM","C","XC","L","XL","X","IX","V","IV","I"};

            StringBuffer roman = new StringBuffer();
            int length = values.length;
            for (int i = 0; i < length; i++) {
                int value = values[i];
                while (number >= value){
                    number -= value;
                    roman.append(ramoFormat[i]);

                }
                if (number == 0){
                    break;
                }
            }
            return roman.toString();
        }
        
10.  /* 编写一个函数来查找字符串数组中的最长公共前缀。
    如果不存在公共前缀，返回空字符串 ""。*/

  // 横向扫描
  
        private static String getLongestPrefix(String[] args) {
            int length = args.length;
            String strOne = args[0];
            for (int i = 1; i < length; i++) {
                strOne = longestCommonPrefix(strOne, args[i]);
                if (strOne.length() == 0){
                    return "";
                }
            }
            return strOne;
        }

        private static String longestCommonPrefix(String strOne, String arg) {
            int size = Math.min(strOne.length(), arg.length());
            int index = 0;
            while (index < size && arg.charAt(index) == strOne.charAt(index)) {
                index++;
            }
            return strOne.substring(0,index);
        }

   // 纵向扫描
   
        private static String getLongestCommonPrefix(String[] args){
            String arg = args[0];
            int length = arg.length();
            int count = args.length;
            for (int i = 0; i < length; i++) {
                char ch = arg.charAt(i);
                for (int j = 1; j < count; j++) {
                    if (i == args[j].length() || args[j].charAt(i) != ch){
                        return arg.substring(0,i);
                    }
                }
            }
           return "";
        }        
11.0  // 给你一个包含 n 个整数的数组nums，判断nums中是否存在三个元素 a，b，c ，使得a + b + c = 0
    // 请你找出所有和为 0 且不重复的三元组。 
    
   解题思路： 排序+双指针
    
        private static List<List<Integer>> threeNum(int[] nums){
             int length = nums.length;
        Arrays.sort(nums);
        List<List<Integer>> arrayList = new ArrayList<>();
        // 判断特殊情况
        if (nums == null || length == 0 || length < 3) {
            return arrayList;
        }

        // 开始用双指针的思想
        // 开始遍历数组（因为是三数之和，除了双指针我们还需要一个指针）
        for (int i = 0; i < length - 2; i++) {
            // 重复的情况我们会先舍去
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }

            // 初始化双指针
            int left = i + 1;
            int right = length - 1;
            while (left < right) {
                if (nums[left] + nums[i] + nums[right] < 0) {
                    left++;
                } else if (nums[left] + nums[i] + nums[right] > 0) {
                    right--;
                } else {
                    // 用一个list记录每次循环找到的答案
                    List<Integer> list = new ArrayList<>();
                    list.add(nums[i]);
                    list.add(nums[left]);
                    list.add(nums[right]);
                    arrayList.add(list);
                    // 还不能跳出循环，后面可能还有不同的组合
                    //为了避免重复还是需要判断左指针后一位是否和左指针重复
                    //判断右指针前一位是否和右指针重复
                    while (left < right && nums[left] == nums[left + 1]) {
                        left++;
                    }
                    while (left < right && nums[right] == nums[right - 1]) {
                        right--;
                    }
                    // 去寻找后续的不同组合
                    left++;
                    right--;
                }
            }
        }
        return arrayList;
        }
        
12.给定一个只包括 '('，')'，'{'，'}'，'[',']' 的字符串 s ，判断字符串是否有效。
    有效字符串需满足：
    1.左括号必须用相同类型的右括号闭合。
    2.左括号必须以正确的顺序闭合。
    
        private static boolean isValid(String s){
            int length = s.length();
            HashMap<Character, Character> map = new HashMap<>();
            map.put(')','(');
            map.put(']','[');
            map.put('}','{');

            Deque<Character> stack = new LinkedList<>();
            for (int i = 0; i < length; i++) {
                char ch = s.charAt(i);
                if (map.containsKey(ch)){
                    if (stack.isEmpty() ||map.get(ch) != stack.peek()){
                     return false;
                    }
                    stack.pop();
                }else {
                    stack.push(ch);
                }
            }
            return stack.isEmpty();
        }
13. /**
     * 最接近的三个数之和；
     * 给定一个包括n 个整数的数组nums和 一个目标值target。
     * 找出nums中的三个整数，使得它们的和与target最接近。返回这三个数的和。
     * 假定每组输入只存在唯一答案。
     *
     * 解题思路： 排序+双指针
     * @return int
     */
     
     
            private static int threeSumClosest(int[] nums, int target){
                int length = nums.length;
                Arrays.sort(nums);

                if (nums == null || length == 0 || length < 3){
                    return 100000;
                }

                int min = Integer.MAX_VALUE;
                int res = 0;

                for (int i = 0; i < length - 2; i++) {
                    // 跳过重复的数
                    if (i > 0 && nums[i] == nums[i+1]){
                        continue;
                    }
                    // 定义双指针
                    int left = i+1;
                    int right = length - 1;

                    while (left < right){
                       int sum =  nums[i]+nums[left]+nums[right];
                        if (sum == target){
                            return target;
                        }

                        int abs = Math.abs(sum - target);
                        if (abs < min){
                            min = abs;
                            res = sum;
                        }

                        if (sum > target){
                            right--;
                        }else {
                            left++;
                        }
                    }
                }
                return res;
            }
            
14. /**
     * 四数之和
     *给定一个包含n 个整数的数组nums和一个目标值target，
     * 判断nums中是否存在四个元素 a，b，c和 d，
     * 使得a + b + c + d的值与target相等？找出所有满足条件且不重复的四元组。
     *
     * 解题思路：排序 + 双指针；
     * @param nums 任意数组
     * @param target 目标值
     * @return 和为目标值的集合
     */
     
     
            private static List<List<Integer>> fourSum(int[] nums, int target){
                List<List<Integer>> result = new ArrayList<>();
                int length = nums.length;
                if (nums == null || length < 4){
                    return result;
                }
                // 排序
                Arrays.sort(nums);
                for (int i = 0; i < length - 3; i++) {
                    if (i > 0 && nums[i] == nums[ i - 1]){
                        continue;
                    }
                    // 排序后数组的最小的前四个数之和都大于目标数，所以无论后面加哪个都会大于目标数，所以直接跳出，
                    if (nums[i] + nums[i + 1] + nums[i + 2] + nums[i + 3] > target){
                        break;
                    }
                    // 排序后数组的最大的后三个数之和小于目标数，则无需再计算，直接进行下次循环；
                    if (nums[i] + nums[length - 3] + nums[length - 2] + nums[length - 1] < target){
                        continue;
                    }

                    for (int j = i+1; j < length - 2; j++) {

                        if (j > i+1 && nums[j] == nums[j - 1]){
                            continue;
                        }
                        if (nums[i] + nums[j] + nums[j+1] + nums[j + 2] > target){
                            break;
                        }
                        if (nums[i] + nums[j] + nums[length - 2] + nums[length - 1] < target){
                            continue;
                        }

                        // 定义双指针
                        int left = j + 1;
                        int right = length - 1;
                        while (left < right){
                            if (nums[i] + nums[j] + nums[left] + nums[right] < target){
                                left++;
                            }else if (nums[i] + nums[j] + nums[left] + nums[right] > target){
                                right--;
                            }else {
                                List<Integer> list = new ArrayList<>();
                                list.add(nums[i]);
                                list.add(nums[j]);
                                list.add(nums[left]);
                                list.add(nums[right]);
                                result.add(list);
                                while (left < right && nums[left] == nums[left+1]){
                                    left++;
                                }
                                while (left < right && nums[right] == nums[right-1]){
                                    right--;
                                }
                                left++;
                                right--;
                            }
                        }
                    }
                }
                return result;
            }
15 生成有效括号的组合
    数字 n 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 有效的 括号组合。
  * 有效括号组合需满足：左括号必须以正确的顺序闭合。
  * 思路：递归
  
          private static List<String> generateParenthesis(int n){
                List<String> res = new ArrayList<>();
                if (n <= 0){
                    return res;
                }
                getParenthesis("",n,n,res);
                return res;
            }

         /**
         * 获取括号
         *
         * @param str 括号
         * @param left 左括号个数
         * @param right 右括号个数
         * @param res 结果集
         */
        private static void getParenthesis(String str, int left, int right,List<String> res) {
            // 先写出递归的结束条件
           if (left == 0 && right == 0){
               res.add(str);
               return;
           }
           // 若左右两个括号的数目相等，则先获取左括号；
            if (left == right){
                getParenthesis(str+"(",left-1,right,res);
            }else if (left < right){
                // 若左括号小于右括号的话则即可先获取左括号，也可先获取右括号
                if (left > 0){
                    // 继续先获取左括号
                    getParenthesis(str+"(",left-1,right,res);
                }
                getParenthesis(str+")",left,right-1,res);
            }
        }
16 功能描述 原地删除有序数组中的重复项
 *给你一个有序数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。
 * 不要使用额外的数组空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。


        public static void main(String[] args) {
                int[] nums = {1, 1, 2,2,3,4,5,5,6};
                int i = removeDuplicates(nums);
                System.out.println(Arrays.toString(nums));
                System.out.println(i);
            }
 
         private static int removeDuplicates(int[] nums){
                int n = nums.length;
                if (n == 0) {
                    return 0;
                }

                // 快指针扫描，满指针标记覆盖位置 
                int fast = 1, slow = 1;
                while (fast < n) {
                    if (nums[fast] != nums[fast - 1]) {
                        nums[slow] = nums[fast];
                        ++slow;
                    }
                    ++fast;
                }
                return slow;
            }
            
17  功能描述 移除元素
 * 给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度
 *（元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。）     
 
        public static void main(String[] args) {
            int[] nums = {0,1,2,2,3,0,4,2};
            int i = removeElement(nums,2);
            System.out.println(Arrays.toString(nums));
            System.out.println(i);
        }


        private static int removeElement(int[] nums, int val){
            int length = nums.length;
            if (length == 0){
                return 0;
            }

            int fast = 0;
            int slow = 0;
            while (fast < length){
                if (nums[fast] != val){
                    nums[slow] = nums[fast];
                    ++slow;
                }
                ++fast;
            }
            return slow;
        }
18  * 功能描述
 * 给定两个整数，被除数dividend和除数divisor。将两数相除，要求不使用乘法、除法和 mod 运算符。
 * 返回被除数dividend除以除数divisor得到的商。

           /**
             * 除法
             *
             * @param devidend 被除数
             * @param devisor 除数
             * @return 结果
             */
            private static int devide(int devidend, int devisor){

                if (devisor == 0){
                    return devidend;
                }

                if (devidend == Integer.MIN_VALUE && devisor == -1){
                    return Integer.MAX_VALUE;
                }
                int res = 0;
                int devidend2 = Math.abs(devidend);
                int devisor2 = Math.abs(devisor);
                res = call(devidend2, devisor2, res);
                if ((devidend < 0 && devisor > 0) || (devidend > 0 && devisor < 0)){
                    res = -res;
                }
                return res;
            }

            private static int call(int devidend, int devisor,int res){
                while (devidend - devisor > 0){
                    devidend  -= devisor;
                    res++;
                }
                return res;
            }
19  * 功能描述: 获取下一个更大的排列
 *
 * 实现获取 下一个排列 的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列（即，组合出下一个更大的整数）。
 * 如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。
 * 必须 原地 修改，只允许使用额外常数空间。

 * 思路及解法
 * 注意到下一个排列总是比当前排列要大，除非该排列已经是最大的排列。我们希望找到一种方法，能够找到一个大于当前序列的新序列，且变大的幅度尽可能小。具体地：
 * 我们需要将一个左边的「较小数」与一个右边的「较大数」交换，以能够让当前排列变大，从而得到下一个排列。
 * 同时我们要让这个「较小数」尽量靠右，而「较大数」尽可能小。当交换完成后，「较大数」右边的数需要按照升序重新排列。这样可以在保证新排列大于原来排列的情况下，使变大的幅度尽可能小。
 *
 * [4,5,2,6,3,1] 为例； 左边的较小数是：2，右边的较大数是：3 ；满足「较小数」尽量靠右，而「较大数」尽可能小。
 * 当我们完成交换后排列变为 [4,5,3,6,2,1]，此时我们可以重排「较小数」右边的序列，序列变为 [4,5,3,1,2,6]。

        public static void main(String[] args) {
                int[] nums = {4,5,2,6,3,7,4,1};
                int[] ints = nextPermutation(nums);
                System.out.println(Arrays.toString(ints));
            }

            private static int[] nextPermutation(int[] nums) {
                int i = nums.length - 2;
                // 1.从后向前查找第一个顺序对（i,i+1）,满足nums[i] < nums[i+1],这样“较小数”为nums[i],此时[i+1,n]必然是降序的
                while (i >= 0 && nums[i] >= nums[i + 1]) {
                    i--;
                }
                // 2.若找到顺序队，那么在区间[i+1,n)中从后向前查找第一个元素j满足a[i] < a[j].这样“较大数”即为：a[j];
                if(i >= 0){
                    int j = nums.length - 1;
                    while (j>=0 && nums[i] >= nums[j]){
                        j--;
                    }
                    // 3.交换nums[i] 和 nums[j]的值，此时[i+1,n)比为降序，我们通过双指针将其转为升序即可；
                    swap(nums,i,j);
                }
                reverse(nums,i+1);
                return nums;
            }

            /**
             * 交换
             *
             * @param nums 数组
             * @param i 索引位置
             * @param j 索引位置
             */
            private static void swap(int[] nums, int i , int j){
                int temp = nums[i];
                nums[i] = nums[j];
                nums[j] = temp;
            }

            /**
             * 位置反转
             *
             * @param nums 数组
             * @param start 开始位置
             */
            private static void reverse(int[] nums, int start){
                int left = start;
                int right = nums.length - 1;
                while (left < right){
                    swap(nums,left,right);
                    left++;
                    right--;
                }
            }
20 功能描述 实现strStr()
 * 给你两个字符串haystack 和 needle ，请你在 haystack 字符串中找出 needle 字符串出现的第一个位置（下标从 0 开始）。如果不存在，则返回 -1
 *当needle是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。
 * 对于本题而言，当needle是空字符串时我们应当返回 0 。这与 C 语言的strstr()以及 Java 的indexOf()定义相符。
 
          public static void main(String[] args) {
                String haystack = "";
                String needle = "";
                int i = strStr(haystack, needle);
                System.out.println(i);
            }

            private static int strStr(String haystack,String needle){
                int longLen = haystack.length();
                int shortLen = needle.length();

                if (longLen < shortLen){
                    return -1;
                }
                if (longLen == 0 || shortLen == 0){
                    return 0;
                }
                for (int i = 0; i < shortLen; i++) {
                    for (int j = 0; j < longLen - shortLen; j++) {
                        if (needle.charAt(i) != haystack.charAt(j)) {
                            continue;
                        }
                        if (haystack.substring(j,j+shortLen).equals(needle)){
                            return j;
                        }
                    }
                }

                return -1;
            }
21 功能描述 给你一个只包含 '(' 和 ')' 的字符串，找出最长有效（格式正确且连续）括号子串的长度。
 * 输入：s = "(()"
 * 输出：2
 * 解释：最长有效括号子串是 "()"
 *
 * 输入：s = ")()())"
 * 输出：4
 * 解释：最长有效括号子串是 "()()"

 * 输入：s = ""
 * 输出：0

        private static int longestValidParentheses(String str){
                int length = str.length();
                if (length == 0){
                    return 0;
                }
                int res = 0;
                Deque<String> stack = new LinkedList<>();
                for (int i = 0; i < length; i++) {
                    if (str.charAt(i) == '('){
                        stack.push("(");
                    }else if(!stack.isEmpty() && str.charAt(i) == ')'){
                        stack.pop();
                        res += 2;
                    }
                }
                return res;

            }
