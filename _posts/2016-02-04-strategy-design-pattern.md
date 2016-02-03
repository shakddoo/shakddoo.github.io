---
layout: post
title:  "Using strategy Design-Pattern"
date:   2016-02-04 01:08:00 +0900
category: c++
tags: [Design Pattern, Strategy]
---
#1. Proc
- Reduce overlapping programming
- Fiexible 

#2. Using case
- When you have to override a method of Super-Class, don’t override the method. Make to Interface (like AttackBehavior)

#3. Example Code
Below code show cons when programmer use Inheritance.

``` cpp
class Character
{
protected :
    virtual void attack()
    {
        printf("kick and punch");
    }
}

class Knight : public Character
{
public :
    void attack() override
    {
        printf("swing sword");
    }
}

class Magician : public Character
{
public :
    void attack() override
    {
        printf("fire fire-ball");
    }
}
```

If Some Characters(Knight, Thief etc..) have same attack() method **"kick and punch"**, you would copy Knight’s attack() method to other Character classes.
Copy make overlapped and inflexible codes. And if you have to change **“kick and punch”** to **"kick and kick"**, you would change all Characters that defined attack() method to “kick and punch”.


To solve this problem, use Strategy Design-Pattern. 

``` cpp

class Behavior
{
    virtual void do() = 0;
}

class AttackBehavior : public Behavior
{
    void do() override
    {
        printf("kick and punch");
    }
}

class MagicBehavior : public Behavior
{
    void do() override
    {
        printf("fire fire-ball");
    }
}

class Character
{
    
protected :
    Behavior*    _behavior
public:
    Character();
    virtual ~Character();

    void attack()
    {
        _behavior->do();
    }
}

class Knight : public Character
{
public :
    Knight()
    {
        _behavior = new AttackBehavior();
    }
}

class Magician : public Character
{
public :
    Magician()
    {
        _behavior = new MagicBehavior();
    }
}
```

If Some Characters(Knight, Thief etc..) have same attack() method **"kick and punch"**, set **'_behavior'** to **AttackBehavior**.
If you have to change method **"kick and punch"** to **"kick and kick"**, just change **AttackBehavior** interface.
