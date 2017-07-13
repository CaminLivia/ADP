#include "mpi.h"
#include <time.h>
#include <iostream>
using namespace std;

#define SIZE 12
#define NR 0

int main(int argc, char *argv[])
{
	int rank, nrProcs, slice, indexVpoz;
	int array[SIZE], segment[SIZE], Vpoz[SIZE], finalFound[SIZE];
	bool display = false;

	srand((unsigned int)time(NULL));

	MPI_Init(&argc, &argv);
	MPI_Comm_rank(MPI_COMM_WORLD, &rank);
	MPI_Comm_size(MPI_COMM_WORLD, &nrProcs);

	slice = SIZE / nrProcs;

	//avem grija ca toate bucatile sa fie egale
	if (SIZE % nrProcs != 0)
		++slice;
	//blocheaza procesul curent pana cand toate celelalte procese din communicator isi termina rutina
	MPI_Barrier(MPI_COMM_WORLD);
	
	//initializeaza array 
	if (rank == 0)
	{
		cout << "Array elements are:\n";
		for (int i = 0; i < SIZE; i++)
		{
			array[i] = rand() % 5;
			cout << array[i] << " ";
			finalFound[i] = -1;
		}
		//cout << "Searched number is: ";
		//cin >> NR;
		//cout << "\n";
	}
	//trimite seg egale de date de la root catre celelalte proc din communicator
	MPI_Scatter(array, slice, MPI_INT, segment, slice, MPI_INT, 0, MPI_COMM_WORLD);
	cout << "\n\nRank: " << rank << ". Segement size: " << slice << "\n";
	//initializare 
	for (int i = 0; i < slice; i++)
		Vpoz[i] = -1;

	indexVpoz = 0;
	for (int i = 0; i < slice; i++)
	{
		if (segment[i] == NR)
		{
			Vpoz[++indexVpoz] = i + rank * slice;
		}
	}
	//reuneste toate pozitiile in vect finalFound prin intermediul Gather
	MPI_Gather(Vpoz, slice, MPI_INT, finalFound, slice, MPI_INT, 0, MPI_COMM_WORLD);

	if (rank == 0)
	{
		for (int i = 0; i < SIZE ; i++)
		{
			if (finalFound[i] >= 0)
			{
				if (!display)
					cout << "\n\nNumber found on the follwing position(s): \n";
				display = true;
				cout << finalFound[i] << " ";
			}
		}
		if (!display)
			cout << "\n\nNumber not found.";
	}
	
	MPI_Finalize();
	cout << endl;
	system("pause");
	return 0;
}
