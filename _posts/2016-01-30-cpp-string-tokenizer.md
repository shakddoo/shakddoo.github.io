---
layout: post
title:  "c++ string tokenizer implement"
date:   2016-01-30 02:38:00 +0900
categories: c++
---
#1. Implement
This code use string class instead of strtok included in <string.h>.

``` cpp
void StringTokenize(const string& str, vector<string>& tokens, const string& delimiters)
{
    // Skip delimiters at beginning.
    string::size_type lastPos = str.find_first_not_of(delimiters, 0);
    // Find first "non-delimiter".
    string::size_type pos     = str.find_first_of(delimiters, lastPos);

    while (string::npos != pos || string::npos != lastPos)
    {
        // Found a token, add it to the vector.
        tokens.push_back(str.substr(lastPos, pos - lastPos));
        // Skip delimiters.  Note the "not_of"
        lastPos = str.find_first_not_of(delimiters, pos);
        // Find next "non-delimiter"
        pos = str.find_first_of(delimiters, lastPos);
    }
}
```
- const string& str : target string to be split by delimiters
- vector<string>& tokens : split sub strings will be pushed. This parameter is reference type, so It have to be not null.


#2. Using Example


``` cpp
void main()
{
    vector<string> quiz_str_list;
    string quiz_str = "abc:def:ghi"        
    StringTokenize(quiz_str, quiz_str_list, ":");

    for(auto token : quiz_str_list)
    printf("%s\n", token.c_str());
}
```


Token size is 3. Result is

"abc"

"def"

"ghi"
