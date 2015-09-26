# heroku-(luajit+turbolua)-buildpack
buildpack with luajit and turbo(fast framework for webapp) - for Heroku Cedar platform.

How to setup :
 
 1)
 >heroku login
 
 2)
 >heroku create --stack cedar --buildpack https://github.com/6volt/heroku-luajit-turbolua-buildpack.git
 
 3)
 >git clone %your_app_repo_name.git%
 
 4)
 >cd %your_app_repo_name%
 
 5)create file named Procfile with next content : 
 >web:	luajit -e '_G.package.cpath=[[/app/luajit/lib/?.so]];_G.package.path=[[/app/luajit/share/lua/5.1/?.lua]]'  main.lua
 
 6)create file named main.lua with next content:
```lua
local turbo = require "turbo"
local ExampleHandler = class("ExampleHandler", turbo.web.RequestHandler)

function ExampleHandler:get()
	self:write("Hello , Heroku")
end

turbo.web.Application({{"^/$", ExampleHandler}}):listen(tonumber(os.getenv('PORT')))
turbo.ioloop.instance():start()
```
   
   7)type in your shell : 
   >git init;git add . ;git commit -am 'text';git push
   
   8) go to your webapp url and enjoy//or cry - this shitty shell script written very bad.

 
