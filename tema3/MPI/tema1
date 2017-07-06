#include "mpi.h"
#include <iostream>
#include <math.h>
using namespace std;

#define N 240
#define FirstRank 0 /* Rankul primului proces*/

int isprime(int n) {
    int i,squareroot;
    if (n>10) {
		squareroot =  (int) sqrt(n);
		for (i=3; i<=squareroot; i=i+2)
			if ((n%i)==0)
            return 0;
		return 1;
	}
	else
		return 0;
}

int main (int argc, char *argv[])
{
	int Mtasks; /* numar total procese */
	int rank; /* identificatorul procesului*/
	int n;
	int foundone; 
	int maxprime; /* cel mai mare nr prim gasit */
	int mystart; /* incepe calculul */
	int stride; /* calculeaza fiecare nr;pasul */
	int pc; /*numarator */
	int pcsum; /* numarul de nr prime gasit de procese*/

	double start_time,end_time;

MPI_Init(&argc,&argv);

MPI_Comm_rank(MPI_COMM_WORLD,&rank); //obtinere rank procesc curent

MPI_Comm_size(MPI_COMM_WORLD,&Mtasks); //marimea comunicatorului


  //verificare daca N se imparte la numarul de procese
	if (((Mtasks%2) !=0) || ((N%Mtasks) !=0)) {
		cout<<"Sorry - this exercise requires an even number of tasks.\n";

		MPI_Finalize();
		exit(0);
	}

start_time = MPI_Wtime(); /* Initializeaza start time, timpul scurs de cand a fost apelat procesorul */

mystart = (rank*2)+1; /* Gaseste punctul de inceput -trebuie sa fie un nr impar */

stride = Mtasks*2; /* Determina pasul si sare peste nr pare*/

pc=0; /* Initializeaza numaratorul */

foundone = 0; /* Initializare */

/******************** task with rank 0 does this part ********************/
	if (rank == FirstRank) {
		cout<<"Using"<<Mtasks<<"tasks to scan"<<N<<"numbers";
		pc = 4; /* Assume FirstRank four primes are counted here */
			for (n=mystart; n<=N; n=n+stride) {
				if (isprime(n)) {
					pc++;
					foundone = n;

				cout<<foundone<<endl;

				}
			}

MPI_Reduce(&pc,&pcsum,1,MPI_INT,MPI_SUM,FirstRank,MPI_COMM_WORLD);

MPI_Reduce(&foundone,&maxprime,1,MPI_INT,MPI_MAX,FirstRank,MPI_COMM_WORLD);

end_time=MPI_Wtime();

cout<<"Done. Largest prime is<<maxprime<<Total primes"<<pcsum;

cout<<"Wallclock time elapsed: "<<end_time-start_time<<"seconds";
	}


	/******************** all other tasks do this part ***********************/
	if (rank > FirstRank) {
		for (n=mystart; n<=N; n=n+stride) {
			if (isprime(n)) {
				pc++;
				foundone = n;

			cout<<foundone<<"by process" <<rank<<endl;



			}
		}


MPI_Reduce(&pc,&pcsum,1,MPI_INT,MPI_SUM,FirstRank,MPI_COMM_WORLD);

MPI_Reduce(&foundone,&maxprime,1,MPI_INT,MPI_MAX,FirstRank,MPI_COMM_WORLD);

	}


	MPI_Finalize();
}
