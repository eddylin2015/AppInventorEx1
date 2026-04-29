# AppInventor Ex 1 

## Main Interface

![主介面](https://github.com/eddylin2015/AppInventorEx1/blob/main/img/design.png?raw=true)

## Debug ISO / Android with wifi link

## Build Apk for Android

## Code

```js
/************
* Globle Varibles
*************/
time =0  # 故事主綫累計器
page1=0  # 頁Page1累計器
page2=0  # 頁Page2累計器
page3=0  # 頁Page3累計器
page4=0  # 頁Page4累計器
page5=0  # 頁Page5累計器
page6=0  # 頁Page6累計器
page7=0  # 頁Page7累計器
page8=0  # 頁Page8累計器
page9=0  # 頁Page9累計器
SO=0     # Pause 1 , Play 0
CurrPM3="1.mp3" # Current MP3 file

/****
 * 設置初始狀態, 
 * SetTimeVal:設定主計時 -1 IGNORE
 * */
function initVariables(SetTimeVal=-1){
    if SetTimeVal>-1
       time=SetTimeVal
    page[1-9]=0
    Clock1.enble=false 
    Clock_page[1-9].enble=false
    Sound_Stop()
}
/*****
 * 主計時:換頁功能
 * inerval=2000
 */
Clock1.Timer(){
    if time<=8
        time++
    else
        time=9    
    HA1.image=f"{time}.png" # 換頁
    Clock1.enable=false     # 暫停主綫播放
    if time==1
       Clock_page1.enable=true # 第一頁播放
    else if time==2
       Clock_page2.enable=true # 第二頁播放
    else if time==3
       Clock_page3.enable=true # 第三頁播放
}
/***
 * PageX 計時控制器 
 * inerval=2000
 * x:Page_idx 第几頁
 * y:MaxNum   最大累計數之后,停止播放, 啟動主綫換下一頁。
 */
function PgaeX(x,y){
   if GetPageCnt(x)<=y
      IncPageCnt(x)
    else
      initVariables(x)     # 設主綫計數器time 設為x, 全局變數Page清零, 音效停止.
      TextBox1.Text=""     # 字幕清空
      Clock1.enable=true   # 啟動主綫換下一頁
      SetPageTimer(x,false)# 當前頁面支綫停止
}
/***
 * 支綫頁面播放畫面1: 字幕及MP3
 */ 
function Clock_page1.Timer()
{
    PgaeX(1,17)          # 頁面1, 17秒, 計數器Page1++
    Temp=GetPageCnt(1)   # 取得計數器Page1值
    if Temp==1:          
       PlayMP3("1.mp3","On a sunny hill")
    else if Temp==5
       TextBox1.Text="Her patched."
    else if Temp==8
       TextBox1.Text="....."
}
/***
 * 開始鍵
 */ 
function StartBtn(){
    VA2.visible=false
    VA1.Visible=true
    initVariable(0)
    Clock1.enable=true
}
/***
 * 下一頁鍵
 */ 
function PlayNext(){
    if time<9
      initVariable(time)
      HA1.image=f"{time}.png"
      Clock1.enable=true
}
/***
 * 上一頁鍵
 */ 
function PlayPrev(){
    if time>1
      time-=2
      initVariable(time)
      HA1.image=f"{time}.png"
      Clock1.enable=true
}
/***
 * 暫停鍵
 */ 
function PauseAndPlay(){
    SO++
    if SO % 2==1
        BTN_SO.image="SO2.png"
        PauseMP3(CurrPM3)
        SetPageTimer(time，false)
    else
        BTN_SO.image="SO1.png"
        PlayMP3(CurrPM3，"None")
        SetPageTimer(time，true)
}
/***
 * 重置鍵
 */ 
function ResetAndPlay(){
    initVariables(0)
    VA1.visible=false
    VA2.image="0.jpg"
    VA2.visible=true
}
/**
 * Pause MP3
 * ref: Curr_PM3 
 */ 
function PauseMP3(mp3_){/*code here*/}
/*
** 播放加字幕
**/
function PlayMP3(mp3_,message){/*code here*/}
/*
*
**/
function SetPageTimer(PageTimer_idx,on_off){/*code here*/}
/**
*
**/
function StopAllSound(){/*code here*/}
/*
 ***/
function StopAllTimer(){/*code here*/}
/**
*
**/
function SetAllPageCnt(val=0){/*code here*/}
/**
*
**/
function SetPageCnt(PageCnt_idx,val=0){/*code here*/}
/**
*
**/
function IncPageCnt(PageCnt_idx){/*code here*/}
/**
*
**/
function GetPageCnt(PageCnt_idx){/*code here*/}
```

## Flowchart

![CodeBlock1](https://github.com/eddylin2015/AppInventorEx1/blob/main/img/CodeBlock1.png?raw=true)

![CodeBlock2](https://github.com/eddylin2015/AppInventorEx1/blob/main/img/CodeBlock2.png?raw=true)

## Conclusion

滿意!
