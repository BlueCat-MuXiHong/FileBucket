# vue-模板指令directive

## v-if

```vue
<div v-if="a > 100">
</div>
```

错误的：

```vue
<div v-if="return false">
</div>
```

## v-for

```vue
<html>
<head>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
</head>
<body>
    <div id='app'>
        <p>Vuejs周边的技术生态有： <p>
        <br/>
        <ul>
            <li v-for="tech in technologies">
                {% raw %}{{{% endraw %}tech}}
            </li>
        </ul>
    </div>
    <script>
        var app = new Vue({
            el: '#app', 
            data: {    
                technologies: [
                    "nvm", "npm", "node", "webpack", "ecma_script"
                ]
            }
        })
    </script>
</body>
</html>
```

