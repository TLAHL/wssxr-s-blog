1. 为什么要是用require.js?

   传统的前端开发，都是将js文件按照调用的先后顺序以script标签的形式引用。
这样的模式，当项目规模较小，开发人员较少的的情况下是勉强可以的。如果遇到较大规模
的项目，需要多人配合则维护起来相当麻烦；

主要有以下两点问题：
   1.  加载的时候，浏览器会停止网页渲染，加载文件越多，网页失去响应的时间就会越长； 
   2.  由于js文件之间存在依赖关系，因此必须严格保证加载顺序; 依赖性最大的模块一定要放到最后加载，当依赖关系很复杂的时候，代码的编写和维护都会变得困难。

2. require.js的加载

   <script type="text/javascript"  async="true" defer data-main="main"  src="require.js"></script>

3. 基本函数： require, define, require.config
  
   data-main: main.js 中
   require.config({
      baseUrl: '.', //配置根目录，默认的为： 项目根目录.
      paths:{
         //配置常用插件，模块的的路径
      },
      
      shim: {
         //Remember: only use shim config for non-AMD scripts,
         
         //scripts that do not already call define(). The shim
         
         //config will not work correctly if used on AMD scripts,
         
         //in particular, the exports and init config will not
         
         //be triggered, and the deps config will be confusing
         
         //for those cases.
         
         'backbone': {
         
            //These script dependencies should be loaded before loading
            
            //backbone.js
            deps: ['underscore', 'jquery'],
            
            //Once loaded, use the global 'Backbone' as the
            
            //module value.
            
            exports: 'Backbone'
            
        },
        'underscore': {
        
            exports: '_'
            
        },
        
        'foo': {
        
            deps: ['bar'],
            
            exports: 'Foo',
            
            init: function (bar) {
            
                //Using a function allows you to call noConflict for
                
                //libraries that support it, and do other cleanup.
                
                //However, plugins for those libraries may still want
                
                //a global. "this" for the function will be the global
                
                //object. The dependencies will be passed in as
                
                //function arguments. If this function returns a value,
                
                //then that value is used as the module export value
                
                //instead of the object found via the 'exports' string.
                
                //Note: jQuery registers as an AMD module via define(),
                
                //so this will not work for jQuery. See notes section
                
                //below for an approach for jQuery.
                
                return this.Foo.noConflict();
                
            }
            
        }
        
      },
      
   });


              
                  
