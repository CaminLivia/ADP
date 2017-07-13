#include <iostream>
#include <mpi.h>
#include <stdlib.h>
#include <time.h>
using namespace std;



int main(int argc, char *argv[]){
	int numprocs, procid, j, s, M, nr,i;
	double startTime, endTime;


	MPI_Init(&argc, &argv);

	MPI_Comm_size(MPI_COMM_WORLD, &numprocs);
	MPI_Comm_rank(MPI_COMM_WORLD, &procid);

	startTime = MPI_Wtime();
	s = 0;
	srand(static_cast<unsigned int>(time(NULL)) + procid*numprocs);
	M = rand() % 901 + 100;
	cout << "Hello from proc " << procid << "!Started procs " << numprocs << "!\n";
	cout << "Proc " << procid << " generates " << M << " numbers: \n";

	for (j = 0; j < M; j++){
			nr = rand() % 10;
			cout << nr << " ";
			s = s + nr;
	}
	cout << "\n";
	cout << "Proc " << procid << " sum=" << s << "\n";
	endTime = MPI_Wtime();
	cout << "Proc " << procid << " took " << endTime - startTime << " seconds to do the job.\n";
	MPI_Finalize();
	return 0;
}
