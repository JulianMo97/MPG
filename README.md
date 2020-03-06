import javafx.application.*; 
import javafx.event.ActionEvent;
import javafx.animation.*; 
import javafx.util.Duration;
import javafx.geometry.Insets;
import javafx.scene.*;
import javafx.scene.control.*; 
import javafx.scene.layout.*; 
import javafx.scene.shape.*;
import javafx.scene.paint.*;
import javafx.stage.*;

public class Main extends Application
{

	public static void main(String[] args) 
	{
		launch(args);

	}
	public void start(Stage stage) 
	{
		//*********************************************************** 
		// Create the animation objects 
		//*********************************************************** 
		//create sun
		Circle sun = new Circle(400, 240, 30); 
		sun.setStroke(Color.rgb(190,190,190)); 
		sun.setFill(Color.YELLOW);
		
		//create earth
		Circle earth = new Circle(500, 260, 18);
		earth.setStroke(Color.rgb(190,190,190)); 
		earth.setFill(Color.LIGHTBLUE);
		
		//create saturn
		Circle saturn = new Circle(130, 150, 20); 
		saturn.setStroke(Color.rgb(190,190,190)); 
		saturn.setFill(Color.ORANGERED );
		
		//create venus
		Circle venus = new Circle(470, 110, 15); 
		venus.setStroke(Color.rgb(190,190,190)); 
		venus.setFill(Color.BISQUE);
		
		//*********************************************************** 
		// Create the path for the objects 
		//***********************************************************
		Arc arcEarth = new Arc(300, 260, 200, 100, 0, 360);
		arcEarth.setStroke(Color.rgb(210,210,210));
		arcEarth.setFill(null);
		
		
		Arc arcSaturn = new Arc(320, 220, 200, 120, 180, 360); 
		arcSaturn.setStroke(Color.rgb(210,210,210));
		arcSaturn.setFill(null);
		arcSaturn.setRotate(20.0);
		
		
		Arc arcVenus = new Arc(340, 210, 170, 115, 0, 360); 
		arcVenus.setStroke(Color.rgb(210,210,210));
		arcVenus.setFill(null);
		arcVenus.setRotate(-35.0);
		
		
		PathTransition pt1 = new PathTransition();
		pt1.setInterpolator(Interpolator.LINEAR); 
		pt1.setDuration(Duration.millis(5000)); 
		pt1.setPath(arcEarth);
		pt1.setNode(earth);
		
		
		PathTransition pt2 = new PathTransition();
		pt2.setInterpolator(Interpolator.LINEAR);
		pt2.setDuration(Duration.millis(5000)); 
		pt2.setPath(arcSaturn); pt2.setNode(saturn);
		
		
		PathTransition pt3 = new PathTransition();
		pt3.setInterpolator(Interpolator.LINEAR);
		pt3.setDuration(Duration.millis(5000));
		pt3.setPath(arcVenus); 
		pt3.setNode(venus);
		
		
		//***********************************************************
		// Create the Transitions 
		//*********************************************************** 
		SequentialTransition seqTransition = new SequentialTransition(); 
		seqTransition.getChildren().addAll(pt1, pt2, pt3); 
		seqTransition.setCycleCount(Timeline.INDEFINITE); 
		seqTransition.setAutoReverse(false);
		
		
		ParallelTransition pTransition = new ParallelTransition();
		pTransition.getChildren().addAll(pt1, pt2, pt3);
		pTransition.setCycleCount(Timeline.INDEFINITE); 
		pTransition.setAutoReverse(false);
		//*********************************************************** 
		// Add the animation component to the animation pane 
		
		Pane paneAnimate = new Pane();
		paneAnimate.setMinSize(600, 400);
		paneAnimate.getChildren().addAll(sun,arcEarth, arcSaturn, arcVenus,
		earth, saturn, venus);
		//***********************************************************
		// Start Sequential Animation 
		//***********************************************************
		Button startSeqBtn = new Button("Start Sequential Animation");
		startSeqBtn.setOnAction((ActionEvent e) -> { 
			seqTransition.play();
		});
		//***********************************************************
		// Pause Sequential Animation //***********************************************************
		Button pauseSeqBtn = new Button("Pause Sequential Animation");
		pauseSeqBtn.setOnAction((ActionEvent e) -> {
		seqTransition.pause(); });
		//***********************************************************
		// Stop Sequential Animation //***********************************************************
		Button stopSeqBtn = new Button("Stop Sequential Animation"); 
		stopSeqBtn.setOnAction((ActionEvent e) -> {
		seqTransition.stop(); });
		//***********************************************************
		// Start Parallel Animation //***********************************************************
		Button startPBtn = new Button("Start Parallel Animation");
		startPBtn.setOnAction((ActionEvent e) -> {
		pTransition.play(); });
		//***********************************************************
		// Pause Parallel Animation //***********************************************************
		Button pausePBtn = new Button("Pause Parallel Animation"); 
		pausePBtn.setOnAction((ActionEvent e) -> {
		pTransition.pause(); });
		//***********************************************************
		// Stop Parallel Animation //***********************************************************
		Button stopPBtn = new Button("Stop Parallel Animation"); 
		stopPBtn.setOnAction((ActionEvent e) -> {
		pTransition.stop(); });

		//***********************************************************
		// Add the Sequential buttons to the hbS pane
		//*********************************************************** 
		HBox hbS = new HBox();
		hbS.setSpacing(10);
		hbS.setPadding(new Insets(10, 0, 0, 10)); 
		hbS.getChildren().addAll(startSeqBtn,pauseSeqBtn, stopSeqBtn);
		//*********************************************************** 
		// Add the Parallel buttons to the hbP pane
		//*********************************************************** 
		HBox hbP = new HBox();
		hbP.setSpacing(10);
		hbP.setPadding(new Insets(10, 0, 0, 10)); 
		hbP.getChildren().addAll(startPBtn,pausePBtn, stopPBtn);
		//***********************************************************
		// Add components to VBox 
		//*********************************************************** 
		VBox vb = new VBox();
		vb.setSpacing(7);
		vb.setPadding(new Insets(10, 0, 0, 10)); 
		vb.getChildren().addAll(paneAnimate, hbS, hbP);
		//*********************************************************** 
		// Prepare the stage 
		//***********************************************************
		Scene scene = new Scene (vb, 200, 200); stage.setScene(scene); stage.setTitle("Animation"); stage.setWidth(800); stage.setHeight(550);
		stage.show();

	}
}

