"# AppInventorEx1" 

![主介面](https://github.com/eddylin2015/AppInventorEx1/blob/main/img/design.png?raw=true)

```js
/************
* Globle Varibles
*************/
time =0
page1=0
page2=0
page3=0
page4=0
page5=0
page6=0
page7=0
page8=0
page9=0
SO=0
CurrPM3=1.mp3

function initVariables(SetTimeVal=-1){
    if(SetTimeVal>-1)
       time=SetTimeVal;
    page[1-9]=0;
    Clock1.enble=false ;
    Clock_page[1-9].enble=false;
    Sound_Stop();
}
Clock1.Timer(inerval=2000){
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
function PgaeX(x,y){
   if GetPageCnt(x)<=y
      IncPageCnt(x)
    else
      initVariables(x)
      TextBox1.Text=""
      Clock1.enable=true
      SetPageTimer(x,false)
}
function Clock_page1.Timer()
{
    PgaeX(1,17)
    Temp=GetPageCnt(1)
    if Temp==1:
       PlayMP3("1.mp3","On a sunny hill,")
    else if Temp==5
       TextBox1.Text="Her patched."
}
```

![CodeBlock1](https://github.com/eddylin2015/AppInventorEx1/blob/main/img/CodeBlock1.png?raw=true)

![CodeBlock2](https://github.com/eddylin2015/AppInventorEx1/blob/main/img/CodeBlock2.png?raw=true)

