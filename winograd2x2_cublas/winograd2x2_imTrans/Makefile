TF_INC=/usr/local/lib/python2.7/dist-packages/tensorflow/include
LD_LIBRARY_PATH=/usr/local/cuda/lib64
TF_LIB=/usr/local/lib/python2.7/dist-packages/tensorflow

all: winograd2x2_imTrans_op.so winograd2x2_imTrans_grad_op.so

forward: winograd2x2_imTrans_op.so

backward: winograd2x2_imTrans_grad_op.so

winograd2x2_imTrans_op.so: winograd2x2_imTrans_op.cc winograd2x2_imTrans_cuda.cu.o
	g++ -std=c++11 -shared -o winograd2x2_imTrans_op.so winograd2x2_imTrans_op.cc winograd2x2_imTrans_cuda.cu.o -I $(TF_INC) -I $(TF_INC)/external/nsync/public -fPIC -L$(LD_LIBRARY_PATH) -L$(TF_LIB) -lcudart -O2 -ltensorflow_framework

winograd2x2_imTrans_cuda.cu.o: winograd2x2_imTrans_cuda.cu.cc
	nvcc -std=c++11 -c -o winograd2x2_imTrans_cuda.cu.o winograd2x2_imTrans_cuda.cu.cc -I $(TF_INC) -I $(TF_INC)/external/nsync/public -D GOOGLE_CUDA=1 -x cu -Xcompiler -fPIC -arch sm_61 -ltensorflow_framework # --use_fast_math
		
winograd2x2_imTrans_grad_op.so: winograd2x2_imTrans_grad_op.cc winograd2x2_imTrans_grad_cuda.cu.o
	g++ -std=c++11 -shared -o winograd2x2_imTrans_grad_op.so winograd2x2_imTrans_grad_op.cc winograd2x2_imTrans_grad_cuda.cu.o -I $(TF_INC) -I $(TF_INC)/external/nsync/public -fPIC -L$(LD_LIBRARY_PATH) -L$(TF_LIB) -lcudart -O2 -ltensorflow_framework

winograd2x2_imTrans_grad_cuda.cu.o: winograd2x2_imTrans_grad_cuda.cu.cc
	nvcc -std=c++11 -c -o winograd2x2_imTrans_grad_cuda.cu.o winograd2x2_imTrans_grad_cuda.cu.cc -I $(TF_INC) -I $(TF_INC)/external/nsync/public -D GOOGLE_CUDA=1 -x cu -Xcompiler -fPIC -arch sm_61 -ltensorflow_framework # --use_fast_math
	
clean:
	rm *.o *.so
