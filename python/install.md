Q: importError: No module named numpy  
A:  export PATH="/opt/anaconda2/bin:$PATH"

Q: ImportError: No module named easydict  
A: conda install -c auto easydict=1.4  

Q: ImportError: No module named _caffe  
A: make pycaffe; export PYTHONPATH={Path2yourCaffe}/caffe/python:$PYTHONPATH
  
  ref https://github.com/BVLC/caffe/issues/782
  #for error 'module' object has no attribute 'bool_'
  import sys
  sys.path.insert(0,'/N/software/3DOP_code/frcn-kitti/caffe-master/python')
  import caffe
  sys.path.insert(0,'/N/software/3DOP_code/frcn-kitti/caffe-master/python/caffe')
  import _caffe

