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
time =0  # 主計時
page1=0  # Page1計時
page2=0
page3=0
page4=0
page5=0
page6=0
page7=0
page8=0
page9=0
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
 * 主計時 
 * inerval=2000
 */
Clock1.Timer(){
    if time<=8
        time++
    else
        time=9
    HA1.image=f"{time}.png"
    Clock1.enable=false
    if time==1
       Clock_page1.enable=true
    else if time==2
       Clock_page2.enable=true
    else if time==3
       Clock_page3.enable=true
}
/***
 * Page計時控制器 
 * inerval=2000
 * x:Page_idx
 * y:MaxNum
 */
function PgaeX(x,y){
   if GetPageCnt(x)<=y
      IncPageCnt(x)
    else
      initVariables(x)
      TextBox1.Text=""
      Clock1.enable=true
      SetPageTimer(x,false)
}
/***
 * 畫面1 字幕及MP3
 */ 
function Clock_page1.Timer()
{
    PgaeX(1,17)
    Temp=GetPageCnt(1)
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
 * Next鍵
 */ 
function PlayNext(){
    if time<9
      initVariable(time)
      HA1.image=f"{time}.png"
      Clock1.enable=true
}
/***
 * 返回鍵
 */ 
function PlayPrev(){
    if time>1
      time-=2
      initVariable(time)
      HA1.image=f"{time}.png"
      Clock1.enable=true
}
/***
 * Pause鍵
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
 * Reset鍵
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
function PlayMP3(mp3_,message){/*code here*/}
function SetPageTimer(PageTimer_idx,on_off){/*code here*/}
function StopAllSound(){/*code here*/}
function StopAllTimer(){/*code here*/}
function SetAllPageCnt(val=0){/*code here*/}
function SetPageCnt(PageCnt_idx,val=0){/*code here*/}
function IncPageCnt(PageCnt_idx){/*code here*/}
function GetPageCnt(PageCnt_idx){/*code here*/}
```

## Flowchart

![CodeBlock1](https://github.com/eddylin2015/AppInventorEx1/blob/main/img/CodeBlock1.png?raw=true)

![CodeBlock2](https://github.com/eddylin2015/AppInventorEx1/blob/main/img/CodeBlock2.png?raw=true)

## Conclusion

滿意!