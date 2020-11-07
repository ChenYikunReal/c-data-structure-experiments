# 实验一 线性表的应用

本实验需要使用链表完成！我决定都使用带有头结点的单链表做。

1.学生成绩统计：用线性表存储学生的各科成绩，并可以统计某门课的最高分、最低分、平均分情况（可适当添加其他统计功能）。

我们假设有三门课程的成绩。

代码如下：
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

typedef struct student Student;

struct student {
    int id;
    char name[50];
    int grades[3];
    Student *next;
};

int main() {
    srand((unsigned int)time(0));
    Student *head = (Student *)malloc(sizeof(Student)), *p = head, *temp;
    head->next = NULL;
    int n = 10, m = 3, i, j, num;
    char names[10][50] = {"Sam", "Bob", "Tom", "Yuki", "Steven", "Amy", "Joe", "XiaoMing", "David", "Eleven"};
    for (i = 1; i <= n; i++) {
        temp = (Student *)malloc(sizeof(Student));
        temp->id = 20200000+i;
        strcpy(temp->name, names[i-1]);
        for (j = 0; j < m; j++) {
            num = rand() % 101;
            temp->grades[j] = num;
        }
        temp->next = NULL;
        p->next = temp;
        p = temp;
    }
    int counter = 0;
    // 遍历一遍链表以作测试
    p = head;
    while (p->next != NULL) {
        p = p->next;
        counter++;
        printf("学生%d的学号为%d 姓名为%s 科目1成绩为%d 科目2成绩为%d 科目3成绩为%d\n", counter, p->id,
                p->name,p->grades[0], p->grades[1], p->grades[2]);
    }
    // 统计科目2的最高分
    int max = -0xfffffff;
    p = head;
    while (p->next != NULL) {
        p = p->next;
        if (p->grades[1] > max) {
            max = p->grades[1];
        }
    }
    printf("科目2的最高分是%d\n", max);
    // 统计科目3的平均分
    double sum = 0;
    counter = 0;
    p = head;
    while (p->next != NULL) {
        p = p->next;
        counter++;
        sum += p->grades[2];
    }
    printf("科目3的平均分是%.2lf\n", sum/counter);
    return 0;
}
```

2.集合运算：用线性表存储集合数据，并完成集合运算，至少包括集合的交集、并集、补集、差集。

代码如下：
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct element Element;

struct element {
    int value;
    Element *next;
};

int main() {
    // 集合A
    Element *head_a = (Element *)malloc(sizeof(Element)), *p_a = head_a, *temp;
    temp = (Element *)malloc(sizeof(Element));
    temp->value = 3;
    p_a->next = temp;
    p_a = temp;
    temp = (Element *)malloc(sizeof(Element));
    temp->value = 4;
    p_a->next = temp;
    p_a = temp;
    temp = (Element *)malloc(sizeof(Element));
    temp->value = 10;
    p_a->next = temp;
    p_a = temp;
    temp = (Element *)malloc(sizeof(Element));
    temp->value = 6;
    p_a->next = temp;
    p_a = temp;
    p_a->next = NULL;
    // 查看集合A的元素
    p_a = head_a;
    while (p_a->next != NULL) {
        p_a = p_a->next;
        printf("%d ", p_a->value);
    }
    printf("\n");

    // 集合B
    Element *head_b = (Element *)malloc(sizeof(Element)), *p_b = head_b;
    temp = (Element *)malloc(sizeof(Element));
    temp->value = 1;
    p_b->next = temp;
    p_b = temp;
    temp = (Element *)malloc(sizeof(Element));
    temp->value = 6;
    p_b->next = temp;
    p_b = temp;
    temp = (Element *)malloc(sizeof(Element));
    temp->value = 5;
    p_b->next = temp;
    p_b = temp;
    temp = (Element *)malloc(sizeof(Element));
    temp->value = 10;
    p_b->next = temp;
    p_b = temp;
    p_b->next = NULL;
    // 查看集合B的元素
    p_b = head_b;
    while (p_b->next != NULL) {
        p_b = p_b->next;
        printf("%d ", p_b->value);
    }
    printf("\n");

    // 求A∪B 定义为集合C
    Element *head_c = (Element *)malloc(sizeof(Element)), *p_c = head_c;
    p_a = head_a;
    while (p_a->next != NULL) {
        p_a = p_a->next;
        temp = (Element *)malloc(sizeof(Element));
        temp->value = p_a->value;
        temp->next = NULL;
        p_c->next = temp;
        p_c = temp;
    }
    p_b = head_b;
    int flag;
    while (p_b->next != NULL) {
        p_b = p_b->next;
        flag = 1;
        p_a = head_a;
        while (p_a->next != NULL) {
            p_a = p_a->next;
            if (p_a->value == p_b->value) {
                flag = 0;
                break;
            }
        }
        if (flag) {
            temp = (Element *)malloc(sizeof(Element));
            temp->value = p_b->value;
            temp->next = NULL;
            p_c->next = temp;
            p_c = temp;
        }
    }
    // 查看集合C的元素
    p_c = head_c;
    while (p_c->next != NULL) {
        p_c = p_c->next;
        printf("%d ", p_c->value);
    }
    printf("\n");

    // 求A∩B 定义为集合D
    Element *head_d = (Element *)malloc(sizeof(Element)), *p_d = head_d;
    p_b = head_b;
    while (p_b->next != NULL) {
        p_b = p_b->next;
        p_a = head_a;
        while (p_a->next != NULL) {
            p_a = p_a->next;
            if (p_a->value == p_b->value) {
                temp = (Element *)malloc(sizeof(Element));
                temp->value = p_b->value;
                temp->next = NULL;
                p_d->next = temp;
                p_d = temp;
                break;
            }
        }
    }
    // 查看集合D的元素
    p_d = head_d;
    while (p_d->next != NULL) {
        p_d = p_d->next;
        printf("%d ", p_d->value);
    }
    printf("\n");

    // 设全集为A∪B，求A的补集 定义为集合E
    Element *head_e = (Element *)malloc(sizeof(Element)), *p_e = head_e;
    p_c = head_c;
    while (p_c->next != NULL) {
        p_c = p_c->next;
        flag = 1;
        p_a = head_a;
        while (p_a->next != NULL) {
            p_a = p_a->next;
            if (p_a->value == p_c->value) {
                flag = 0;
                break;
            }
        }
        if (flag) {
            temp = (Element *)malloc(sizeof(Element));
            temp->value = p_c->value;
            temp->next = NULL;
            p_e->next = temp;
            p_e = temp;
        }
    }
    // 查看集合E的元素
    p_e = head_e;
    while (p_e->next != NULL) {
        p_e = p_e->next;
        printf("%d ", p_e->value);
    }
    printf("\n");

    // 求A-B
    Element *head_f = (Element *)malloc(sizeof(Element)), *p_f = head_f;
    p_a = head_a;
    while (p_a->next != NULL) {
        p_a = p_a->next;
        flag = 1;
        p_b = head_b;
        while (p_b->next != NULL) {
            p_b = p_b->next;
            if (p_a->value == p_b->value) {
                flag = 0;
                break;
            }
        }
        if (flag) {
            temp = (Element *)malloc(sizeof(Element));
            temp->value = p_a->value;
            temp->next = NULL;
            p_f->next = temp;
            p_f = temp;
        }
    }
    // 查看集合F的元素
    p_f = head_f;
    while (p_f->next != NULL) {
        p_f = p_f->next;
        printf("%d ", p_f->value);
    }
    printf("\n");

    return 0;
}
```

