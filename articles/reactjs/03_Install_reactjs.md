## نصب ری اکت
<div dir="rtl" align="right">
به منظور نصب ری اکت ابتدا باید node.js را نصب کنید تا از طریق npm که مدیریت پکیج رو برای node.js انجام میده ، به مخازن دسترسی داشته باشیم و نصب رو شروع کنیم . 
<br/>
برای نصب node.js مراحل زیر را داخل لینوکس ،  انجام بدید

<div dir="ltr" align="left">

#### Arch Linux 
```
pacman -S nodejs npm
```
#### FreeBSD
```
pkg install node
```
#### Gentoo
```
emerge nodejs
```
#### macOS
```
curl "https://nodejs.org/dist/latest/node-${VERSION:-$(wget -qO- https://nodejs.org/dist/latest/ | sed -nE 's|.*>node-(.*)\.pkg</a>.*|\1|p')}.pkg" > "$HOME/Downloads/node-latest.pkg" && sudo installer -store -pkg "$HOME/Downloads/node-latest.pkg" -target "/"
brew install node
```
#### Debian
```
# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs

# Using Debian, as root
curl -sL https://deb.nodesource.com/setup_10.x | bash -
apt-get install -y nodejs
```

</div>

بعد از نصب node.js ، مدیریت پکیج هم نصب میشود . با کد زیر میتونیم از صحت نصبمون مطمئن بشیم

<div dir="ltr" align="left">

```
npm -v
nodejs -v
```

</div>

کد بالا ورژن نود جی اس و npm نصب شده شما را به شما نمایش میدهد


 حالا با دستور زیر میتونیم ری اکت رو نصب کنیم 
<div dir="ltr" align="left"> 

 ```
 sudo npm install -g create-react-app
 
 OR
 
 npm init react-app 01_helloworld 
 ```
  که 01_helloworld اسم پروژه ای که قصد ساختنش رو داریم هست . 
 
 </div>
 
 پکیج create-react-app یک boilerplate برای راه اندازی ری اکت به صورت خیلی راحتتر ، همراه با یک مثال آماده و تنظیمات استاندارد ری اکت است . 
 
 <br/>
 پس از اتمام نصب ، تنها کافیست که کد زیر را وارد کنیم 
 
 <div dir="ltr" align="left">
 
 ```
 create-react-app PersianReactAppProject
 ```
 
 </div>
 
 حالا ری اکت داخل پوشه PersianReactAppProject  نصب شده . کافیست به این مسیر برید و کد زیر را بنویسید
 <div dir="ltr" align="left">
 
 ```
 cd PersianReactAppProject
 npm run start
 ```
 
 </div>
 
 پروژه ری اکت شما روی آدرس localhost:3000 قابل مشاهده است .
 
</div>
