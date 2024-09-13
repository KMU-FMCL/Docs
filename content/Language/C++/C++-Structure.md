---
title: Structure
tag: CPP
---

## Structure

- C++ 언어에서는 구조체의 <font color='red'>**태그(tag)가 곧 자료형**</font>

> [!example]
>
> ```cpp
> #include <iostream>
> using namespace std;
>
> struct Score {
>           char  name[12];
>           int   kor, eng, math, tat;
>           flot  ave;
> };
>
> int main()
> {
>           // Struct Score   temp;       // C Language Style
>           Score             temp;       // C++ Language Style
>
>           return 0;
> }
> ```

> [!question] 구조체 & 공용체
>
> > [!example] Big endian & Little endian
> >
> > ```cpp
> > #include <iostream>
> > using namespace std;
> >
> > // 비트 필드 구조체 형식 정의
> > struct Unit {
> >         unsigned int  FirstBit : 8;
> >         unsigned int  SecondBit : 8;
> >         unsigned int  ThirdBit : 8;
> >         unsigned int  ForthBit : 8;
> > };
> >
> > // 공용체 형식 정의: 정수형과 구조체 멤버
> > union Endian {
> >         int     a;      // 정수형 멤버
> >         Uint    b;      // 구조체 멤버
> > };
> >
> > int main()
> > {
> >       // 공용체 변수 선언
> >       Endian          temp;
> >       temp.a = 0x12345678;
> >
> >       // "Big endian" & "Little endian"
> >       cout << hex;
> >       cout << "temp.i: " << temp.a << endl;             // x12345678
> >       cout << "temp.i: " << temp.b.FirstBit << endl;    // 78
> >       cout << "temp.i: " << temp.b.SecondBit << endl;   // 56
> >       cout << "temp.i: " << temp.b.ThirdBit << endl;    // 34
> >       cout << "temp.i: " << temp.b.ForthBit << endl;    // 12
> >
> >       return 0;
> > }
> > ```
>
> > [!example] TV 채널
> >
> > ```cpp
> > #include <iostream>
> > using namespace std;
> >
> > int main()
> > {
> >         // 열거형 정의
> >         enum TV {
> >                 afn = 2, sbs = 6, kbs2 = 7,
> >                 kbs1 = 9, mbc = 11, ebs = 13,
> >                 ytn = 60, mbn = 61, cnn = 51
> >         };
> >
> >         cout << "즐겨보는 TV 채널 목록" << endl;
> >         cout << "   AFN : " << afn << endl;
> >         cout << "   SBS : " << sbs << endl;
> >         cout << "   KBS2: " << kbs2 << endl;
> >         cout << "   KBS1: " << kbs1 << endl;
> >         cout << "   MBC : " << mbc << endl;
> >         cout << "   EBS : " << ebs << endl;
> >         cout << "   YTN : " << ytn << endl;
> >         cout << "   CNN : " << cnn << endl;
> >
> >         return 0;
> > }
> > ```
