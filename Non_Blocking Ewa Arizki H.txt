#include <stdio.h>
#include <stdlib.h>
#include <mpi.h>

int main(int argc, char** argv) {
  // Inisiasi Environment Awal
  MPI_Init(NULL, NULL);
  
  //Mencari Rank dan Size 
  int posisi;
  MPI_Comm_rank(MPI_COMM_WORLD,&posisi);
  int ukuraan;
  MPI_Comm_size(MPI_COMM_WORLD,&ukuraan);
  MPI_Request m;
  // Menggunakan 2 Processor
  if (ukuraan < 2) {
    fprintf(stderr, "Ukuraan harus lebih besar dari 1 untuk  %s\n", argv[0]);
    MPI_Abort(MPI_COMM_WORLD, 1);
  }

  int u;
  
  if (posisi == 0) {
    u= -1;
    MPI_Isend(&u, 1, MPI_INT, 1,0,MPI_COMM_WORLD,&m);
  } else if (world_rank == 1) {
    MPI_Recv(&number, 1, MPI_INT, 0, 0, MPI_COMM_WORLD, MPI_STATUS_IGNORE);
    printf("Process 1 received number %d from process 0\n", number);
  }
  
  MPI_Finalize();	
}