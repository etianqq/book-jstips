#UI设计模式

分为三大类：MVC，MVP，MVVM

共同点：
######1.Model
The Model represents a set of classes that describes the business logic and data. It also defines business rules for data means how the data can be changed and manipulated.
######2.View
The View represents the UI components like CSS, jQuery, html etc. It is only responsible for displaying the data that is received from the controller as the result. This also transforms the model(s) into UI.

####MVC
![](/assets/mvcpattern.png)
######Controller
The Controller is responsible to process incoming requests. It receives input from users via the View, then process the user's data with the help of Model and passing the results back to the View. Typically, it acts as the coordinator between the View and the Model.

####MVP
![](/assets/mvppattern.png)

######Presenter
The Presenter is responsible for handling all UI events on behalf of the view. This receive input from users via the View, then process the user's data with the help of Model and passing the results back to the View. **Unlike view and controller, view and presenter are completely decoupled from each other’s and communicate to each other’s by an interface.**
Also, presenter does not manage the incoming request traffic as controller.

####MVVM
![](/assets/mvvmpattern.png)

######View Model
The View Model is responsible for exposing methods, commands, and other properties that helps to maintain the state of the view, manipulate the model as the result of actions on the view, and trigger events in the view itself.