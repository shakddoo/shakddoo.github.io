---
layout: post
title:  "int to currency string"
date:   2016-03-30 00:12:00 +0900
category: ios
tags: [c++]
---


In Games, number to currency-expression like, 1000000 -> 1,000,000

``` cpp

std::string Util::numberToCurrency(int num)
{
    if(num == 0)
        return string("0");

    char currentArray[20];
    int64_t tmpNum = num;
    int numLength = Util::NumLength(num);
    int commaCount = (numLength%3) != 0 ? (numLength/3) : (numLength/3) -1;
    if(commaCount < 0)
        commaCount = 0;

    int currentLength = num > 0 ? numLength + commaCount : numLength + commaCount + 1;

    if(currentLength > 20)
        return string();

    currentArray[currentLength] = '\0';

    int j = 0;
    for(int i = currentLength - 1 ; tmpNum > 0 ; tmpNum /= 10, j++)
    {
        currentArray[i--] = tmpNum % 10 + '0';
        if(j%3 == 2)
        currentArray[i--] = ',';
    }

    if(num < 0)
        currentArray[0] = '-';

    return string(currentArray);
}

```