# vscodePython 自定义函数不高亮的解决办法 

其实MagicPython的高亮方案中已经对自定义函数指定了高亮scope , 但是由于 Monokai 的颜色方案中并没有给起范围添加颜色 , 所以与sublime text中不同 ; 

参考 https://github.com/MagicStack/MagicPython/issues/96 之后得到得解决方案 : 

修改 ...\Microsoft VS Code\resources\app\extensions\theme-monokai\themes 下的 monokai-color-theme.json 文件 ,   
添加 :  
		{
			"name": "User-define Function name",
			"scope": "meta.function-call.generic.python",
			"settings": {
				"fontStyle": "",
				"foreground": "#66D9EF"
			}
		},	
即可 ;  
不用修改 python 文件夹下的 tmLanguege 文件 ;  
折腾了一天总结经验:      
英语不过关导致没有注意到别人已经说明高亮不仅取决于语法 , 而且取决于theme有没有方案 ;  


