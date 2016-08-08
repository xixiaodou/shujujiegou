# shujujiegou
c 语言描述--单链表
#include<stdio.h>
#include<malloc.h>
typedef struct LNode
{
	int data;
    struct LNode *next;
}LNode,*LinkList;//函数的声
struct LNode *Create_list();
void View_list (LinkList head);
void Change_list(LinkList &head);
void Merger_list(LinkList &head,LinkList &Lb,LinkList &Lc);
void Merger_list2(LinkList &head,LinkList &Lb,LinkList &Lc);
int main()
{
	LinkList Lb,Lc,head;
	Lc=NULL;
	//等价于struct LNode *head
	int i;
while (1){
	printf("*****1.创建链表           2.遍历链表*******************************\n");
	printf("*****3.逆置               4.创建两个非递减的链表，合并成一个非递减的链表\n");
	printf("*****5.创建两个非递增的链表，合并成一个非递增的链表**************\n");

	printf("********************************************;\n");
	printf("请输入选择的序号：");
	scanf("%d",&i);
	switch (i){
		case 1:printf("创建链表");
			  head= Create_list();break;
			case 2:
                View_list(head);break;
			case 3:
				Change_list(head);break;
			case 4:
				printf("请按照指示输入两组非递减的数：\n");
				head= Create_list();
			    Lb= Create_list();
				Merger_list(head,Lb,Lc);
                View_list(head);break;
            case 5:
				printf("按照指示输入两组非递増的数：\n");
				head= Create_list();
				Lb= Create_list();
				Merger_list2(head,Lb,Lc);
                View_list(head);break;

			}
		}

	return 0;

}



struct LNode *Create_list()//建立一个带头节点的单链表//LinkList Create_list()
{
	int len,i,vai;
	LinkList p;
	LinkList head=(LinkList)malloc(sizeof(LNode));
	head->next=NULL;
	p=head;
	if(head==NULL)
	{
		printf("error");
	}
	printf("请输入创建数据的个数：");
	scanf("%d",&len);
	for(i=0;i<len;++i）
	{
		printf("第%d个数字为：",i+1);
		scanf("%d",&vai);
		LinkList s=(LinkList)malloc(sizeof(LNode));
		if(s==NULL)
	{
      	printf("error");
	}
		s->data=vai;
		s->next=p->next;
		p->next=s;
		p=p->next;
	}
	return head;
}
void View_list(LinkList head){//遍历链表
if (head==NULL)
printf("error");
	LinkList p;
	p=head->next;
	printf("遍历链表结果为：\n");
   while (p)
	{
	   printf("%4d",p->data);
	   p=p->next;
	}
   printf("\n");
}
void Change_list(LinkList &head){//逆置
	LinkList p,s;
	p=head->next;
	head->next=NULL;
	while (p){
		s=p;
		p=p->next;
		s->next=head->next;
		head->next=s;
	}
	View_list(head);
}

void Merger_list(LinkList &head,LinkList &Lb,LinkList &Lc){
//合并
	LinkList Pa,Pb,Pc,s;
	Pa=head->next;
	Pb=Lb->next;
	Lc=Pc=head;
	while (Pa&&Pb){//排序非递减
		if (Pa->data<Pb->data){
		s=Pa;
		Pa=Pa->next;
		}
		else{
		s=Pb;
		Pb=Pb->next;
		}
		s->next=Pc->next;
		Pc->next=s;
		Pc=Pc->next;
	}
	if (Pa)
		Pc->next=Pa;
	else
		Pc->next=Pb;
	free(Lb);

}

void Merger_list2(LinkList &head,LinkList &Lb,LinkList &Lc){
//合并
	LinkList Pa,Pb,Pc,s;
	Pa=head->next;
	Pb=Lb->next;
	Lc=Pc=head;
	while (Pa&&Pb){//排序非递
		if (Pa->data>=Pb->data)
		{
	    	s=Pa;
	    	Pa=Pa->next;
		}
		else
		{
		    s=Pb;
	    	Pb=Pb->next;
		}
		s->next=Pc->next;
		Pc->next=s;
		Pc=Pc->next;
	}
	if (Pa)
		Pc->next=Pa;
	else
		Pc->next=Pb;
	free(Lb);
}
