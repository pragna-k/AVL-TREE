# AVL-TREE

#include<stdio.h>
#include<stdlib.h>
#include<math.h>
struct AVL
{
        int data,height;
        struct AVL *left,*right;
};
typedef struct AVL node;
int max(int a,int b)
{
    if(a>b)
    {
        return a;
    }
    else
    {
        return b;
    }
}
node* single_LL(node *k2)
{
        node *k1=k2->left;
        k2->left=k1->right;
        k1->right=k2;
        return k1;
}
node* single_RR(node *k1)
{
        node *k2=k1->right;
        k1->right=k2->left;
        k2->left=k1;
        return k2;
}
node* double_LR(node *k3)
{
        k3->left=single_RR(k3->left);
        return(single_LL(k3));
}
node* double_RL(node *k1)
{
        k1->right=single_LL(k1->right);
        return(single_RR(k1));
}
int height(node *p)
{
        if(p==NULL)
                return -1;
        else
                return p->height;
}
node* insert(node *p,int x)
{
        if(p==NULL)
        {
                p=(node*)malloc(sizeof(node));
                p->data=x;
                p->right=p->left=NULL;
                p->height=0;
        }
        else if(x<p->data)
        {
                p->left=insert(p->left,x);
                if(abs(height(p->left)-height(p->right))==2)
                {
                        if(x<p->left->data)
                        {
                                p=single_LL(p);
                        }
                        else
                        {
                                p=double_LR(p);
                        }
                }
        }
        else if(x>p->data)
        {
                p->right=insert(p->right,x);
                if(abs(height(p->right)-height(p->left))==2)
                {
                        if(x>p->right->data)
                        {
                                p=single_RR(p);
                        }
                        else
                        {
                                p=double_RL(p);
                        }
                }
        }
        p->height=max(height(p->left),height(p->right))+1;
        return p;
}
void inorder(node *p)
{
        if(p!=NULL)
        {
                inorder(p->left);
                printf("%d\t",p->data);
                inorder(p->right);
        }
}
void preorder(node *p)
{
        if(p!=NULL)
        {
                printf("%d\t",p->data);
                preorder(p->left);
                preorder(p->right);
        }
}
void postorder(node *p)
{
        if(p!=NULL)
        {
                postorder(p->left);
                postorder(p->right);
                printf("%d\t",p->data);
        }
}
void main()
{
        node *root=NULL;
        int x,ch;
        printf("1.INSERT\n2.INORDER\n3.PREORDER\n4.POSTORDER\n5.EXIT\n");
        while(1)
        {
                printf("Enter your choice: \n");
                scanf("%d",&ch);
                switch(ch)
                {
                        case 1: printf("Enter the element into AVL tree :\n ");
                                scanf("%d",&x);
                                root=insert(root,x);
                                break;
                        case 2: printf("The inorder traversal of the AVL tree is: \n");
                                inorder(root);
                                break;
                        case 3: printf("The preorder traversal of the AVL tree is: \n");
                                preorder(root);
                                break;
                        case 4: printf("The postorder traversal of the AVL tree is: \n");
                                postorder(root);
                                break;
                        case 5:exit(0);
                               break;
                }
        }
}
        OUTPUT:
        1.INSERT
2.INORDER
3.PREORDER
4.POSTORDER
5.EXIT
Enter your choice: 
1
Enter the element into AVL tree :
 25
Enter your choice: 
1
Enter the element into AVL tree :
 30
Enter your choice: 
1
Enter the element into AVL tree :
 93
Enter your choice: 
2
The inorder traversal of the AVL tree is: 
25	30	93	Enter your choice: 
3
The preorder traversal of the AVL tree is: 
30	25	93	Enter your choice: 
4
The postorder traversal of the AVL tree is: 
25	93	30	Enter your choice: 

5
exit
