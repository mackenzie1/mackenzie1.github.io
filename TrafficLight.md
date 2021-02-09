# [Home Page](README.md)

This was created as a project to practice with java gui. The code outputs a traffic light with three buttons on the bottom for red, yellow, and green.

![image](green.PNG)
![image](red.PNG)
![image](yellow.PNG)
## Imports
```java
import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.geometry.Pos;
import javafx.scene.Scene;
import javafx.scene.control.RadioButton;
import javafx.scene.control.ToggleGroup;
import javafx.scene.layout.BorderPane;
import javafx.scene.layout.GridPane;
import javafx.scene.layout.HBox;
import javafx.scene.layout.StackPane;
import javafx.scene.paint.Color;
import javafx.stage.Stage;
import javafx.scene.shape.*;
```
## Creating Basic Ingredients

Here I create a stage. I also create a Stack Pane and Rectange objects. 

```
public class TrafficLight extends Application {
    public static void main(String[] args) {
        launch(args);
    }

    @Override
    public void start(Stage primaryStage) {
        primaryStage.setTitle("Traffic Light");
        //create stackpane
        StackPane pane = new StackPane();
        Rectangle rectangle = new Rectangle(125, 250, 100, 250);
```
## Rectanlge Adjustments

Here I put the rectangle inside the stack pane. The next lines are modify the recatngles apperance. Setting the fill to white and the border to black so we can see it.

```
        //add rectangle to stackpane
        pane.getChildren().add(rectangle);
        rectangle.setFill(Color.WHITE);
        rectangle.setStroke(Color.BLACK);
```
## Grid Pane

Here I am creating a grid pane. I personally used a grid pane because I thought it would be the easiest to get all of our elements lined up correctly. This was my personal choice but you can use lots of other layouts like VBox. This layout could be useful in recreating this project because it stacks the objects you put inside it vertically.

```
        //create gridpane
        GridPane pane1 = new GridPane();
        pane1.setAlignment(Pos.CENTER);
        pane1.setPadding(new Insets(5, 5, 5, 5));
        pane1.setHgap(5);
        pane1.setVgap(5);
```
## Grid Pane in Stack Pane

This step is very important and can be overlooked easily. Here I am putting the gridpane inside the stack pane. Remember our stack pane contains our rectangle. I am setting it up like this so the stack pane will contain our rectangle and then our grid pane. Object will soon go inside the gride pane. 
```
        //add gridpane to stackpane
        pane.getChildren().add(pane1);
```
## Create Circles and Add Them to the Grid Pane

This code is creating circle objects. I modify the circle's size, color, and border. With the pane.add command I am setting the circles to be stacked inside the grid pane vertically like so, myPane.add(yourObject, columnIndex, rowIndex)

```
        //create some circles
        Circle circle = new Circle();
        circle.setStroke(Color.BLACK);
        circle.setFill(Color.WHITE);
        circle.setRadius(25.0f);

        //add circle to gridpane
        pane1.add(circle,1,1);

        Circle circle2 = new Circle();
        circle2.setStroke(Color.BLACK);
        circle2.setFill(Color.WHITE);
        circle2.setRadius(25.0f);

        //add circle to gridpane and put it below the other circle
        pane1.add(circle2,1,2);

        Circle circle3 = new Circle();
        circle3.setStroke(Color.BLACK);
        circle3.setFill(Color.WHITE);
        circle3.setRadius(25.0f);
        //add circle to gridpane and put it below the other circle
        pane1.add(circle3,1,3);
        
```
## Toggle Group and Radio Buttons
This code creates a toggle group and radio buttons. I simply create the toggle group. Next I create the radio buttons and modify their text and add them to our toggle group. 
```
        //create a toggle group
        final ToggleGroup group = new ToggleGroup();

        //make a radio button
        RadioButton rb1 = new RadioButton("Red");
        //put radio button in the toggle group
        rb1.setToggleGroup(group);


        RadioButton rb2 = new RadioButton("Yellow");
        rb2.setToggleGroup(group);

        RadioButton rb3 = new RadioButton("Green");
        rb3.setToggleGroup(group);
```
## HBox

Here I create a Hbox. This is similar to the Vbox mentioned before but it puts all the objects inside horizontally. I then put all of our radio buttons inside.
```
        //create Hbox
        HBox hBox = new HBox(5);
        //add the buttons to the hbox
        hBox.getChildren().addAll(rb1, rb2, rb3);
        hBox.setAlignment(Pos.CENTER);
```
## Border Pane
This code creates a border pane. This border pane contains our stack pane which contains our rectange and our grid pane (which contains our circles). Then I put our Hbox at the bottom below the stack pane. Basically this border pane is our last container to hold all the elements we've created so far.
```
        //create a border pane
        BorderPane borderPane = new BorderPane();
        //add border pane to stack pane
        borderPane.setCenter(pane);
        borderPane.setBottom(hBox);

        //create a scene with the border pane which now
        // contains a stackpane (the rectangle) and within
        // the stack pane a grid pane(the circles)
        Scene scene = new Scene(borderPane);
        //add the scene to the scene
        primaryStage.setScene(scene);
        primaryStage.show();
```
## Making our Buttons Change the Color

Here I create our on action event. When a radio button is pressed I set our circles to the corresponding colors.

```
        //create action events for buttons
        rb1.setOnAction(e -> {
            circle.setFill(Color.RED);
            circle2.setFill(Color.WHITE);
            circle3.setFill(Color.WHITE);
        });

        rb2.setOnAction(e ->{
            circle.setFill(Color.WHITE);
            circle2.setFill(Color.YELLOW);
            circle3.setFill(Color.WHITE);
        });

        rb3.setOnAction(e ->{
            circle.setFill(Color.WHITE);
            circle2.setFill(Color.WHITE);
            circle3.setFill(Color.GREEN);
        });

    }
}
```
