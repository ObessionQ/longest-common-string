# longest-common-string
动态规划法求解最长公共子序列
#include <iostream>
#include <string.h>
using namespace std;

void LCSLength(char *s1,char *s2,int m,int n,int c[][100],int s[][100])
{
	int i,j;
	for(i=0;i<=m;i++)
	{c[i][0]=0;s[i][0]=0;}
	for(i=0;i<=n;i++)
	{c[0][i]=0;s[0][i]=0;}
	for(i=1;i<=m;i++)
	{
		for(j=1;j<=n;j++)
		{
			if(s1[i-1]==s2[j-1])
			{
				c[i][j]=c[i-1][j-1]+1;s[i][j]=1; 	
			}
			else if(c[i-1][j]>=c[i][j-1])
			{
				c[i][j]=c[i-1][j];s[i][j]=2;		
			}
			else
			{
				c[i][j]=c[i][j-1];s[i][j]=3;
			}
		}
	}
}

void CLCS(int m,int n,int s[][100],char *s1)
{
	if(m==0||n==0) return;
	if(s[m][n]==1)
	{
		CLCS(m-1,n-1,s,s1);
	}
	else if(s[m][n]==2)
		CLCS(m-1,n,s,s1);
	else
		CLCS(m,n-1,s,s1);
}

void print(int m,int n,int c[][100],int s[][100])
{
	int i,j;
	for(i=0;i<=m;i++)
	{
		for(j=0;j<=n;j++)
		{
			cout<<c[i][j]<<" ";
		}
		cout<<endl;
	}
	cout<<endl;
	for(i=0;i<=m;i++)
	{
		for(j=0;j<=n;j++)
		{
			cout<<s[i][j]<<" ";
		}
		cout<<endl;
	}
}

int main()
{
	int c[100][100],s[100][100];
	char s1[100],s2[100];
	int m,n;
	m=strlen(gets(s1));
	n=strlen(gets(s2));
	LCSLength(s1,s2,m,n,c,s);
	cout<<c[m][n]<<endl;
	print(m,n,c,s);
	cout<<endl;
	CLCS(m,n,s,s1);
	cout<<endl;
	return 0;
}
