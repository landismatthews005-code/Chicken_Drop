# Chicken_Drop

--game where animals fall from top player clicks
--before hit the bottom
--game ends when animal hits bottom

function love.load()
  chickenFace = love.graphics.newImage("sprites/Chicken.png")
  backgroundImage = love.graphics.newImage("sprites/grass.png")
  powerUp = love.graphics.newImage ("sprites/powerUp.png")
   randX = math.random(love.graphics.getWidth()-powerUp:getWidth()) randY = math.random(love.graphics.getHeight()-powerUp:getHeight())
  math.randomseed(os.time())
  math.random(); math.random(); math.random()
  startx = {math.random(0, love.graphics.getWidth() - chickenFace:getWidth()), 
            math.random(0, love.graphics.getWidth() - chickenFace:getWidth()),  
            math.random(0, love.graphics.getWidth() - chickenFace:getWidth()),  
            math.random(0, love.graphics.getWidth() - chickenFace:getWidth()), 
            math.random(0, love.graphics.getWidth() - chickenFace:getWidth())}
  starty = {0 - math.random(chickenFace:getHeight(), chickenFace:getHeight() * 2),
            0 - math.random(chickenFace:getHeight(), chickenFace:getHeight() * 2),
            0 - math.random(chickenFace:getHeight(), chickenFace:getHeight() * 2),
            0 - math.random(chickenFace:getHeight(), chickenFace:getHeight() * 2),
            0 - math.random(chickenFace:getHeight(), chickenFace:getHeight() * 2)}
        
end

-------------------------------------------------
--MOUSE PRESS
--1 = left, 2 = right, 3 = middle wheel
-------------------------------------------------
function love.mousepressed(x, y, button, istouch, dt)
  if button == 1 then
    --print("left mouse clicked")
    for i, v in ipairs(startx) do
      --if the mouse x and y is within the boundary of a chicken picture
      if x >= startx[i] and x <= startx[i] + chickenFace:getWidth() and y >= starty[i] and y <= starty[i] + chickenFace:getHeight() then
        --print("in bounds")
        math.randomseed(os.time())
        math.random(); math.random(); math.random()
        --reset its y value (go back to the top)
        starty[i] = math.random(chickenFace:getHeight(), chickenFace:getHeight() * 2) * -1
  
      end
       if x >= randX and x <= randX + powerUp:getWidth() and y >= randY and y <= randY + powerUp:getHeight() then
        --print("in bounds")
        math.randomseed(os.time())
        math.random(); math.random(); math.random()
        --reset its y value (go back to the top)
        randX = math.random(love.graphics.getWidth()-powerUp:getWidth()) randY = math.random(love.graphics.getHeight()-powerUp:getHeight())
        starty[i] = starty[i] + -80 *dt
       
      end
    end
  end
end

-------------------------------------------------
--UPDATE
-------------------------------------------------
function love.update(dt)
 
  --love.graphics.draw(powerUp, randX, randY, 0, 1, 1 )
  for i, v in ipairs(starty) do
    --if chicken hits the bottom of the screen, lua quits (we lose)
    if starty[i] + chickenFace:getHeight() >= love.graphics.getHeight() then
      --print("over the edge")
      love.event.quit()
    end
    --chickens move down 
    starty[i] = starty[i] + 80 * dt
  end
end

-------------------------------------------------
--DRAW
-------------------------------------------------
function love.draw()
  
  love.graphics.draw(backgroundImage, 0, 0, 0, 10, 10 )
  love.graphics.draw(powerUp, randX, randY)
  --draw each chicken at their respective x and y
  for i, v in ipairs(startx) do
    love.graphics.draw(chickenFace, startx[i], starty[i])

  end
end
