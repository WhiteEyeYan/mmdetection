# mmskeleton

參考https://blog.csdn.net/weixin_43390800/article/details/109838293 先安裝 mmdetection
安裝mmdetection 參考https://zhuanlan.zhihu.com/p/159912450
其中mmdetection並未修改程式碼直接安裝mmdetection
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
