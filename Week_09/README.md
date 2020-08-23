学习笔记


爬楼梯

int dp[n];
dp[0]=1;
dp[1]=2;

for(int i=2;i<n;++i){
	dp[i]=dp[i-1]+dp[i-2];
}

return dp[n-1];

爬楼梯进阶1：如果一次能上1 2 3三种
int dp[n];
dp[0]=1;
dp[1]=2;
dp[2]=3;

for(int i=3;i<n;++i){
	dp[i]=dp[i-1]+dp[i-2]+dp[i-3];
}

return dp[n-1];

爬楼梯进阶2：给一个步数的数组x[m]，里面是可以走的步数

for(int i=3;i<n;++i){
	for(int j=0;j<m;j++){
		dp[i] +=dp[i-x[j]];
	}
}

return dp[n-1];


爬楼梯进阶3：给一个步数的数组x[m]，里面是可以走的步数,且不能走相同的步数
dp[n][k] k表示上次使用的步数


不同路径二
int uniquePathsWithObstacles(int** obstacleGrid, int obstacleGridSize, int* obstacleGridColSize){
    int m=obstacleGridSize;
    int n=obstacleGridColSize[0];

    int dp[m][n];
    for(int i=0;i<m;i++){
        if(obstacleGrid[i][0]==1 || (i>0 && dp[i-1][0]==0)){
            dp[i][0]=0;
        }
        else{
            dp[i][0]=1;
        }
    }

    for(int j=0;j<n;j++){
        if(obstacleGrid[0][j]==1 || (j>0 && dp[0][j-1]==0)){
            dp[0][j]=0;
        }
        else{
            dp[0][j]=1;
        }
    }

    for(int i=1;i<m;i++){
        for(int j=1;j<n;j++){
            if(obstacleGrid[i][j]==1){
                dp[i][j]=0;
            }
            else{
                dp[i][j]=dp[i-1][j]+dp[i][j-1];
            }
        }
    }

    return dp[m-1][n-1];
}



字符串
atoi转换
int myAtoi(string str) {
   int res = 0;
   int sign = 1;
   size_t index = 0;
   if(str.find_first_not_of(' ') != string::npos) 
       index = str.find_first_not_of(' ');
   if(str[index] == '+' || str[index] == '-')
       sign = str[index] == '-' ? -1 : 1;
    
    while(index < str.size() && isdigit(str[index])) {
        res = res * 10 + (str[index++] - '0');
        if(res*sign > INT_MAX) return INT_MAX;
        if(res*sign < INT_MIN) return INT_MIN; 
    }

   return res*sign;
}

字符串暴力匹配

int forceSearch(string text, string pattern) {
    int len_txt = text.length();
    int len_pat = pattern.length();

    for (int i = 0; i <= len_txt - len_pat; i++) {
        int j = 0;
        for (j = 0; j < len_pat; j++) {
            if (text[i + j] != pattern[j]) break;
        }
        if (j == len_pat) {
            return i;
        }
    }
    return -1;
}



字符串匹配 Rabin-Karp算法 代码
const int D = 256;
const int Q = 9997;

int RabinKarpSerach(string txt, string pat) {
    int M = pat.length();
    int N = txt.length();
    int i, j;
    int patHash = 0, txtHash = 0;

    for (i = 0; i < M; i++) {
        patHash = (D * patHash + pat[i]) % Q;
        txtHash = (D * txtHash + txt[i]) % Q;
    }
    int highestPow = 1;  // pow(256, M-1)
    for (i = 0; i < M - 1; i++) 
        highestPow = (highestPow * D) % Q;

    for (i = 0; i <= N - M; i++) { // 枚举起点
        if (patHash == txtHash) {
            for (j = 0; j < M; j++) {
                if (txt[i + j] != pat[j])
                    break;
            }
            if (j == M)
                return i;
        }
        if (i < N - M) {
            txtHash = (D * (txtHash - txt[i] * highestPow) + txt[i + M]) % Q;
            if (txtHash < 0)
                txtHash += Q;
        }
    }

    return -1;
}
