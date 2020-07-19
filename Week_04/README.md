学习笔记

	深度优先搜索Depth first search
		递归实现模板
			//C/C++
			//递归写法：
			map<int, int> visited;

			void dfs(Node* root) {
			  // terminator
			  if (!root) return ;

			  if (visited.count(root->val)) {
				// already visited
				return ;
			  }

			  visited[root->val] = 1;

			  // process current node here. 
			  // ...
			  for (int i = 0; i < root->children.size(); ++i) {
				dfs(root->children[i]);
			  }
			  return ;
			}
		
		栈实现模板
			//C/C++
			//非递归写法：
			void dfs(Node* root) {
			  map<int, int> visited;
			  if(!root) return ;

			  stack<Node*> stackNode;
			  stackNode.push(root);

			  while (!stackNode.empty()) {
				Node* node = stackNode.top();
				stackNode.pop();
				if (visited.count(node->val)) continue;
				visited[node->val] = 1;


				for (int i = node->children.size() - 1; i >= 0; --i) {
					stackNode.push(node->children[i]);
				}
			  }

			  return ;
			}
		
	
	
	广度优先搜索Breadth first search	
		队列实现模板
			// C/C++
			void bfs(Node* root) {
			  map<int, int> visited;
			  if(!root) return ;

			  queue<Node*> queueNode;
			  queueNode.push(root);

			  while (!queueNode.empty()) {
				Node* node = queueNode.top();
				queueNode.pop();
				if (visited.count(node->val)) continue;
				visited[node->val] = 1;

				for (int i = 0; i < node->children.size(); ++i) {
					queueNode.push(node->children[i]);
				}
			  }

			  return ;
			}
		

	启发式搜素（优先级优先搜素） --深度学习算法
	
	
	贪心算法Greedy
		在每一步选择中都采取当前状态下最好或最优的选择，
		从而希望导致全局结果最好或最优的算法
		
		与动态规划的区别：
			与动态规划的区别：
				贪心算法堆每个子问题的方案都作出选择，不能回退。
				动态规划则会保存以前的运算结果，并根据以前的结果对当前进行选择，有回退功能。
	
	
	二分查找Binary search
		前提条件：
			1、目标函数单调性（单调递增或递减）--有序
			2、存在上下界
			3、能够通过索引访问
			
		代码模板
		int binarySearch(const vector<int>& nums, int target) {
			int left = 0, right = (int)nums.size()-1;
			
			while (left <= right) {
				int mid = left + (right - left)/ 2;
				if (nums[mid] == target) return mid;
				else if (nums[mid] < target) left = mid + 1;
				else right = mid - 1;
			}
			
			return -1;
		}
