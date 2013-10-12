layout: post
title: '#UVa：272 – TEX Quotes'
date: 2011-11-25 00:21
comments: true
categories: [UVa]
tags: [UVa]
---
## 解法指引
照著題目要求，更換雙引號即可。

##程式碼(C++：0.016)
```C++ 272.cpp
/*******************************************************/
/* UVa 272 TEX Quotes                                  */
/* Author: LanyiKnight [at] knightzone.org             */
/* Version: 2011/11/24                                 */
/*******************************************************/
#include<iostream>
#include<cstdio>
using namespace std;
 
int main(){
  string s;
  bool leftorright = 0;
  while( getline( cin, s ) )
  {
    for( int i = 0 ; i < s.length() ; i++ )
      if( s[i] == '"' ){
        if( leftorright )
          printf( "''" );
        else
          printf( "``" );
        leftorright ^= 1;
      }
      else{
        printf( "%c", s[i] );
      }
    printf( "\n" );
  }
  return 0;
}
```