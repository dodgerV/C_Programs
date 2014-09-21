#include <stdio.h>

void change(int Parametr)
{
   int count=0,summ=0, temp=0,top=0,check=0, test=0,cycle=0;
   int i=0,j=0,l=0,t=0;
   int parametr=Parametr;
   int matrix [parametr][parametr]; 
   
   printf("Матрица до изменения:\n");
   for(i=0; i<parametr; i++)
   {
      for(j=0; j<parametr; j++)
      {
         matrix[i][j]=i*2-j;
         printf("%i\t",matrix[i][j]);
      }
         printf("\n");
   }

   //1)

   for(i=0;i<parametr-1;i++)
   {
      matrix[parametr-1][0]+=matrix[i][0];
   }  

   for(i=parametr-2;i>0;i--)
   {
       count=1;
      for(t = 0; t<i+1; t++)
      {
         summ +=matrix[t][0]; // прибавление вертикали
      }
      for(l = i+1; l < parametr; l++)
      {
         summ+=matrix[l][count]; // прибавление диагонали
         count++;
      }
      matrix[i][0]=summ;
      summ=0;
   }
      // 2)

   for(j=1; j<parametr-1; j++)
{
   for(t=1; t<=j;t++)
   {
      for(i=0; i<parametr-1-j+t;i++)
      {
      summ+=matrix[i][t];
      }   
   }
      matrix[parametr-1][j]=matrix[parametr-1-j][0]+summ;
      summ=0;
}
      // 3)
   
   count=0;
   for(j=1; j<parametr-2;j++)
   {
      
      temp=1;
      for(i=parametr-2; i>1+count;i--)
      {
         summ=0; 
         for(t=0; t<parametr-1; t++)
         {
            summ+=matrix[t][j+temp];
         }
         matrix[i][j]=matrix[parametr-1][j+temp]-summ;
         temp++;
      
      }
      count++;
      
   }
      // 4)
      
      temp=1;
      for(j=parametr-2; j>=0;j--)
      {
            count=parametr-1;
            summ=0;
            for(l = temp; l >0; l--)
            {
               summ+=matrix[l][count];
               count--;
            }

         matrix[0][j]+=summ;
         temp++;
         
      }
      // 5)
      top=0;
      summ=0;
      for(cycle=0; cycle<parametr-2;cycle++)
      {
         check=0;
         for(i=1,j=1+top; i<parametr-1-top, j<parametr-1; i++,j++)
         {
            count=0;
            summ=0;
            for(t=top;t<j+1;t++)
            {
               
               if(t==top)
               {
                  count+=matrix[0][t];
               }
               else
               {
                  temp=matrix[0][t];
                  for(test=parametr-1; test>j;test--)
                  {

                     temp-=matrix[test-t][test];

                  }
                  summ+=temp;
                  

               }

            }
       

            matrix[i][j]=summ+count;
            summ=0;
            
         }
         top++;
      }
      
      // 6)

      temp=0;
      for(i=parametr-1; i>0;i--)
      {
         summ=0;
         for(t=temp; t<parametr;t++)
         {
            summ+=matrix[0][t];
         }
         matrix[i][parametr-1]=summ;
         temp++;
      }
      
      // Algoritm finished

      printf("Матрица после изменения:\n");
   
   for(i=0; i<parametr; i++)
      {
         for(j=0; j<parametr; j++)
         {
            printf("%i\t",matrix[i][j]);
         }
         printf("\n");
      }  
}

int main(void)
{
	int parametr=9;
	int line=5, column=6;
	
	printf("Введите количество строк и столбцов: ");
	scanf("%i",&parametr);
	//printf("Введите номер строки и столбца элемента для изменения: ");
	//scanf("%i,%i",&line,&column);
	change(parametr);
}

   

