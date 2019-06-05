# Homework6 - Match Moving SLAM
## Our video（5%）
第一部：https://www.youtube.com/watch?v=NTvBQIbW6SA&feature=youtu.be

第二部：https://www.youtube.com/watch?v=t_wiQIOmccY&feature=youtu.be
## AR effect with ORB-SLAM2
### Result
#### Image（10%）
將Pikachu的圖片放到書桌上:  
![](output_image.gif)  
#### 3D Model（5%）
將一個茶壺放到書桌上:  
![](output_video.gif)  
原本影片和SLAM結果:  
![](output.gif)
#### Mark
嘗試利用特殊標記增加穩定性，但標記無法提供足夠特徵點維持SLAM運作:  
![](output_marker.gif)  

### Method  
我們使用ORB_SLAM2範例中中TUM的Monocular版本加上ROS的AR範例，作為實作3D model AR特效的基礎，加上手動微調model位置與使用客製化model的功能。由於Pangolin僅能顯示預設的彩設方塊，因此加入其它3D model基本上必須要用OpenGL加入整個pipline。並由於其使用的OpenGL為舊版的，實作上需要特別去查舊版語法，特別費了一番功夫。SLAM的部分直接使用ORB_SLAM2的範例，影片切成與TUM相同大小，直接使用TUM的camera calibration參數，並無另外矯正。

## Special Effects Based On the Pose Information（10%）
這裡我們根據相機和model的位置算出它們之間的距離，並根據距離的遠近改變顏色。  
![](output_color.gif)

## AR effect with post-production software（10%）
運用AE的3D track camera effect來追蹤camera位置，並在場景中加上Pikachu的圖片。
在此部分，我們利用After Effect CC這個後製軟體來對我們的第二部影片進行後製，我們是參考以下這部影片來做到3D track effect的效果的
連結：https://www.youtube.com/watch?v=t6hgmRZZ4WE&fbclid=IwAR0viDbbr6cHeuIDEZvv8pUrx8CXnp3iQxAnNtzA4n_uCgFjId-a244jcIo

而第二部影片經過AE所做出來的結果影片為以下連結：https://www.youtube.com/watch?v=qSIBZtAg_Ss&feature=youtu.be

而在後製軟體我們所增加的Visual effects為了要和ORB-SLAM2這個方法做比較，一樣都是把Pikachu的圖片放到書桌上
## Comparison and Disccusion（10%）

* ORB_SLAM2由於使用許多third party libraries，安裝上非常容易出錯，需要花費大量時間搞定環境問題。
* ORB-SLAM2結果影片的部分可以看到，當桌子空白的區塊站畫面比例太大或是角度太大時，效果會明顯變差，造成虛擬model稍微滑動，但其它情況效果還不錯。
* 觀察利用ORB SLAM做出的影片，我們發現到不管是2D圖片或是3D model尤其是3D model會有上下左右抖動，類似拍照手抖的問題。推測是由於程式所用的相機參數和實際使用的參數有誤差的緣故。然而用AE後製出來的影片，圖片位置相對穩定，較沒有抖動的感覺。

Visual Effect這個後製軟體則有以下優缺點：

* 有UI介面提供給使用者使用，並且可以自動追蹤影片的特徵點，並且產生Camera移動的軌跡
* 從以上影片後製的結果，可以看出所加上的圖案相對擬真，ORB_SLAM2會有浮在空中的感覺
* Visual Effect這個後製軟體的最大缺點在於需要付費才能使用，而且價格不菲。
兩個做法再加上mark以後都有讓效果更好的趨勢，在AE上增加了mark讓軟體可以有更明確的track point使圖片可以更完美的浮貼在桌面，而兩個做法都沒有加上影子，

綜上所述，兩個方法做出的效果大致上差不多，就是ORB SLAM的結果會稍稍受相機參數的誤差影響。而在沒有影子這個幫助判斷深度的提示下，人會因為視差，覺得前面的物體該動的較多的想法，對同一部影片會有不同感覺。
