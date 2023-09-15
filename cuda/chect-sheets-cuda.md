# 参考教材
[《CUDA 编程基础与实践》](D:\OneDrive\Books\CUDA编程基础与实践.pdf)

# CUDA基本概念

# CUDA编程

## Examples

### MatrixMul
```cuda
#include <cstddef>
#include <cstdlib>
#include <iostream>
#include <cuda_runtime.h>

using namespace std;

const size_t M = 512;
const size_t N = 512;
const size_t K = 512;

__global__ void matrixmul(int *a, int *b, int *c, int m, int n, int k) {
    int row = blockIdx.x * blockDim.x + threadIdx.x;
    int col = blockIdx.y * blockDim.y + threadIdx.y;
    if (row < m && col < k) {
        int sum = 0;
        for (int i = 0; i < n; ++i) {
            sum += a[row * n + i] * b[i * n + col];
        }
        c[row * n + col] = sum;
    }
}

void naiveMatrixOp(int *a, int *b, int *c, int m, int n, int k) {
    for (int row = 0 ; row < m; ++row) {
        for (int col = 0; col < k; ++col) {
            int sum = 0;
            for (int i = 0; i < n; ++i) {
                sum += a[row * n + i] * b[i * n + col];
            }
            c[row * n + col] = sum;
        }
    }
}

int main() {
    int *ha, *hb, *hc;
    ha = (int*)malloc(M * N * sizeof(int));
    hb = (int*)malloc(N * K * sizeof(int));
    hc = (int*)malloc(M * K * sizeof(int));
    srand(0);
    for (int i = 0; i < M * N; ++i) {
        ha[i] = rand() % 100;
    }
    for (int i = 0; i < N * K; ++i) {
        hb[i] = rand() % 100;
    }

    int *da, *db, *dc;
    cudaMalloc((void **)&da, M * N * sizeof(int));
    cudaMalloc((void **)&db, N * K * sizeof(int));
    cudaMalloc((void **)&dc, M * K * sizeof(int));

    cudaMemcpy(da, ha, M * N * sizeof(int), cudaMemcpyHostToDevice);
    cudaMemcpy(db, hb, N * K * sizeof(int), cudaMemcpyHostToDevice);

    dim3 blockDim(16, 16);
    dim3 gridDim((N + blockDim.x - 1) / blockDim.x, (N + blockDim.y - 1) / blockDim.y);

    matrixmul<<<gridDim, blockDim>>>(da, db, dc, M, N, K);

    cudaMemcpy(hc, dc, M * K * sizeof(int), cudaMemcpyDeviceToHost);

    int *ground_truth = (int *)malloc(M * K * sizeof(int));
    naiveMatrixOp(ha, hb, ground_truth, M, N, K);
    for (int i = 0; i < M * K; ++i) {
        if (ground_truth[i] != hc[i]) {
            cout << "Error" << endl;
            return 0;
        }
    }
    cout << "Good" << endl;

    // 释放 GPU 和主机内存
    cudaFree(d_a);
    cudaFree(d_b);
    cudaFree(d_c);
    free(h_a);
    free(h_b);
    free(h_c);

    return 0;
}

```
