# mmdetection

為了安裝mmskeleton
參考https://blog.csdn.net/weixin_43390800/article/details/109838293 先安裝 mmdetection
安裝mmdetection 參考https://zhuanlan.zhihu.com/p/159912450
其中mmdetection並未修改程式碼直接安裝mmdetection
<br>
<br>
在conda環境下建構失敗 一直找不到的.lib 在一般cmd下使用
>pip install -v -e .

也失敗
最後使用
>python setup.py develop

成功~
<br>
<br>
問題
>UserWarning: Error checking compiler version for cl

cmd輸入cl
>'cl' 不是內部或外部命令、可執行的程式或批次檔
<br>
<br>
<br>
解決方式

cl為VS內的東西 找到VS安裝路徑C:\Program Files (x86)\Microsoft Visual Studio\2017\Community
直接搜尋cl.exe
最後cl.exe位置在
>C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\VC\Tools\MSVC\14.16.27023\bin\Hostx64\x64

將此路徑加入環境變量path中
<br>
<br>
<br>
問題
>subprocess.CalledProcessError: Command '['ninja', '-v']' returned non-zero exit status 1.

後來發現我還沒安裝ninja
    
    
至ninja github下載 https://github.com/ninja-build/ninja
解壓縮後cd至ninja-master目錄下
使用
>python configure.py --bootstrap

>cmake -Bbuild-cmake -H.

皆失敗
<br>
<br>
使用
>cmake --build build-cmake

安裝成功
至cmd輸入 ninja有成功顯示
<br>
<br>
<br>
問題
>subprocess.CalledProcessError: Command '['ninja', '-v']' returned non-zero exit status 1.

似乎是因為沒有此指令 直接在cmd執行 ninja -v也是錯誤 該指令似乎是mmdetection安裝時要檢查版本
查看ninja版本的指令
>ninja --version

所以修改cpp_extension.py
該文件在torch的目錄下
我使用conda下載 目錄在
>C:\Users\WhiteEyeYan\anaconda3\envs\open-mmlab\Lib\site-packages\torch\utils\cpp_extension.py

修改cpp_extension.py第1496行
>command = ['ninja', '-v']

改為
>command = ['ninja', '--version']
<br>
<br>
<br>

問題

>LINK : fatal error LNK1181: 無法開啟輸入檔 'cudart.lib'

先執行一次
>python stepup.py build_ext --library-dirs C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v11.0/lib/x64

再執行
>python stepup.py develop

設定環境變數 path新增cuda lib的所在位置
>C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.1\lib\x64


https://wiki.hackzine.org/development/python/library-in-custom-path.html


問題
>fatal error C1083: 無法開啟包含檔案: 'cuda_runtime_api.h': No such file or directory

開啟mmdet\ops\utils\src\compiling_info.cpp 
>#include <cuda_runtime_api.h>

更改為cuda_runtime_api.h所在的路徑
>#include <C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.1\include\cuda_runtime_api.h>


問題
>No CUDA runtime is found

明明就有安裝CUDA也有搜尋到路徑 不知道為甚麼會這樣
後來重裝torch 用pytorch官網的pip指令下載後正常

問題
>KeyError: 'ConvWS is already registered in conv layer'

參考https://blog.csdn.net/weixin_40755306/article/details/113666002
至D:\WhiteEyeYan\Desktop\mmdetection-2.1.0\mmdet\ops\conv_ws.py
>@CONV_LAYERS.register_module('ConvWS')

改為
>@CONV_LAYERS.register_module(name='ConvWS', force=True)



>AttributeError: module 'pycocotools' has no attribute '__version__'
>pip uninstall pycocotools
>pip install mmpycocotools
