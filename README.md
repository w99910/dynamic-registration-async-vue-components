# Register asynchronous VUE components dynamically


```js
import { createApp, defineAsyncComponent } from 'vue'
import App from './App.vue';

const app = createApp(App)

const components = import.meta.glob('./components/**/*.vue');

for (let component of Object.keys(components)) {
    let paths = component.split('/');
    let componentName = '';
    paths = paths.slice(2, paths.length)
    paths.forEach((path, i)=>{
        componentName += path.replace('.vue','');
        if(i !== paths.length - 1){
            componentName += '.'
        }
    });
    app.component(componentName, defineAsyncComponent(() => components[component]()))
}


app.mount('#app')
```