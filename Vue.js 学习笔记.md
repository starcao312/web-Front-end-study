## Vue.js 学习笔记

### 一、vue指令学习

1. v-text:

2. v-html:

3. v-on:

   1. 绑定事件监听器
   2. v-on: 在某些时候可以使用简写 `@` 符号
   3. v-on 指令用于绑定HTML事件 ：v-on:click 缩写为 @click
   4. v-on结合事件修饰符可以对事件进行限制，比如：enter
   5. v-on在绑定事件时可以传递自定义参数

4. v-show:

   1. 如果条件为false，运行后，还是生成了条件为false所在的标签，但是只是让其display属性为none，即该标签不进行显示

5. v-if:

   1. v-show 与 v-if 的区别：
      1. 手段：v-if是通过控制dom节点的存在与否来控制元素的显隐；v-show是通过设置DOM元素的display样式，block为显示，none为隐藏；
      2. 编译过程：v-if切换有一个局部编译/卸载的过程，切换过程中合适地销毁和重建内部的事件监听和子组件；v-show只是简单的基于css切换；
      3. 编译条件：v-if是惰性的，如果初始条件为假，则什么也不做；只有在条件第一次变为真时才开始局部编译（编译被缓存？编译被缓存后，然后再切换的时候进行局部卸载); v-show是在任何条件下（首次条件是否为真）都被编译，然后被缓存，而且DOM元素保留；
      4. 性能消耗：v-if有更高的切换消耗；v-show有更高的初始渲染消耗；

   2. 使用场景：

      基于以上区别，因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件很少改变，则使用 v-if 较好。

   3. 总结：

      v-if判断是否加载，可以减轻服务器的压力，在需要时加载,但有更高的切换开销;v-show调整DOM元素的CSS的dispaly属性，可以使客户端操作更加流畅，但有更高的初始渲染开销。如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件很少改变，则使用 v-if 较好。

6. v-bind:

   1. v-bind指令用于设置HTML属性：v-bind:href  缩写为 :href

7. v-for:

   1. 作用：根据数据生成列表结构；
   2. 数组经常和v-for结合使用；
   3. 语法是：(item, index) in 数据；
   4. item 和 index 可以结合其他指令一起使用；
   5. 数组长度的更新会同步到页面上，是响应式的。

8. v-model

   1. `v-model`指令的作用是便捷的设置和获取表单元素的值
   2. 绑定的数据会和表单元素值相关联
   3. 绑定的数据 <----> 表单元素的值
   4. `v-model`是一个指令，限制在`<input>`、`<select>`、`<textarea>`、`components`中使用，修饰符`.lazy`(取代 input 监听 change 事件)、`.number`(输入字符串转为有效的数字)、`.trim`(输入首尾空格过滤)。它其实是一个**语法糖**

### 二、axios

1. `axios`

   - `axios`是基于`promise`（诺言）用于浏览器和`node.js`是`http`客户端。

2. `axios`的作用

   - `axios`主要是用于向后台发起请求的，还有在请求中做更多是可控功能。

3. `axios`的特点

   - 支持浏览器和`node.js`
   - 支持`promise`
   - 能拦截请求和响应
   - 能转换请求和响应数据
   - 能取消请求
   - 自动转换JSON数据
   - 浏览器支持防止CSRF（跨站请求伪造）

4. `promise`

   - `promise`是一个对象用来传递异步操作的信息，它代表了某个未来才会知道结果的事件（通常是一个异步操作），并且这个事件提供统一的api，可供进一步的处理。

5. `promise`的作用

   - `Promise`的出现主要是解决地狱回调的问题，比如你需要结果需要请求很多个接口，这些接口的参数需要另外那个的接口返回的数据作为依赖，这样就需要我们一层嵌套一层，但是有了`Promise` 我们就无需嵌套。
   - `promise` 的本质是分离异步数据获取和业务。

6. `axios` 执行 `GET` 请求

   ```js
   // 为给定 ID 的 user 创建请求
   axios.get('/user?ID=12345')
     .then(function (response) {
       console.log(response);
     })
     .catch(function (error) {
       console.log(error);
     });
   
   // 可选地，上面的请求可以这样做
   axios.get('/user', {
       params: {
         ID: 12345
       }
     })
     .then(function (response) {
       console.log(response);
     })
     .catch(function (error) {
       console.log(error);
     });
   ```

7. `axios` 执行 `POST` 请求

   ```javascript
   axios.post('/user', {
       firstName: 'Fred',
       lastName: 'Flintstone'
     })
     .then(function (response) {
       console.log(response);
     })
     .catch(function (error) {
       console.log(error);
     });
   ```

8. 执行多个并发请求

   ```javascript
   function getUserAccount() {
     return axios.get('/user/12345');
   }
   
   function getUserPermissions() {
     return axios.get('/user/12345/permissions');
   }
   
   axios.all([getUserAccount(), getUserPermissions()])
     .then(axios.spread(function (acct, perms) {
       // 两个请求现在都执行完成
     }));
   ```

   - get和post都是基于promise的所以写法上很相似，是用then和catch，使用这种方法来进行发送请求。

9. 拦截器

   - 在请求或响应被 `then` 或 `catch` 处理前拦截它们（拦截器可以做什么：在请求或者响应时拦截下来进行处理）
   - 拦截器分为请求拦截器和响应拦截器
   - 请求拦截器（`interceptors.requst`）是指可以拦截每次或指定HTTP请求，并可修改配置项。
   - 响应拦截器（`interceptors.response`）可以在每次HTTP请求后拦截住每次或指定HTTP请求，并可修改返回结果项。

   ```javascript
   // 添加请求拦截器
   axios.interceptors.request.use(function (config) {
       // 在发送请求之前做些什么
       return config;
     }, function (error) {
       // 对请求错误做些什么
       return Promise.reject(error);
     });
   
   // 添加响应拦截器
   axios.interceptors.response.use(function (response) {
       // 对响应数据做点什么
       return response;
     }, function (error) {
       // 对响应错误做点什么
       return Promise.reject(error);
     });
   ```

10. 拦截器的工作流程：

    ![img](.\笔记图片\拦截器.png)

11. 移除拦截器

    ```javascript
    var myInterceptor = axios.interceptors.request.use(function () {/*...*/});
    axios.interceptors.request.eject(myInterceptor);
    ```

12. 自定义 `axios` 实例添加拦截器

    ```javascript
    var instance = axios.create();
    instance.interceptors.request.use(function () {/*...*/});
    ```

13. 错误处理

    ```javascript
    axios.get('/user/12345')
      .catch(function (error) {
        if (error.response) {
          // 请求已发出，但服务器响应的状态码不在 2xx 范围内
          console.log(error.response.data);
          console.log(error.response.status);
          console.log(error.response.headers);
        } else {
          // Something happened in setting up the request that triggered an Error
          console.log('Error', error.message);
        }
        console.log(error.config);
      });
    ```

    