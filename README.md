#include<stdio.h>
#include<stdlib.h>
#include<string.h>
struct Book{
    int id;
    char title[100];
    char author[100];
    struct Book *next;
};
struct Book *create(int id,char title[],char author[]){
    struct Book *new=NULL;
    new=(struct Book *)malloc(sizeof(struct Book));
    new->id=id;
    strcpy(new->title,title);
    strcpy(new->author,author);
    new->next=NULL;
    return new;
}
void add(struct Book **head,int id,char title[],char author[]){
    struct Book *new=create(id,title,author);
    if(*head==NULL){
        *head=new;
        return;
    }
    else{
        struct Book *temp=*head;
        while(temp->next!=NULL){
            temp=temp->next;
        }
        temp->next=new;
        return;
    }
}
void display(struct Book *head){
    if(head==NULL)
    {
        printf("Library is empty");
        return;
    }
    else{
        struct Book *temp=head;
        while(temp!=NULL){
            printf("ID:%d\n",temp->id);
            printf("Title:%s\n",temp->title);
            printf("Author:%s\n",temp->author);
            temp=temp->next;
        }
        return;
    }
}
void search(struct Book *head,int id){
    while(head!=NULL){
        if(head->id==id){
            printf("Book found\nID:%d\nTitle:%s\nAuthor:%s",head->id,head->title,head->author);
            return;
        }
        head=head->next;
    }
    printf("Book not found");
}
void delete(struct Book **head,int id){
    struct Book *temp=*head;
    struct Book *previous=NULL;
    if(temp!=NULL && temp->id==id){
        *head=temp->next;
        free(temp);
        printf("Book deleted successfully");
        return;
    }
    while(temp!=NULL && temp->id!=id){
        previous=temp;
        temp=temp->next;
    }
    if(temp==NULL){
        printf("Book not found");
        return;
    }
    previous->next=temp->next;
    free(temp);
    printf("Book deleted scuccessfully");
}
int main(){
    struct Book *lib=NULL;
    int choice,id;
    char title[100],author[100];
    while(1){
        printf("\n___Library Menu___\n");
        printf("1.Add Book\n2.Display Books\n3.Search Books\n4.Delete Books\n5.Exit\nEnter your choice:");
        scanf("%d",&choice);
        switch(choice){
            case 1:
            printf("Enter Book ID:");
            scanf("%d",&id);
            printf("Enter Book title(without spaces):");
            scanf("%s",title);
            printf("Enter Book Author(without spaces):");
            scanf("%s",author);
            add(&lib,id,title,author);
            break;
            case 2:
            display(lib);
            break;
            case 3:
            printf("Enter book id:");
            scanf("%d",&id);
            search(lib,id);
            break;
            case 4:
            printf("Enter the book id:");
            scanf("%d",&id);
            delete(&lib,id);
            break;
            case 5:
            printf("Exiting...\n");
            exit(0);
            default:
            printf("Invalid choice\n");
        }
    }
    return 0;
}
