#include <mpi.h>
#include <stdio.h>

int main(int argc, char **argv)
{
	int rank, size, A, B;
	int periods, newC, dims;
	int sourceB, destB, sourceM, destM;

	MPI_Comm commCart;
	MPI_Status status;

	MPI_Init(&argc, &argv);

	MPI_Comm_size(MPI_COMM_WORLD, &size);
	MPI_Comm_rank(MPI_COMM_WORLD, &rank);

	dims = 0;
	periods = 0;

	MPI_Dims_create(size, 1, dims);
	MPI_Cart_create(MPI_COMM_WORLD, 1, dims, periods, 0, &commCart);
	MPI_Cart_coords(commCart, rank, 1, newC);

	A = newC;
	B = -1;

	if(newC == 0){
		sourceM = destM = MPI_PROC_NULL;
	}
	else{ 
		sourceM = destM = newC - 1;
	}

	if(newC == dims - 1){
		destB = sourceB = MPI_PROC_NULL;
	}
	else{ 
		destB = sourceB = newC + 1;
	}

	MPI_Sendrecv(&A, 1, MPI_INT, destB, 12, &B, 1, MPI_INT, sourceM, 12, commCart, &status);
	printf ("newC = %d В = %d\n", newC , B);

	MPI_Sendrecv(&A, 1, MPI_INT, destM, 12, &B, 1, MPI_INT, sourceB, 12, commCart, &status);
	printf("newC = %d В = %d\n", newC, B);

	MPI_Comm_free(&commCart);
	MPI_Finalize();
	return 0;
}
