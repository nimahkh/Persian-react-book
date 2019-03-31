## کامپوننت ها در ری اکت

<div dir="rtl" align="right">
کامپوننت ها قطعاتی هستند که میتوان از آن ها هرجایی در پروژه استفاده کرد و در اصطلاح reusable  هستند . 
<br/>
در ری اکت دو نوع کامپوننت میتوان نوشت ، یکی به شکل تابع و دیگری به شکل کلاس  (class components , functional components).
<br/>
داخل مثال hello world که پیشتر نوشتیم ، از کلاس کامپوننت ها استفاده کردیم 
<br/>

[مثال hello world](https://github.com/nimahkh/Persian-react-book/blob/master/examples/reactjs/01_helloworld/src/App.js) 
<br/>

حالا میتونیم همین کد رو به شکل زیر به شکل functional component  بنویسیم .

</div>

```
function App(props){

    return (
      <div className="App">
        <header className="App-header">
          <p>
            Hello World , Hello Iran .
          </p>
        </header>
      </div>
    );
}

export default App;
```

<div dir="rtl" align="right">
بعد از جایگزین کردن ، میبینید که اپ به درستی کار میکنه . 

### تفاوت میان کلاس و تابع 

این سوال شاید پیش بیاد که کدوم حالت بهتره؟
<br/>
استفاده از توابع از نظر سینتکسی خیلی راحت تر از کلاس ها هستند . 
<br/>
قبل از ری اکت 16.8 تنها دلیلی که میتوانست کلاس را برتر از توابع کند ، امکان نوشتن setState داخل کلاس ها بود .
<br/>
اما با ایجاد hooks  در ری اکت 16.8 این قابلیت پیش آمد که تمام life cycle  ری اکت را در functional Components  داشته باشید . 
<br/>
به کد زیر دقت کنید :
</div>

```
import React, { useState } from 'react';

function App() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}

export default App;
```

<div dir="rtl" align="right">
اگر کد بالا را جایگزین کد App.js  کنین میبینید که state  ها به راحتی جایگزین میشن . 
<br/>

#### چرا از توابع استفاده کنیم؟

ری اکت برای تبدیل کردن کدها به یک نسخه قابل قبول در جاوا اسکریپت نیاز به یک کامپایلر دارد . این کامپایلر به نام babel  شناخته شده .
<br/>
اگر ما کدهای کلاس کامپوننت ها را با توابع در babel  مقایسه کنیم ، متوجه میشیم که کلاس ها خروجی بسیار سنگینی نسبت به توابع دارند . 

###### خروجی babel  از کلاس کامپوننت

<img alt="خروجی babel  از کلاس کامپوننت" src="https://user-images.githubusercontent.com/12640517/55287214-397d1800-53bb-11e9-86c1-d10c3493fed6.png" width="250">

###### خروجی babel از توابع

<img alt="خروجی babel از توابع" src="https://user-images.githubusercontent.com/12640517/55287215-397d1800-53bb-11e9-873c-7f749fd5cebe.png" width="250">

<br/>
با مقایسه خروجی ها متوجه حجم زیاد خروجی های کلاس کامپوننت ها میشویم . 

<br/>

#### چرخه کامپوننت ها

کامپوننت های ری اکت دارای چرخه های زیادی هستند . 
معروفترین ها را در این سند میگیم . اما باقی چرخه ها به علت deprecate  شدن و یا کمتر استفاده شدن ، در این سند نیستند و ارجاع داده میشند به لینک ری اکت .
<br/>

- [Mounting](#mounting)

    - [constructor()](#constructor)
    - [static getDerivedStateFromProps()](https://reactjs.org/docs/react-component.html#static-getderivedstatefromprops)
    - [render()](#render)
    - [componentDidMount()](#componentDidMount)

- [Updating](#updating)

    - [static getDerivedStateFromProps()](https://reactjs.org/docs/react-component.html#static-getderivedstatefromprops)
    - [shouldComponentUpdate()](#shouldComponentUpdate)
    - [render()](https://reactjs.org/docs/react-component.html#shouldcomponentupdate)
    - [getSnapshotBeforeUpdate()](https://reactjs.org/docs/react-component.html#getsnapshotbeforeupdate)
    - [componentDidUpdate()](#componentDidUpdate)

- [Unmounting](#unmounting)

    - [componentWillUnmount()](#componentWillUnmount)

- [Error Handling](#error_handling)

    - [static getDerivedStateFromError()](https://reactjs.org/docs/react-component.html#static-getderivedstatefromerror)
    - [componentDidCatch()](#componentDidCatch)

<h5 id="mounting"> Mounting </h5>

- <h6 id="constructor"> constructor </h6>

در کلاس های constructor  ها سازنده مقادیر پیشفرض کلاس هستند . کاری که constructor ها داخل شی گرایی در همه زبان ها کار مقدار سازی اولیه را بر عهده دارند . 
<br/>
داخل لایبرری ری اکت ، این تابع عمدتا به منظور تعریف state  ها و bind  کردن توابع داخل کلاس کاربرد دارد . 

<br/>

اما در مورد functional components این موارد به شکل ثابت ها تعریف میشوند . 
<br/>

مثال کلاس کامپوننت ها : 

</div>

```
class A extends Component {

   constructor(props){
     super(props);
     this.state={
       grades:['a','b','c'],
       name : '',
       family : ''
     };
   }
   
   ...
}
```

<div dir="rtl" align="right">

مثال در توابع : 

</div>


```
function A(props){
...
   const [grades , setGrades]=useState(['a','b','c']);
   const [name , setName]=useState('');
   const [family , setFamily]=useState('');
...

}
```


<div dir="rtl" align="right">

- <h6 id="render"> render </h6>

این تابع فقط داخل کلاس کامپوننت ها کاربرد دارد  در واقع این تابع همراه خود this.props  و this.state  را به داخل بدنه کامپوننت میارد . 


- <h6 id="componentDidMount"> componentDidMount </h6>

این تابع زمانی که بارگذاری کامپوننت  به صورت کامل به اتمام رسید ، کار خود را شروع میکند . 
<br/>
خیلی بهتر بخوایم بگیم ، زمانی که کامپوننت بارگزاری شود ، هر آنچه داخل این تابع باشد اتفاق میفتد . شبیه به کار onLoad  در جاوا اسکریپت


<h5 id="updating"> Updating </h5>

- <h6 id="shouldComponentUpdate"> shouldComponentUpdate(nextProps, nextState) </h6>

این تابع به کامپوننت ما میگه که زمانی که یک state  به روز بشه ، کامپوننت رو مجدد render  کن  . 
<br/>
این تابع دو مقدار میگیره به اسم nextProps, nextState . در واقع بررسی میکنیم که state  یا props به سمت کامپوننت میاد ، آیا با مقادیر قبلی یا هر شرط دیگری که ما میدونیم ، قابل بررسی هست و نیاز به بروزرسانی کامپوننت دارد یا خیر.

- <h6 id="componentDidUpdate"> componentDidUpdate </h6>

اگر کامپوننت به روز شد و به روز رسانی موفقیت آمیز بود ، این تابع کار میکند و هر آنچه که در بدنه آن نوشته شده باشد اجرا میشود . 
<br/>

این تابع برای کلاس کامپوننت های نوشته شده است و برای توابع باید از useEffect  که معادل این تابع است استفاده کنیم . 
<br/>

useEffect یک هوک برای سنجش تغییرات کامپوننت در کلاس های تابعی هست که کاری مشابه  componentDidUpdate, componentWillUnmount , componentDidmount را انجام میدهد . 


<h5 id="unmounting"> Unmounting </h5>

- <h6 id="componentWillUnmount"> componentWillUnmount </h6>

این تابع در کلاس کامپوننت ها کاربرد دارد و وظیفه این را بر عهده دارد که بعد از خروج از کامپوننت ، یک سری عملیات انجام دهد . 
<br/>

عمدتا توابعی که به صورت async  هستند ، بعد از خروج از کامپوننت ها همچنان به کار خود ادامه میدهند . 
<br/> 
مثلا شما یک setInterval  نوشتید که هر 10 ثانیه یک عملیاتی را انجام دهد . 
حالا از صفحه و کامپوننت خارج شدید . قاعدتا باید clearInterval اتفاق بیفتد . در غیر این صورت بدنه اینتروال همچنان ادامه خواهد داشت . 
<br/>
clearInetrval  را در این تابع مینویسیم که به کامپوننت بگیم بعد از خروج ، حتما تابع async  رو متوقف کن 


<h5 id="error_handling"> Error Handling </h5>

- <h6 id="componentDidCatch"> componentDidCatch(error, info) </h6>

این تابع که به تازگی معرفی شده دو مقدار دارد .  error, info . 
زمانی که یک خطایی در کامپوننت رخ دهد ، به کمک این تابع میتوانید جلو یک سری ارور ها و exception  هایی که ری اکت به کاربر نمایش میدهد را بگیرید . 
<br/>

</div>


```
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // Update state so the next render will show the fallback UI.
    return { hasError: true };
  }

  componentDidCatch(error, info) {
    // Example "componentStack":
    //   in ComponentThatThrows (created by App)
    //   in ErrorBoundary (created by App)
    //   in div (created by App)
    //   in App
    logComponentStackToMyService(info.componentStack);
  }

  render() {
    if (this.state.hasError) {
      // You can render any custom fallback UI
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children; 
  }
}
```
