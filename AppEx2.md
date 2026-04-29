# AppInventor Ex 2 
## Draft

![Draft](https://github.com/eddylin2015/AppInventorEx1/blob/main/img/Ex2Draft01.png?raw=true)

## Main Interface

![主介面](https://github.com/eddylin2015/AppInventorEx1/blob/main/img/F6APROJ260429.png?raw=true)

### 場景之間切換及數據交換

* startscreen
* introduct
* loading
* screen3(main menu）
* game1              
  PoseNetExtension https://mit-cml.github.io/extensions/
* game2
* game3
* game4
* winsrc
* losesrc
  
```js
/************
* main menu (screen3)
* Globle Varibles
*************/
GameScores=[0,0,0,0,0,0,0,0]
countOfWin=0
countOfLose=0

Open another Screen With start value screenName Game1    
                                     startValue 1   

when Screen3 OtherScreenClosed(otherScreenName,result) do
   if otherScreenName=='Game1' then
       GameScores[1]=result
       if result<100 then
          GameScores[5]+=1
   if countOfWin>=4
        Open another Screen screenName winscr 
   if countOfLose>=2
        Open another Screen screenName losescr 
end do
```
```js
/************
* Game1
* Globle Varibles
*************/
global PosenetExtension1
global Trash,Trash2,Flute
global scrStartValue,score=0

when Game1.initalize do
    set scrStartValue=Get_Start_Value
    set PosenetExtension1.Enabled=true
    set Clock1.TimerEnabled=true
end do

when PosenetExtension1.PoseUpdated do

end do

When Trash.CollidedWith(other) do

end do
When Trash2.CollidedWith(other) do

end do

when Clock1.times do
   if score>= 100 || score<0
      close screen with value result(score)
end do
```
## Blocks

### mainscreen

![CodeBlock1](https://github.com/eddylin2015/AppInventorEx1/blob/main/img/mainscrblocks.png?raw=true)

### game1

![CodeBlock2](https://github.com/eddylin2015/AppInventorEx1/blob/main/img/game1blocks.png?raw=true)

## Conclusion

記錄moonteam近期作品.
