# Homework6 - Match Moving SLAM

## AR effect with ORB-SLAM2
### Result
#### Image
將Pikachu的圖片放到書桌上:  
![](output_image.gif)  
#### 3D Model
將一個茶壺放到書桌上:  
![](output_video.gif)  
原本影片和SLAM結果:  
![](output.gif)
#### Mark
嘗試利用特殊標記增加穩定性，但標記無法提供足夠特徵點維持SLAM運作:  
![](output_marker.gif)  

### Method  
我們使用ORB_SLAM2範例中中TUM的Monocular版本加上ROS的AR範例，作為實作3D model AR特效的基礎，加上手動微調model位置與使用客製化model的功能。由於Pangolin僅能顯示預設的彩設方塊，因此加入其它3D model基本上必須要用OpenGL加入整個pipline。並由於其使用的OpenGL為舊版的，實作上需要特別去查舊版語法，特別費了一番功夫。SLAM的部分直接使用ORB_SLAM2的範例，影片切成與TUM相同大小，直接使用TUM的camera calibration參數，並無另外矯正。

## Special Effects Based On the Pose Information
這裡我們根據相機和model的位置算出它們之間的距離，並根據距離的遠近改變顏色。  
![](output_color.gif)

## AR effect with post-production software

## Comparison and Disccusion

* ORB_SLAM2由於使用許多third party libraries，安裝上非常容易出錯，需要花費大量時間搞定環境問題。
* ORB-SLAM2結果影片的部分可以看到，當桌子空白的區塊站畫面比例太大或是角度太大時，效果會明顯變差，造成虛擬model稍微滑動，但其它情況效果還不錯。
