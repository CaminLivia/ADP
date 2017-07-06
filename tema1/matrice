#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>

#define N 15
#define nrThread 8    //numarul de threaduri folosit

int matrice_A[500][500];
int matrice_B[500][500];
int matrice_Rezultat[500][500];


//functia care va fi executata de toate thread-urile
void *Inmultire_Matrici(void *param)
{

    int id = *(int *)param;
    int i,j,k;

    printf("Thread %d start inmultire\n",id);
    for (i = id; i < N; i+= nrThread)
    {
        printf("Thread =%d  LINIE =%d\n",id,i);
        for(j = 0; j < N; j++)
        {
            for(k = 0; k < N; k++)
            {
                matrice_Rezultat[i][j]+=matrice_A[i][k] * matrice_B[k][j];
            }
        }
    }
    pthread_exit(NULL);

}

int main()
{
    pthread_t thread[nrThread];
    int tid[nrThread];

	int i, j;

    //Initializare matricea A cu valori random 

    for(i=0;i<N;i++)
    {
        for(j=0;j<N;j++)
        {
            matrice_A[i][j] = rand()%10;
        }
    }

    printf("\n");

    //Initializare matricea B cu valori random 

    for(i=0;i<N;i++)
    {
        for(j=0;j<N;j++)
        {
            matrice_B[i][j] = rand()%10;
        }
    }

    //Initializare matrice rezultat cu 0

    for(i=0;i<N;i=i+2)
        {
            for(j=0;j<N;j=j+2)
            {
                matrice_Rezultat[i][j]=0;
            }
        }

        for (i = 0; i < nrThread; i++) {

            tid[i]=i;
            pthread_create(&thread[i], NULL, Inmultire_Matrici, &tid[i]);


        }

        for (i = 0; i < nrThread; i++)
        {
            pthread_join(thread[i], NULL);
        }


    //Afisam rezultatul

        printf("\n Rezultatul inmultiri matricilor A si B : \n");

        for(i=0;i<N;i++)
        {
            for(j=0;j<N;j++)
            {
                printf("%d \t",matrice_Rezultat[i][j]);
            }
            printf("\n");
        }

	return 0;


}
