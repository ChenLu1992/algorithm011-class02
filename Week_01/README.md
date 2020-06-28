学习笔记

      
数组        
  优点：
	访问元素快，随机访问某个节点时间复杂度O(1)
  缺点：
    大小固定：数组的大小是静态的（在使用前必须制定数组的大小）；
    分配一个连续空间块：数组初始分配空间时，有时候无法分配能存储整个数组的内存空间（当数组规模太大时）；
    基于位置的插入操作实现复杂：如果要在数组中的给定位置插入元素，那么可能就会需要移动存储在数组中的其他元素，
                            这样才能腾出指定的位置来放插入的新元素；而如果在数组的开始位置插入元素，那么这样的移动操作开销就会很大。
  各操作时间复杂度：
	lookup（随机访问某一个节点）O(1)
	delete（删除一个节点）O(n)
	insert（插入一个节点）O(n)
	append（在尾部增加一个节点）O(1)
	prepend(从头部增加一个节点) 注意：正常情况下数组的prepend操作是O(n)，
								   这里可以通过优化达到O(1)。方法是：申请稍大的内存，
                                   在数组前预留一部分空间，执行prepend时只把头节点前移即可。 
  
  解题常用操作
    暴力解法循环嵌套
		双层嵌套遍历数组：两数之和，ij不重复
          for(int i=0; i<numsize-1; ++i){
			 for(int j=i+1; j<numsize; ++j){
			 }
          }
        三层嵌套遍历数组：三数之和，ijk不重复
          for(int i=0; i<numsize-2; ++i){
			 for(int j=i+1; j<numsize-1; ++j){
				for(int k=j+1; k<numsize; ++k)
				
			 }
          }
    对有序数组：
		前后夹逼：
			int i=0;
			int j=numsize-1;
			while(i<j){
				if(nums[i]+nums[j] > target){
				j--;
				}
				else if(nums[i]+nums[j] < target){
					i++;
				}
			}
			
		快慢指针：删除排序数组中的重复项
			int i=0;
			for(j=1;j<numsize;j++){
				if(nums[i] != nums[j]){
					nums[++i]=nums[j];
				}
			}
	数组旋转：123->321
	    
		void reverse(int *nums, int start, int end)
		{
			int tmp;
			while(start < end){
				tmp = nums[start];
				nums[start++] = nums[end];
				nums[end--] = tmp;
			}
			
			return;
		}
		
			
			
			
		
    

链表
	优点
		能够在O(1)时间复杂度增加和删除节点
	缺点
		丧失了随机访问的能力，时间复杂度O(n)
	各操作时间复杂度
		prepend  O(1)
		append  O(1)
		insert  O(1)
		delete  O(1)
		lookup O(n)
	工程应用：
		LUR Cache
	


跳表
	目的：
		为了优化链表linked list搜索时间复杂度O(n)。对标平衡树AVL tree和二分查找
	前提条件：
		必须是元素有序的情况
	优点：
		搜索快于链表，时间复杂度均为O(logn)
		 原理简单，容易实现，方便扩展，效率更高。
	缺点：
		由于每次增加，删除都需要更新索引，
		所以时间复杂度从链表的O(1)，升为O(logn)
	各操作的时间复杂度：
		增加，删除，搜索的时间复杂度均是O(logn)
	工程应用：
		Redis
		LevelDB
		

栈(Stack)
	后进先出  LIFO（last in first out）
	时间复杂度
		push(插入) O(1)
		pop(取出) O(1)
		查寻 O(n)  原因：无序的
		


队列(Queue)
	双端队列（Double-End Queue）
		先入先出 FIFO
		时间复杂度
			插入 O(1)
			取出 O(1)
			查寻 O(n) 原因：无序的
		操作
			addFirst
			removeFirst
			addEnd
			removeEnd
			peekFirst
			peekEnd
		

	优先队列(Priority Queue)
		不是先入先出，按元素的优先级取出
		时间复杂度
			插入 O(1)
			取出O(logn)
		底层实现使用的数据结构复杂多样:
			heep
				二叉树堆
				斐波那契堆
			bst（binary search tree） 二叉搜索树
			平衡二叉搜索树
				红黑树
				AVL
			treap
		
