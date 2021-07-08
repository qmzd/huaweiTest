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
