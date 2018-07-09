一、算法

1、排序算法

（1）冒泡排序

void swap(int a[],int i,int j)
{
     int temp;
     temp = a[i];
     a[i] = a[j];
     a[j] = temp;
}

void bubbleSort(int a[],int n)
{
    for(int i=0;i<n-1;i++)
    {
	   for(int j=0;j<n-1-i;j++)
         {
		 if(a[j]>a[j+1])
              {    swap(a,j,j+1);  }
          }
     }
}

（2）选择排序
void selectionSort(int a[],int n)
{
      int min, i, j;
     
      for(i=0;i<n-1;i++)
      {
	     min=i;
           for(j=i+1;j<n;j++)
           {
		  if(a[j]<a[min])
               {    min=j;   }
           }
           if(min!=i)
           {   swap(a,min,i);  }
       }
}

（3）插入排序
void insertSort(int a[],int n)
{
     int temp, i, j;
     
     for(i=1;i<n;i++)
     {
	   temp = a[i];
          j=i-1;
          while(j>=0 && a[j]>temp)
          {
		  a[j+1] = a[j];
               j--;
           }
           a[j+1] = temp;
      }
}

（4）快速排序
int partion(int a[],int left,int right)
{
	int pivot = a[right];
       int tail=left-1;
       
      for(int i=left;i<right;i++)
      {
            if(a[i] <= pivot)
            {
		   swap(a,++tail,i);
            }
      }  
      swap(a,tail+1,right);
      return tail+1;
}

void quickSort(int a[],int left,int right)
{
       if(left>right)
       {   return;    }

	int p = partion(a,left,right)
       quickSort(a,left,p-1);
       quickSort(a,p+1,right);
}


int partition(int a[],int left,int right)
{
     int temp = a[left];
     int i=left+1;
     int j=right;
     while(i<j)
     {
	   while(a[j]>temp && j>i)
         {   j--;   }
         while(a[i]<temp && i<j)
         {   i++;  }
         swap(a,i,j);
     }
     swap(a,i,left);
     return i;
}

2、二分查找
int binarySearch(int a[],int n,int key)
{
     int l, h, med;
     l=0; 
     h=n-1;
     
     while(l<=h)
     {
          med = l + (h-l)/2;
          if(a[med] == key)
          {  return med;  }
          else if(a[med] >key)
          {  l= med + 1;   }
          else
          {  h = med - 1; th}
     }


return -1;
}

3、判断数组中是否有重复元素

public boolean containsDuplicate(int[] nums){
       Set<Integer> set = new HashSet<>();
       for(int num:nums){
            set.add(num);
       }
       return set.size() < nums.length;
}

4、java统计文章中单词出现的次数
统计一篇文章中单词出现的次数，要存储单词和次数，根据次数排序输出，要用Map数据结构保存键值对。首先想到是用TreeMap<String, Integer>，它为有序映射表，但默认按照键Key排序，要让Map按照Value值排序，难以直接实现，所以用先存储再排序的方法。先用HashMap<String, Integer>存储单词和单词的次数，利用Map的entrySet()方法获取映射关系视图，再由此构建ArrayList<Map.Entry<String, Integer>>，最后用Collections.sort()方法，自定义一个比较Integer的comparator，对该ArrayList排序。

impot java.util.*;

pubilic class WordCountTest{
       public static void main(String[] args){
          //读取
           Map<String,Integer> map = new HashMap<String,Integer>();
           Scanner in = new Scanner(System.in);
           
           while(in.hasNest()) 
           {
               String word = in.next();
               
               word = word.replace(',',' ').replace('.',' ').replace('\'',' ').replace('"',' ').replace('"',' ').replace(';',' ');
               if(!map.containsKey(word))
               {      map.put(word,1);      }
               else
               {      map.put(word,(map.get(word)+1));    }
           }
           
           //排序
           List<Map.Entry<String,Integer>> arrylist = new ArryList<Map>Entry<String,Integer>>(map.entrySet());
           Collections.sort(arryList, new Comparator<Map.Entry<String,Integer>>(){
                 public int compare(Map.Entry<String,Integer> obj1, Map.Entry<String,Integer> obj2)
                 {
                      return ((Integer) obj2.getValue()).compareTo((Integer) obj1.getValue());
                 }
           });
           
           	// 输出次数前20的单词
            List<Map.Entry<String,Integer>> list = arrylist. subList(0,20);
            System.out.println("出现频率前20的单词：");
            for(Map.Entry<String,Integer> item:list)
            {    System.out.println(item.getKey() +"="+item.getValue());   }
           
       }
}
     
