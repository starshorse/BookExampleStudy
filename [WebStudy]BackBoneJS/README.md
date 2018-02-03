# README.md
## Web Tutorial for Backbone.Js 
Backbone.js for Absolute Beginners - Getting started (Part 1: Intro)
http://adrianmejia.com/blog/2012/09/11/backbone-dot-js-for-absolute-beginners-getting-started/#start
##Default  Including Scripts 
  <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js" type="text/javascript"></script>
  <script src="http://cdnjs.cloudflare.com/ajax/libs/underscore.js/1.3.3/underscore-min.js" type="text/javascript"></script>
  <script src="http://cdnjs.cloudflare.com/ajax/libs/backbone.js/0.9.2/backbone-min.js" type="text/javascript"></script>
  <script src="http://cdnjs.cloudflare.com/ajax/libs/backbone-localstorage.js/1.0/backbone.localStorage-min.js" type="text/javascript"></script>  

## Tutorial 2 
Backbone.js for absolute beginners - getting started (part 2: Models, Collections and Views)
## Tutorial 3 
Backbone.js for absolute beginners - getting started (part 3: CRUD) 
There are a couple of features that we could improve. Let¡¯s implement the CRUD (Create-Read-Update-Delete) for the item list.
#### 1.- You want to respond to a double click event showing up a text box, where the user can change the text. 
First, let¡¯s add the HTML in the item-template template below the label tag.                                                                                                                                                                                       
<input class="edit" value="<%- title %>">     
#### D-elete                                                                                                                                                                                                                                                                                                                         
To be able to remove to-do items, we need to add a remove button in each item and listen to the click event on it,
which will trigger the destroy function in the selected todo object.
                                                                               
@@ -47,6 +47,7 @@                                                              
       <input class="toggle" type="checkbox" <%= completed ? 'checked' : '' %>>
       <label><%- title %></label>                                             
       <input class="edit" value="<%- title %>">                               
+      <button class="destroy">remove</button>                                 
     </div>                                                                    
   </script>      
                                                                
@@ -105,12 +106,14 @@
       },
       initialize: function(){
         this.model.on('change', this.render, this);
+        this.model.on('destroy', this.remove, this); // remove: Convenience Backbone'
       },
       events: {
         'dblclick label' : 'edit',
         'keypress .edit' : 'updateOnEnter',
         'blur .edit' : 'close',
-        'click .toggle': 'toggleCompleted'
+        'click .toggle': 'toggleCompleted',
+        'click .destroy': 'destroy'
       },
       edit: function(){
         this.$el.addClass('editing');
@@ -130,7 +133,10 @@
       },
       toggleCompleted: function(){
         this.model.toggle();
-      }
+      },
+      destroy: function(){
+        this.model.destroy();
+      }
     });         
## Tutorial 4 
Backbone.js for absolute beginners - getting started (part 4: Routers) 
You could build web application without using the routers. 
However, if you want to make reference to certain ¡®state¡¯ or location of the web application, you need a reference (link/URL) to it. 
This is where routers come to rescue.
Routing in most of JS application are achieved by hash-tags. E.g. If you take a look of Gmail URL you will see something like:
https://mail.google.com/mail/u/0/#inbox/139c0d48e11d986b
where the #inbox/139c0d48e11d986b is the hash-tag which reference some email location.
In backbone, routes are hash maps that match URL patterns to functions. You can use parameter parts, 
such as todos/:id, or using splats file/*path you will match all the parameters from the splat on. For that reason, 
the splat parameter should be always the last matcher.

app.Router = Backbone.Router.extend({
  routes: {
    '*filter' : 'setFilter'
  },
  setFilter: function(params) {
    console.log('app.router.params = ' + params); // just for didactical purposes.
    window.filter = params.trim() || '';
    app.todoList.trigger('reset');
  }
});

    //--------------
     // Initializers
     //--------------
+    app.router = new app.Router();
+    Backbone.history.start();
     app.appView = new app.AppView();

You can test that you router is working just typing #anything/that/you/want and seeing the parameter in you browser¡¯s console.
@@ -164,7 +177,18 @@
       },
       addAll: function(){
         this.$('#todo-list').html(''); // clean the todo list
-        app.todoList.each(this.addOne, this);
+        // filter todo item list
+        switch(window.filter){
+          case 'pending':
+            _.each(app.todoList.remaining(), this.addOne);
+            break;
+          case 'completed':
+            _.each(app.todoList.completed(), this.addOne);
+            break;
+          default:
+            app.todoList.each(this.addOne, this);
+            break;
+        }
       },
       newAttributes: function(){
         return {
@@ -85,7 +90,15 @@
     //--------------
     app.TodoList = Backbone.Collection.extend({
       model: app.Todo,
-      localStorage: new Store("backbone-todo")
+      localStorage: new Store("backbone-todo"),
+      completed: function() {
+        return this.filter(function( todo ) {
+          return todo.get('completed');
+        });
+      },
+      remaining: function() {
+        return this.without.apply( this, this.completed() );
+      }
     });
  @@ -32,6 +32,11 @@
     <header id="header">
       <h1>Todos</h1>
       <input id="new-todo" placeholder="What needs to be done?" autofocus>
+      <div>
+        <a href="#/">show all</a> |
+        <a href="#/pending">show pending</a> |
+        <a href="#/completed">show completed</a>
+      </div>
     </header>
     <section id="main">
       <ul id="todo-list"></ul>

