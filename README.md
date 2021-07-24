# tweenCFX
Standalone  
But it will be included in the Threads script in the future.

#Example

```
DrawText2D = function(text,x,y,alpha)
	SetTextScale(0.5, 0.5)
	SetTextFont(1)
	SetTextColour(255, 255, 255, alpha)
	SetTextDropshadow(0, 0, 0, 0, 255)
	SetTextDropShadow()
	SetTextOutline()
	SetTextCentre(true)
	BeginTextCommandDisplayText('STRING')
	AddTextComponentSubstringPlayerName(text)
	EndTextCommandDisplayText(x, y)
	ClearDrawOrigin()
end
local testDrawWhile = nil 
local testDrawWhile2 = nil 
function OnDrawFinish(text)
    print(text.." draw finish!")
    testDrawWhile = nil
end 
function OnDrawFinish2(obj,state)
    if state == 2 then 
    print(obj._text.." draw finish!")
    testDrawWhile2 = nil
    else 
    TweenCFX.Tween.to(obj,3.0,{_alpha=0.0,ease=TweenCFX.Ease.EaseTable[1],onCompleteScope=OnDrawFinish2,onCompleteArgs={obj,2}})
    end 
end 
CreateThread(function()
    local object = {}
    object._text = "haha"
    object._x = 0.5
    object._y = 0.0
    object._alpha = 0
    TweenCFX.Tween.to(object,3.0,{_y=0.5,_alpha=255,delay=1,ease=TweenCFX.Ease.LinearNone,onCompleteScope=OnDrawFinish,onCompleteArgs={object._text}})
    local object2 = {}
    object2._text = "haha2"
    object2._x = 0.0
    object2._y = 0.5
    object2._alpha = 255
    TweenCFX.Tween.to(object2,5.0,{_x=0.7,ease=TweenCFX.Ease.EaseTable[4],onCompleteScope=OnDrawFinish2,onCompleteArgs={object2,1}})
    CreateThread(function()
        testDrawWhile = true 
        testDrawWhile2 = true 
        while testDrawWhile or testDrawWhile2 do Wait(0)
            DrawText2D(object._text,object._x,object._y,math.floor(object._alpha))
            DrawText2D(object2._text,object2._x,object2._y,math.floor(object2._alpha))
        end 
    end)
end)
```
