---
title: 记一次 C++ 代码 Debug 记录
date: 2022-05-30 00:37:07
tags:
---

我是短小精悍的文章摘要(๑•̀ㅂ•́) ✧

<!-- more -->

```c++
#include <iostream>
using namespace std;

typedef struct Student{
    string stuId;
    string name;
    double mathScore;
    double chineseScore;
    double englishScore;
} student;

typedef student ElemType;

typedef struct LinkList{
    ElemType elem;
    struct LinkList *next;
} linkList;

ElemType inputStudent();
linkList* initLink(int n);
linkList* insertElem(linkList * p,ElemType elem,int add);
void display(linkList *p);

int main(){
    int linked_length = 3;
    linkList* linked_stu = initLink(linked_length);

    student stu = inputStudent();

    // Student information is inputted from the keyboard
    linked_stu = insertElem(linked_stu,stu,2);

    display(linked_stu);

    return 0;
}

student inputStudent(){
    student stu;
    cout << "Id" << endl;
    cin >> stu.stuId;
    cout << "name" << endl;
    cin >> stu.name;
    cout << "mathScore" << endl;
    cin >> stu.mathScore;
    cout << "chineseScore" << endl;
    cin >> stu.chineseScore;
    cout << "englishScore" << endl;
    cin >> stu.englishScore;
    return stu;
}

linkList* initLink(int n){
    linkList * p=(linkList*)malloc(sizeof(linkList));//创建一个头结点
    linkList * temp=p;
    for (int i=1; i<n; i++) {
        linkList *a=(linkList*)malloc(sizeof(linkList));
        a->next=NULL;
        temp->next=a;
        temp=temp->next;
    }
    return p;
}

linkList* insertElem(linkList* p,ElemType elem,int add){
    linkList* temp=p; //创建临时结点temp
    for (int i = 1; i < add; i++) {
        if (temp==NULL) {
            printf("插入位置无效\n");
            return p;
        }
        temp=temp->next;
    }
    linkList* c = (linkList*)malloc(sizeof(linkList)); //创建插入结点c
    c -> elem = elem; //向链表中插入结点
    c->next = temp->next;
    temp->next = c;
    return  p;
}
void display(linkList *p){
    linkList* temp=p;//将temp指针重新指向头结点
    while (temp->next) {
        temp=temp->next;
        student stu = temp -> elem;
        cout << stu.stuId << endl;
    }
    printf("\n");
}
```

