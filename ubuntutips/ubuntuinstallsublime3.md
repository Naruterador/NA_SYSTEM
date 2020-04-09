1.wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -

2.sudo apt-get install apt-transport-https

3.echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list

4.sudo apt-get update

5.sudo apt-get install sublime-text 
	Using next commands to fix the problem of typing chinese.

6.git clone https://github.com/lyfeyaj/sublime-text-imfix.git

7.cd sublime-text-imfix && ./sublime-imfix

8.installing sublime text3 plug-in in mac pro

Changing the content in Settings-Users

	"channels":
	[
		"http://cst.stu.126.net/u/json/cms/channel_v3.json"
	],
	