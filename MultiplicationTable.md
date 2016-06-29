
```c


//用C语言实现乘法口诀表的关键在于如何控制数据输出的格式，这一点在于对嵌套for循环
//的深入理解。首先，外循环赋值一次，内循环执行一遍；对于乘法口诀表这个程序来说，
//外层循环为1，内层循环也为1时，打印一行一列；外层循环为1，内层循环为2时，打印一
//行两列......以此类推。然后为了美观起见，在打印时按“ %-4d”的格式打印，“ -”号代表
//左对齐，“ 4d”代表输出的整形数据至少占4位，其实在这儿最多占两位，剩下的两位用空
//格填充。


# include <stdio.h>

int main()
{
	 int i,j;

	 for(i=1; i <= 9; i++)
	 {

		 for(j=1; j <= i; j++)
		 {
			 printf("%d*%d = %-4d", j, i, i*j);    //结果四位有效数字，左对齐		
		 }                                      
		    
		 printf("\n");
						  
	 }
		 
	 return 0;	  
}


```