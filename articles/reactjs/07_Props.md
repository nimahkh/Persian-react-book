## پراپس ها در ری اکت

<div dir="rtl" align="right">
پراپس ها یا (Props) داده های هستند که میتوانیم آن ها را میان کامپوننت ها انتفال بدیم . برای مثال ما یک کامپوننت A داریم و قصد داریم که مقادیری از داخل این کامپوننت به کامپوننت B ارسال کنیم . 

<br/>

این اتفاق شاید شایع ترین کار در ری اکت باشد و باید روی فراگرتن آن بسیار تمکرز کرد . 

<br/>

نحوه کار با پراپس ها در کلاس کامپوننت ها و توابع متفاوت است . مثل همیشه هر دو مثال را مطرح میکنم و با هم روی مثال ها بحث میکنیم . 

## Funtional component

</div> 

```
import React from "react";

const A = ()=>{

   const world= "World";
   return (
      <Hello what={world} />
   );
}

const Hello = (props)=>{
   return (
      <React.Fragment>
         {props.what}
      </React.Fragment>
   );
}

```

<div dir="rtl" align="right">

## Class Components

</div>


```
import React,{Component} from "react";

class A extends Component {   
   render(){
     const world= "World";
     
     return (
        <Hello what={world} />
     );
   }
   
}

class Hello extends Component{
   render(){
     const {what}=this.props;
     
     return (
        <React.Fragment>
           {what}
        </React.Fragment>
     );
   }
}

```

<div dir="rtl" align="right">

در دو مثال بالا از داخل کامپوننت A مقداری را به کامپوننت Hello پاس دادیم . در واقع این کار به کمک پراپسی به اسم what  انجام شد . 

<br/>

what  هر اسمی میتونه داشته باشه . ما برای مثال ، این اسم رو انتخاب کردیم . 

## نحوه پاس دادن Props ها 

شما میتوانید به هر شکلی پراپس ها را پاس بدید . به مثال های زیر توجه کنید . 

<br/>

#### مثال اول

</div>

```
import React, {Component} from "react";

class A extends Component {
    render() {
        const world = {"sayWhat": "hello", "toWho": "world"};

        return (
            <Hello what={world}/>
        );
    }

}

class Hello extends Component {
    render() {
        const {what} = this.props;

        return (
            <React.Fragment>
                {what.sayWhat} Dear {what.toWho}
            </React.Fragment>
        );
    }
}

}

```

<div dir="rtl" align="right">

#### مثال دوم

</div>

```
import React, {Component} from "react";

class A extends Component {
    render() {
        const world = ["hello","React","world"];

        return (
            <Hello what={world}/>
        );
    }

}

class Hello extends Component {
    render() {
        const {what} = this.props;

        return (
            <React.Fragment>
                {what[0]} Dear {what[1]} i am {what[2]}
            </React.Fragment>
        );
    }
}
```

<div dir="rtl" align="right">

#### مثال سوم

</div>

```
import React, {Component} from "react";

class A extends Component {
    render() {
        const world = ["hello","React","world"];
        const description="everything is awesome";

        return (
            <Hello what={world} whatsUp={description}/>
        );
    }

}

class Hello extends Component {
    render() {
        const {what,whatsUp} = this.props;

        return (
            <React.Fragment>
                {what[0]} Dear {what[1]} i am {what[2]}
                <br/>
                Oh , hello {what[2]} , whats up?
                <br/>
                mmmm... {whatsUp}
            </React.Fragment>
        );
    }
}
```

<div dir="rtl" align="right">

##### مثال چهارم  

</div>

```
import React, {Component} from "react";

class A extends Component {

    description(){
        return "everything is awesome";
    }

    render() {
        const world = ["hello","React","world"];

        return (
            <Hello what={world} whatsUp={this.description.bind(this)}/>
        );
    }

}

class Hello extends Component {
    render() {
        const {what,whatsUp} = this.props;

        return (
            <React.Fragment>
                {what[0]} Dear {what[1]} i am {what[2]}
                <br/>
                Oh , hello {what[2]} , whats up?
                <br/>
                mmmm... {whatsUp}
            </React.Fragment>
        );
    }
}

```

<div dir="rtl" align="right">

## render props

یک مفهوم بسیار جذاب در ری اکت وجود دارد به اسم render props که شما به کمک این مفهوم میتوانید به راحتی کامپوننت ها را به شکل یک props بین هم انتقال بدید . 
<br/>

</div>

```
class Cat extends React.Component {
  render() {
    const mouse = this.props.mouse;
    return (
      <img src="/cat.jpg" style={{ position: 'absolute', left: mouse.x, top: mouse.y }} />
    );
  }
}

class Mouse extends React.Component {
  constructor(props) {
    super(props);
    this.handleMouseMove = this.handleMouseMove.bind(this);
    this.state = { x: 0, y: 0 };
  }

  handleMouseMove(event) {
    this.setState({
      x: event.clientX,
      y: event.clientY
    });
  }

  render() {
    return (
      <div style={{ height: '100%' }} onMouseMove={this.handleMouseMove}>

        {/*
          Instead of providing a static representation of what <Mouse> renders,
          use the `render` prop to dynamically determine what to render.
        */}
        {this.props.render(this.state)}
      </div>
    );
  }
}

class MouseTracker extends React.Component {
  render() {
    return (
      <div>
        <h1>Move the mouse around!</h1>
        <Mouse render={mouse => (
          <Cat mouse={mouse} />
        )}/>
      </div>
    );
  }
}
```

<div dir="rtl" align="right">

در مثال بالا MouseTracker کامپوننت Mouse  را فراخوانی کرد . اما به جای آن که داخل Mouse کامپوننت Cat  را قرار دهد ، با کمک پراپسی به اسم render آن را به شکل props صدا زد . 

<br/>
 درنهایت کامپوننت Mouse نتایج حرکت کردن موس را داخل کامپوننتی که در render معرفی شد قرار داد . 
<br/>
 کاموننت cat  هم با تغییر دادن موس ، مختصات تصویر را جابه جا کرد . 
<br/>
در واقع دو کاموننت mouse و cat  بدون داشتن هیچگونه وابستگی به یکدیگر ، کاری را انجام دادن که نتیجه آن به هردوی آن ها وابسته بود و وابستگی آن در کاموننت MouseTracker  ایجاب شد . 

</div>
