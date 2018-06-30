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