3.一元多项式运算：用线性表存储一元多项式，并完成一元多项式的求和运算

简化的部分：
- 这里假设多项式的幂次只有非负数。
- 直接指定了多项式的值且添加顺序就是有序的。

代码如下：
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct term Term;

struct term {
    int coefficient;
    int power;
    Term *next;
};

void print(Term *p) {
    if (p->next != NULL) {
        p = p->next;
        if (p->power == 0) {
            printf("%d", p->coefficient);
        } else {
            printf("%dx^%d", p->coefficient, p->power);
        }
        while (p->next != NULL) {
            p = p->next;
            if (p->coefficient > 0) {
                printf("+");
            }
            if (p->coefficient != 1) {
                printf("%d", p->coefficient);
            }
            printf("x");
            if (p->power != 1) {
                printf("^%d", p->power);
            }
        }
    }
    printf("\n");
}

void add(Term *p_a, Term *p_b, Term *p_c, Term *temp) {
    while (p_a->next != NULL || p_b->next != NULL) {
        if (p_a->next == NULL) {    // 只剩B多项式
            p_b = p_b->next;
            temp = (Term *)malloc(sizeof(Term));
            temp->coefficient = p_b->coefficient;
            temp->power = p_b->power;
            temp->next = NULL;
            p_c->next = temp;
            p_c = temp;
        } else if (p_b->next == NULL) {    // 只剩A多项式
            p_a = p_a->next;
            temp = (Term *)malloc(sizeof(Term));
            temp->coefficient = p_a->coefficient;
            temp->power = p_a->power;
            temp->next = NULL;
            p_c->next = temp;
            p_c = temp;
        } else {    // A和B都没结束
            if (p_a->next->power == p_b->next->power) {    // A和B同幂次
                p_a = p_a->next;
                p_b = p_b->next;
                if (p_a->coefficient + p_b->coefficient != 0) {
                    temp = (Term *)malloc(sizeof(Term));
                    temp->coefficient = p_a->coefficient + p_b->coefficient;
                    temp->power = p_a->power;
                    temp->next = NULL;
                    p_c->next = temp;
                    p_c = temp;
                }
            } else if (p_a->next->power > p_b->next->power) {    // A幂次大于B
                p_b = p_b->next;
                temp = (Term *)malloc(sizeof(Term));
                temp->coefficient = p_b->coefficient;
                temp->power = p_b->power;
                temp->next = NULL;
                p_c->next = temp;
                p_c = temp;
            } else {    // A幂次小于B
                p_a = p_a->next;
                temp = (Term *)malloc(sizeof(Term));
                temp->coefficient = p_a->coefficient;
                temp->power = p_a->power;
                temp->next = NULL;
                p_c->next = temp;
                p_c = temp;
            }
        }
    }
}

