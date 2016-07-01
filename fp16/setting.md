Q: error: identifier "__hsub_sat" is undefined <br>
A: As for cuda_fp16.h, it gets included from nccl.h (which is in turn included in core.h) whenever CUDART_VERSION >= 7050.
   My cuda_runtime_api.h shows #define CUDART_VERSION  7000 (less than 7050)


https://github.com/NVIDIA/nccl/issues/9
