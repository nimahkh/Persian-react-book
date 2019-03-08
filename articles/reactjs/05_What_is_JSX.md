## درباره jsx 

<div dir="rtl" align="right">

در مورد jsx  شاید قبلا شنیده باشید یا پیش از این با این پسوند کد زده باشید .
<br/>
اما الان میخوایم ببینیم که JSX  چیست .

#### JSX چیست؟

jsx  یک فرمت جاوا اسکریپتی برای ایجاد DOM  های HTML در قالب یک کامپوننت است .

##### یک مثال ساده 

```
const Hello =<h1> Hello world </h1>;
```
در این مثال یک هدینگ ایجاد کردیم که hello world  رو داخل متغیر Hello  قرار میدهد .
 <br/>
 در واقع jsx  به کد های جاوا اسکریپت تبدیل میشود و در نهایت یک شئ جاوا اسکریپتی خروجی آن است . 
 
 #####  به عنوان مثال 
 ```
 const hello = <h2 className = "IRC"> Hello World </h2>
 ```
 
 خروجی کد بالا در جاوا اسکریپت کد زیر خواهد بود :
 <br/>
 ```
 const hello = React.createElement {
        type: "h2",
        props: {
            className: "IRC",  
            children: "Hello World" 
           }
     }
 ```
در jsx  میتوانید چندین خط زیر هم بنویسید و یک بلاک ایجاد کنید . اما باید این بلاک میان پرانتز باشد .

```
const headings = (
        <div id = "Outer">
           <h1>first Head </h1>
           <h2>second Head</h1> 
        </div>
    );
```

هر بلاک باید داخل یک المان html یا یک تگ باز و بسته باشد . به عنوان مثال ، کد زیر اشتباه است . 
 
 ```
 const headings = (
           <h1>first Head </h1>
           <h2>second Head</h1> 
       );
 ```

تمام attribute ‌های jsx از قانون camleCase  استفاده میکنند . 

```
    This will work in JSX
    <button onClick = {handleClick}>Click Me</button>

    This will not work in JSX
    <button onclick = {handleClick}>Click Me</button>
```

در مثال بالا باید onclick  در کد دوم که اشتباه است به onClick  با c  بزرگ و به شکل camleCase  باشد . برای باقی attribute ها هم به همین شکل. به عنوان مثال :‌

```
const classHtml= <div className="Hello">Hello world</div>;

```

در مثال بالا className معادل class  هست . 

<br/>
 اما گاهی اوقات ما قصد داریم چندین کلاس را در یک تگ داشته باشیم . 
  <br/>
  در مثال زیر دو مدل درست و اشتباه را مقایسه میکنیم . 
  
  ```
  
  //Wrong example
  const multiClass=<div className="Hello Bye"> two hello and bye </div>
  
  //Correct Example
  const multiClass=<div className={["Hello","Bye"].join(" ")}> two Hello and bye </div>
  
  ```
در مثال بالا یک آرایه از کلاس ها ساختیم و با join با فاصله به هم وصل کردیم . 

<br/>

در jsx تمام تگ ها self closing  هستند . به این معنی که اگر داخل html یک div  خالی باز و بسته کنید در jsx  مانند تگ hr self closing است . 

```
slef closing div

<div className="self" />

```
تگ بالا معادل کد زیر است در html

```
<div class='self' >  </div>
```

</div>