title: react-tutorial-1  
date: 2015-08-20 10:01:42  
categories: react  
tags: ['react','javascript','前端']  
description:
---
react入门教程-1
<!--more-->
### 环境搭建
> 需要安装
> 1. homebrew
> 2. node
> 3. bower  

``` sh
mkdir react-tutorial-1
bower install react
touch index.html
```

### Hello World
``` javascript
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Hello World</title>
    </head>
    <body>
        <div id="app"></div>
        <script type="text/javascript" src="bower_components/react/react.js"></script>
        <script type="text/javascript" src="bower_components/react/JSXTransformer.js"></script>
        <script type="text/jsx">

                var MessageBox  = React.createClass({
                    alertMe: function () {
                        alert("click...");
                    },
                    render: function() {
                        return (
                            <h1 onClick={this.alertMe}>Hello World {this.props.name}</h1>
                        );
                    }

                });

                React.render(
                    <MessageBox name={"shan"} />,
                    document.getElementById("app"),
                    function () {
                        console.log("render finished.");
                    }
                );
        </script>
    </body>
</html>
```

### component嵌套
``` javascript
<script type="text/jsx">
var MessageBox = React.createClass({
                    render: function() {
                        var subMessages = [];
                        for(var i=0; i<10; i++){
                            //key!!!
                            subMessages.push(<SubMessageBox key={"key_" + i}/>);
                        }
                        return (
                            <div>
                                <h1>Hello World {this.props.name}</h1>
                                {subMessages}
                            </div>

                        );
                    }
                });
                var SubMessageBox = React.createClass({
                    render: function() {
                        return (
                            <div>
                                <h3> SubMessageBox </h3>
                                <Footer />
                            </div>

                        );
                    }
                });
                var Footer = React.createClass({
                    render: function() {
                        return (
                            <h5> Footer </h5>
                        );
                    }
                });
                React.render(
                    <MessageBox name={"shan"} />,
                    document.getElementById("app"),
                    function () {
                        console.log("render finished.");
                    }
                );
</script>
```
注意*SubMessageBox*中的*key*, 在动态循环增加组件的过程中, 要给每一个组件的*key*赋唯一的值, 以保证组件的显示顺序和正确结果.

### state
``` javascript
<script type="text/jsx">

	var MessageBox = React.createClass({
                    getInitialState: function () {
                        return {count:0,}
                    },
                    addCount: function () {
                        this.setState({
                            count: this.state.count + 1,
                        });
                    },
                    render: function() {
                        return (
                            <div>
                                <h1>Hello World {this.props.name}</h1>
                                <h3>count: {this.state.count}</h3>
                                <button type="button" name="button" onClick={this.addCount}>click</button>
                            </div>

                        );
                    }
                });

                React.render(
                    <MessageBox name={"shan"} />,
                    document.getElementById("app"),
                    function () {
                        console.log("render finished.");
                    }
                );
</script>
```
注意在给*state*赋值时需要调用setState方法, 不要直接修改state. 每次调用setState都会重绘UI.