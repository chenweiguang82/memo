# Octave的一些设置
最近想要在Linux下（Ubuntu 18.04 LTS）工作，用到一些计算的时候，Windows下有Matlab，Linux下虽然也有，但Octave更方便些。但是在使用的时候有些需要注意的事情。
## 默认编辑器 ##
Octave下默认的编辑器竟然是emacs，可以使用`EDITOR`命令看默认编辑器是哪种。emacs我不熟，我比较常用Vim，因此想要把这个给改一下。
创建`~/.octaverc`文件，加上这样两句话
```
edit mode async
EDITOR ("gnome-terminal -- vim %s")
```
然后在octave里就可以直接使用edit filename对脚本文件进行编辑了。  
**PS**
官网目前的方式有两种，但都已经比较落后了。官网提供的是
```
EDITOR ("gnome-terminal -e 'vim %s'")
```
但总是出现提示说-e以后不用了，让用--代替，但是--后面不能跟引号，所以需要改为上面那种。
## 默认画图程序
Octave下执行
```
octave:2> graphics_toolkit 
ans = fltk
```
可以看到默认的画图工具是fltk。执行
octave:3> available_graphics_toolkits 
ans = 
{
  [1,1] = fltk
  [1,2] = gnuplot
}
可以看到有两种，如果想要用gnuplot，可以在`~/.octaverc`里再加上
```
graphics_toolkit('gnuplot')
```
我本来想改成后者，后来发现fltk也挺小巧，不着急，先用着。  
如果想要在交互环境中临时更换上述默认值，可以直接在交互环境里执行上面的命令就可以了。
