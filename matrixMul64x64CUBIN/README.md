This is an example for cublas 64x64 sass kernel. We extract specific kernel sass, and modify some parameter address, then use the miniPascalAs to insert sass code into the cubin files. It works.

1. Compile cu file to cubin file
	
	nvcc -arch=compute_61 -code=sm_61 matrix_kernel.cu -cubin -o matrix_kernel.cubin

2. Using maxas.pl -e ...(or cuobjdump --dump -func func_name cublas.so > maxwell_sgemm_64x64_raggedMn_nt_maxas.sass) to generate maxwell_sgemm_64x64_raggedMn_nt_maxas.sass

3. Using maxas.pl -i to insert cublas.sass to cubin
	
	maxas.pl -i maxwell_sgemm_64x64_raggedMn_nt_maxas.sass matrix_kernel.cubin cublas64x64.cubin

4. Make build dir and compile the code
	
	make build; cd build; cmake ..; make
