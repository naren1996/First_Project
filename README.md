This project can split large text file into four smaller file and after that it can also merge those splitted file.
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
int Merge();
int Split();
int main()
{
    int c;
    char ch;
    printf("\n\t\tEnter your Choice");
    printf("\n\t1.Split text file");
    printf("\n\t2.Merge the splitted file");
    printf("\n\t");
    scanf("%d",&c);
    fflush(stdin);
    switch(c)
    {
    case 1:
        Split();
        break;
    case 2:
        Merge();
    }
    if(c == 1) {
        printf("\n\tDo you want to merge the file [Y/N]");
        scanf("%c",&ch);
        if(ch == 'Y' || ch == 'y') Merge();
        else printf("\n\tFile merged successfully");
    }
 return 0;
}


int Split()
{
    FILE *fp;
    FILE fp1;
    char str1[10000];
    char str2[2500];
    char fname[20];
    int i,j,len,a;
    printf("\n\tEnter the file name with (.txt) extension \"eg.file_name.txt\" : ");
    scanf("%[^\n]s",fname);
    fp=fopen(fname,"r");
    if (fp==NULL)
    {
     printf("\n\tFile not found");
     return 0 ;
    }
    fscanf(fp,"%[]s",str1); //Reading whole data from file.
    fflush(stdin);


    len = strlen(str1); //Calculating original string length.
    if(len%4==0) a=len/4;
    else a=((len/4)+(len%4)); //Dividing length into four parts.

    j=0;
    for(i=0;i<a;i++,j++) str2[j] = str1[i];
    str2[j] = '\0';
    fp = fopen("file1.txt","w");
    fprintf(fp,"%s",str2);
    fclose(fp);


    for(i=0;i<a;i++,j++) str2[i] = str1[j];
    str2[j] = '\0';
    fp = fopen("file2.txt","w");
    fprintf(fp,"%s",str2);
    fclose(fp);

    for(i=0;i<a;i++,j++) str2[i] = str1[j];
    str2[j] = '\0';
    fp = fopen("file3.txt","w");
    fprintf(fp,"%s",str2);
    fclose(fp);

    for(i=0;i<a;i++,j++) str2[i] = str1[j];
    str2[j] = '\0';
    fp = fopen("file4.txt","w");
    fprintf(fp,"%s",str2);
    fclose(fp);


    return 0;
}
int Merge()
{
    char str1[10000], str2[2500];
    FILE *fp;
    int i,j=0,l;
    printf("\n\tPress Enter to merge the file");
    getchar();

    fp=fopen("file1.txt","r");
    fscanf(fp,"%[]s",str2);
    l=strlen(str2);
    for(i=0;i<l;i++,j++) str1[j] = str2[i];
    fclose(fp);

    fp=fopen("file2.txt","r");
    fscanf(fp,"%[]s",str2);
    for(i=0;i<l;i++,j++) str1[j] = str2[i];
    fclose(fp);

    fp=fopen("file3.txt","r");
    fscanf(fp,"%[]s",str2);
    for(i=0;i<l;i++,j++) str1[j] = str2[i];
    fclose(fp);

    fp = fopen("file4.txt","r");
    fscanf(fp,"%[]s",str2);
    for(i=0;i<l;i++,j++) str1[j] = str2[i];
    fclose(fp);

    str1[j] = '\0';
    fp = fopen("MergeNew.txt","w");
    if(fp==NULL) {
        printf("\n\tUnable to open the file");
        return 0;
    }
    fprintf(fp,"%s",str1);
    fclose(fp);
    printf("\n\tFile Successfully Merged");

    return 0;
}




