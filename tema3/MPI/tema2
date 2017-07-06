#include <iostream>
#include <mpi.h>
#include <math.h>

using namespace std;

#define SIZE 20

int main(int argc, char *argv[])
{
    int  rank;      
    int  nrprocs;   // nr process
	int arr[SIZE]={ 7, 8, 9, 1, 2, 3, 4, 5, 6 }; 
	int i, x, inceput, sfarsit, rezultat;
	int pozitie=0;
	int cautat=6;


    MPI_Init(&argc, &argv); /*START MPI */

    /*Determines the size of the group associated with a communicator */
    MPI_Comm_size(MPI_COMM_WORLD, &nrprocs);

    /*Determines the rank of the calling process in the communicator*/
    MPI_Comm_rank(MPI_COMM_WORLD, &rank);


	MPI_Bcast(arr, SIZE, MPI_INT, 0, MPI_COMM_WORLD);

	// search the number in portion of data 
	x = SIZE/nrprocs; // must be an integer  
	inceput = rank * x;
	sfarsit = inceput + x;
	for(i=inceput; i<sfarsit; i++) {
		if(cautat==arr[i]){
			pozitie=i;
		}
	}


	MPI_Reduce(&poz, &rezultat, 1, MPI_INT, MPI_MAX, 0, MPI_COMM_WORLD);

	if(0 == rank) {
		if(rezultat==0)
		{
			cout<<"Numarul nu a fost gasit!!\n";
		}
		else{
			cout<<"Pozitia maxima "<< rezultat <<"\n";
		}
	}


    MPI_Finalize(); // Exit Mpi
    system("pause");
    return 0;
}
