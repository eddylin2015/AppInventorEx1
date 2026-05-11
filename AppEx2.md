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
       GameScores[1]=result # mark
       if result<100 then
          GameScores[5]+=1  # lose count
   ***
   for i in [1,2,3,4]
      if GameScores[i]>=100
          countOfWin++
      else
          countOfLose+=GameScores[i+4]
   if countOfWin>=4
        Open another Screen screenName winscr 
   if countOfLose>=2
        Open another Screen screenName losescr 
end do
when Game1menu.click do
   if countOfWin>=0
      open Game1 scr
   showmessage("請按次序通關!")
end do
when Game2menu.click do
   if countOfWin>=1
      open Game2 scr
   showmessage("請按次序通關!")
end do
when Game3menu.click do
   if countOfWin>=2
      open Game3 scr
   showmessage("請按次序通關!")
end do
when Game4menu.click do
   if countOfWin>=
      open Game4 scr
   showmessage("請按次序通關!")
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

when Game1.BackPress do
      close screen with value result(0)
end do


when PosenetExtension1.PoseUpdated do
    if not is list empty? list(PosenetExtension1.Nose)
        call Flute.MoveTo((selecct list item in PosenetExtension1.Nose *1.3)[1],Canvas1.Height-60)
end do

When Trash.CollidedWith(other) do
    if other== Flute
        set Trash.y=0
        set Trash.x= random(50...350-50)
         set score+=20
         set ScoreTxt.Text=score
         call Sound_S.Play
         call Sound_S.Play
         call UpdateBar

end do

When Trash2.CollidedWith(other) do

end do

Procedure UpdateBar(score) do

end do
when Clock1.times do
   Trash.Y+=10
   Trash2.Y+=20
   if Trash.Y > canvas1.height-60
       score-=10
   if Trash2.Y > canvas1.height-60
       score-=10
   if score>= 100 || score<0
      close screen with value result(score)
end do
```
## Blocks

### mainscreen

![CodeBlock1](https://github.com/eddylin2015/AppInventorEx1/blob/main/img/mainscrblocks.png?raw=true)

### game1

![CodeBlock2](https://github.com/eddylin2015/AppInventorEx1/blob/main/img/game1blocks.png?raw=true)

## apk


## Conclusion

記錄moonteam近期作品,記錄編程重點.
