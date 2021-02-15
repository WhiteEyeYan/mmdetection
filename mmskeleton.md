#mmskeleton

問題
>error C2664: 'void _nms(int *,int *,const float *,int,int,float,int)': 無法將引數 1 從 '__pyx_t_5numpy_int32_t *' 轉換為 'int *'

修改mmskeleton-master\mmskeleton\ops\nms\gpu_nms.cpp第2216行
>_nms((&(*__Pyx_BufPtrStrided1d(__pyx_t_5numpy_int32_t *, __pyx_pybuffernd_keep.rcbuffer->pybuffer.buf, __pyx_t_10, __pyx_pybuffernd_keep.diminfo[0].strides))), (&__pyx_v_num_out), (&(*__Pyx_BufPtrStrided2d(__pyx_t_5numpy_float32_t *, __pyx_pybuffernd_sorted_dets.rcbuffer->pybuffer.buf, __pyx_t_12, __pyx_pybuffernd_sorted_dets.diminfo[0].strides, __pyx_t_13, __pyx_pybuffernd_sorted_dets.diminfo[1].strides))), __pyx_v_boxes_num, __pyx_v_boxes_dim, __pyx_t_14, __pyx_v_device_id);

改為
>_nms((&(*__Pyx_BufPtrStrided1d(int *, __pyx_pybuffernd_keep.rcbuffer->pybuffer.buf, __pyx_t_10, __pyx_pybuffernd_keep.diminfo[0].strides))), (&__pyx_v_num_out), (&(*__Pyx_BufPtrStrided2d(__pyx_t_5numpy_float32_t *, __pyx_pybuffernd_sorted_dets.rcbuffer ->pybuffer.buf, __pyx_t_12, __pyx_pybuffernd_sorted_dets.diminfo[0].strides, __pyx_t_13, __pyx_pybuffernd_sorted_dets.diminfo[1].strides))), __pyx_v_boxes_num, __pyx_v_boxes_dim, __pyx_t_14, __pyx_v_device_id);


參考
https://www.codenong.com/cs106400215/


>AttributeError: module 'pycocotools' has no attribute '__version__'

解決方式
>pip install mmpycocotools

若無解決 則重裝
>pip uninstall mmpycocotools
>pip install mmpycocotools


>TypeError: __init__() got an unexpected keyword argument 'num_stages'
