.. _apple:

*****
apple
*****

关闭登陆界面多个用户登陆
===========================


sudo defaults write /Library/Preferences/com.apple.loginwindow SHOWOTHERUSERS_MANAGED -bool FALSE

强开随航
=========

defaults write com.apple.sidecar.display AllowAllDevices -bool true

defaults write com.apple.sidecar.display hasShownPref -bool true

环境变量配置
=============

因为terminal每次只会加载.zshrc，所以必须要在.zshrc里面写alias和环境变量，才会每次重启终端生效配置



苹果 电源适配器延长线缆
==============================


https://www.apple.com.cn/shop/product/MK122CH/A


调整鼠标速度
==================

defaults write -g com.apple.mouse.scaling 18

terminal输入然后重启，已爽死，嫌快的调小数值就行

还有滚轮速度

defaults write -g com.apple.scrollwheel.scaling 1.2