int main() {
    // 多项式A : 100+x-2x^2+5x^7
    Term *head_a = (Term *)malloc(sizeof(Term)), *p_a = head_a, *temp;
    temp = (Term *)malloc(sizeof(Term));
    temp->coefficient = 100;
    temp->power = 0;
    temp->next = NULL;
    p_a->next = temp;
    p_a = temp;
    temp = (Term *)malloc(sizeof(Term));
    temp->coefficient = 1;
    temp->power = 1;
    temp->next = NULL;
    p_a->next = temp;
    p_a = temp;
    temp = (Term *)malloc(sizeof(Term));
    temp->coefficient = -2;
    temp->power = 2;
    temp->next = NULL;
    p_a->next = temp;
    p_a = temp;
    temp = (Term *)malloc(sizeof(Term));
    temp->coefficient = 5;
    temp->power = 7;
    temp->next = NULL;
    p_a->next = temp;
    // 打印多项式A
    p_a = head_a;
    print(p_a);

    // 多项式B : 2x^2+4x^4-6x^8
    Term *head_b = (Term *)malloc(sizeof(Term)), *p_b = head_b;
    temp = (Term *)malloc(sizeof(Term));
    temp->coefficient = 2;
    temp->power = 2;
    temp->next = NULL;
    p_b->next = temp;
    p_b = temp;
    temp = (Term *)malloc(sizeof(Term));
    temp->coefficient = 4;
    temp->power = 4;
    temp->next = NULL;
    p_b->next = temp;
    p_b = temp;
    temp = (Term *)malloc(sizeof(Term));
    temp->coefficient = -6;
    temp->power = 8;
    temp->next = NULL;
    p_b->next = temp;
    // 打印多项式B
    p_b = head_b;
    print(p_b);

    // A+B的求和结果是C
    Term *head_c = (Term *)malloc(sizeof(Term)), *p_c = head_c;
    p_a = head_a;
    p_b = head_b;
    add(p_a, p_b, p_c, temp);
    print(p_c);

    return 0;
}
```

[下一个实验](/Experiment2.md)

[返回首页](/README.md)