5、Java——检索一段话中出现次数最多的英文单词

     String str = "Look to the skies above London and you'll see the usual suspects rainclouds, plane and pigeons. But by the end of the year, you might just see something else.";
     str = str.replace('\'',' ').replace(',',' ').replace('.',' ');
     
     String[] strings = str.split("\\s+"); // “\\s+”代表一个或多个空格，是正则表达式
     
     //用哈希表存储每个单词及其个数
     Map<String,Integer> map = new HashMap<String,Integer>();
     
     for(int i=0; i<strings.length; i++)
     {
         if(!map.contains(strings[i]))
	 {
	      map.put(strings[i],1);
	 }
	 else
	 {
	      map.put(strings[i],(map.get(strings[i])+1));
	 }
     }
     
     //构造一个包含“键值对”的List
     List<Map.Entry<String,Integer>> list = new ArryList<Map.Entry<String,Integer>>(map.entrySet());
     /*
      * 对List进行排序
      * 自己实现一个Comparator的匿名内部类，并实现compare方法
      * 使其根据出现的次数降序排列（因为我们需要的是出现最多的单词）
      */


Collections.sort(list,new Comparator<Map.Entry<String,Integer>>(){
            public int compare(Entry<String,Integer> obj1, Entry<String,Integer> obj2){
	           //降序排列
		   return obj2.getValue() - obj1.getValue(); 
	    }
       });
      
      //输出出现次数最多的前20个单词
      
      for(int i=0; i<20; i++)
      {
          System.out.println(list.get(i).getKey());
      }
   
6、找出两个链表的交点，要求：时间复杂度为 O(N)，空间复杂度为 O(1)
当访问 A 链表的指针访问到链表尾部时，令它从链表 B 的头部开始访问链表 B；同样地，当访问 B 链表的指针访问到链表尾部时，令它从链表 A 的头部开始访问链表 A。这样就能控制访问 A 和 B 两个链表的指针能同时访问到交点。


public ListNode getIntersectionNode(ListNode headA,ListNode headB)
{
      ListNode l1 =  headA, l2 = headB;
      
      while(l1!=l2)
      {
          l1 = (l1 == null) ? headB : l1.next;
	  l2 = (l2 == null) ? headA : l2.next;
      }
      return l1;
}

如果只是判断是否存在交点，那么就是另一个问题，即 编程之美：3.6 的问题。有两种解法：把第一个链表的结尾连接到第二个链表的开头，看第二个链表是否存在环；或者直接比较两个链表的最后一个节点是否相同。

7、二分查找
void int binarySearch(int[] a, int num)
{
      int left, right, mid;
      
      left = 0;
      right = a.length - 1;
      
      while(left<=right)
      {
          mid = left + (right - left)/2;
	  if(a[mid] == num)
	  {
	       return mid;
	  }
	  else if(a[mid] > num)
	  {
	       right = mid - 1;
	  }
	  else
	  {
	       left = mid + 1;
	  }
      }
      return -1;
}


8、链接：https://www.nowcoder.com/questionTerminal/5947ddcc17cb4f09909efa7342780048
来源：牛客网

Given a string, find the length of the longest substring without repeating characters. For example, the longest substring without repeating letters for "abcabcbb" is "abc", which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.

链接：https://www.nowcoder.com/questionTerminal/5947ddcc17cb4f09909efa7342780048
来源：牛客网

/*
    "滑动窗口" 
    比方说 abcabccc 当你右边扫描到abca的时候你得把第一个a删掉得到bca，
    然后"窗口"继续向右滑动，每当加到一个新char的时候，左边检查有无重复的char，
    然后如果没有重复的就正常添加，
    有重复的话就左边扔掉一部分（从最左到重复char这段扔掉），在这个过程中记录最大窗口长度
*/

import java.util.HashMap;

punblic class Solution{
    public int lengthOfLongestSubstring(String s){
         if(s == null || s.length() == 0)   return 0;
	 //新建一个map存储char
	 HashMap<Character,Integer> map = new HashMap<Character,Integer>();
	 int leftBound = 0;
	 int max = 0;
	 for(int i=0; i<s.length();i++){
	       char c = s.charAt(i);
	       //窗口左边可能为下一个char，或者不变
	       leftBound = Math.max(leftBound,(map.containsKey(c))? map.get(c)+1:0);
	       max = Math.max(max,i-leftBound+1);//当前窗口长度
	       map.put(c,i);     
	 }
	 return max;
    }
}

9、反转链表
（1）递归
public ListNode ReverseList(ListNode head)
{
    if(head == null || head.next == null)
    {   return head;   }
    ListNode next = head.next;
    head.next = null;
    ListNode newHead = ReverseList(next);
    next.next = head;
    return newHead;
}

(2)迭代
public ListNode ReverseList(ListNode head)
{
   ListNode newList = new ListNode(-1);
   while(head != null)
   {
        ListNode next = head.next;
	head.next = newList.next;
	newList.next = head;
	head = next;
   }
   return newList.next;
}
