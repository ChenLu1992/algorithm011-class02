学习笔记

递归
	通过函数体进行循环
	
	模板
	recursion(level, param1, param2, ...){
     //递归终止条件（recorsion terminator）
     if level > MAX_LEVEL){
       process_result 

       return
     }
     //处理当前层逻辑（process logic in current level）
     process(level, param); 

     //下到下一层（drill down）
    recursion( level: level + 1, newParam); 

     //清理当前层（restore current status）,例如处理一些全局变量
   
	}
	思维要点
		不要人肉的进行递归
		找到最近重复子问题
		数学归纳法思维
		
	细分类
		分治
		回溯
			模板
			def divide_conquer(problem, param1, param2, ...): 
			  # recursion terminator 
			  if problem is None: 
				print_result 
				return 
			  # prepare data 
			  data = prepare_data(problem) 
			  subproblems = split_problem(problem, data) 
			  # conquer subproblems 
			  subresult1 = self.divide_conquer(subproblems[0], p1, ...) 
			  subresult2 = self.divide_conquer(subproblems[1], p1, ...) 
			  subresult3 = self.divide_conquer(subproblems[2], p1, ...) 
			  …
			  # process and generate the final result 
			  result = process_result(subresult1, subresult2, subresult3, …)
				
			  # revert the current level states
