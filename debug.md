https://gcc.gnu.org/onlinedocs/cpp/Variadic-Macros.html


#include <stdio.h>
#include <string.h>

#define __func__ __FUNCTION__
#define __FILENAME__ (strrchr(__FILE__, '/') ? strrchr(__FILE__, '/') + 1 : __FILE__)
#define PI (3.142)
#define p1( fmt, ...) printf("[%s]%s(%d) :" fmt"\n", __FILENAME__, __func__,__LINE__, ## __VA_ARGS__)
#define p1( fmt, ...) printf("[%s]%s(%d) :" fmt"\n", __FILENAME__, __func__,__LINE__, ## __VA_ARGS__)
#define p1_enter( fmt, ...) printf("[%s]%s(%d) ENTER:" fmt"\n", __FILENAME__, __func__,__LINE__, ## __VA_ARGS__)
#define p1_exit( fmt, ...) printf("[%s]%s(%d) exit:" fmt"\n", __FILENAME__, __func__,__LINE__, ## __VA_ARGS__)
#define DBG_IGNORE(...)                                  ((void)0)

#define p1_exit DBG_IGNORE

//#define __USE_UPPER__

int main()
{

#ifdef __WIN32__
  p1_enter("use macro");
  p1_enter("use macro");
#else
#ifdef __UNIX__
  p1("use macro %d %s", 1234, "charlyn" );
#endif


  p1_exit("use macro");
}


//header.h
#ifndef __HEADER_H_
#define __HEADER_H_

int a= 1;

#endif
