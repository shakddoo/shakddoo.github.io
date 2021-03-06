---
layout: post
title:  "Android ndk, unicode to utf-8 or utf-8 to unicode"
date:   2016-02-01 21:34:00 +0900
category: c++
tags: [ndk, utf-8, unicode]
---
###1. utf-8 to unicode
I referenced [wiki](http://en.wikipedia.org/wiki/UTF-8)

``` cpp
wstring Utf8ToUnicode(const string& source_str)
{
    int dest_len 	= 0;
    int source_len 	= source_str.length();
    const char* source 	= source_str.c_str();
    wchar_t* dest 	= new wchar_t[source_len];

    wstring value;

    for (int i = 0; i < source_len; i++, dest_len++)
    {
        // ansi
        if (source[i] <= 127)
        {
            dest[dest_len] = source[i];
        }
        // 2byte
        else if ((source[i] & 0xF0) == 0xC0)
        {
            dest[dest_len] = ((source[i] & 0x1F) << 6) + (source[i+1] & 0x3F);
            i += 1;
        }
        // 3byte
        else if ((source[i] & 0xF0) == 0xE0)
        {
            dest[dest_len] = ((source[i] & 0x0F) << 12) + ((source[i+1] & 0x3F) << 6) + (source[i+2] & 0x3F);
            i += 2;
        }
        // ignore 4byte
        else
        {
            Log::warning("Can't change utf8 4byte characters");
            return value;
        }
    }

    value.assign(dest, dest_len);
    delete[] dest;
    return value;
}
```
If you use window, string has byte order(like EF BB BF). This case you have to remove byte order.


###2. unicode to utf-8
It don't support 4byte


``` cpp
string UnicodeToUtf8(const wstring& source_str)
{
    string value;
    int dest_len 			= 0;
    int source_len 			= source_str.length();
    const wchar_t* source 	= source_str.c_str();
    char* dest 				= new char[source_len*3 + 1];

    for(int i = 0 ; i < source_len ; i++)
    {
        if(source[i]<= 0x7F)
        {
            dest[dest_len] = source[i];
            dest_len++;
        }
        else if(source[i] >= 0x80 && source[i] <=0x7FF)
        {
            wchar_t tmp = source[i];
            char first = 0, second = 0, third = 0;
            for(int j = 0; j < 3 ; j++)
            {
                wchar_t tmp_quota = tmp%16;
                switch(j)
                {
                    case 0: third	 = tmp_quota; break;
                    case 1: second	 = tmp_quota; break;
                    case 2: first	 = tmp_quota; break;
                }
                tmp /= 16;
            }

            dest[dest_len] = 0xC0 + (first<<2) + (second>>2);
            dest[dest_len+1] = 0x80 + (((second%8)%4) << 4) + third;
            dest_len +=2;
        }
        else if(source[i] >= 0x800 && source[i] <=0xFFFF)
        {
            wchar_t tmp = source[i];
            char first = 0, second = 0, third = 0, fourth = 0;
            for(int j = 0; j < 4 ; j++)
            {
                wchar_t tmp_quota = tmp%16;
                switch(j)
                {
                    case 0: fourth	 = tmp_quota; break;
                    case 1: third	 = tmp_quota; break;
                    case 2: second	 = tmp_quota; break;
                    case 3: first	 = tmp_quota; break;
                }
                tmp /= 16;
            }

            dest[dest_len] = 0xE0 + first;
            dest[dest_len+1] = 0x80 + second << 2 + third >> 2;
            dest[dest_len+2] = 0x80 + (((third%8)%4) << 4) + fourth;
            dest_len +=3;
        }
        else
            return value;
    }
    dest[dest_len++] = '\0';

    value.assign(dest, dest_len);
    delete[] dest;
    return value;
}
```
