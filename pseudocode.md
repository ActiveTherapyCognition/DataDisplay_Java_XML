# **TotalPTConnect**

### **Questions**
1. What is the structure and naming convention of the array of objects coming from the back end?
2. Is it most efficient and practical to use MPAndroidCharts or draw the data to the screen without using a library? (Loading time)
3. What needs to be imported to draw to canvas manually?

### **Concept**
TotalPTConnect is a native android application that is written in Java using Android Studio.

### **MVP**
Build a Java class that accepts an array of objects, and displays data to the screen in the form of a bar graph.

#### Initial page load view:
**Top Logo**

**Back Button**

**Top Nav**

**Chart**
- M-S labels (x-axis) below chart (7 days)
- Numeric value labels on left side (y-axis) of chart (0 - ?)
		- (0 - dynamic/responsive to max value + 10)
- Dynamically drawn bar for each day of current week (7 bars)

**Sub Nav**

**Numeric/Statistic Display**
- Total Daily Steps
	- Total Number
- Time in Vigorous Exercise
	- Total Number + “mins”
- Heart Rate Range
	- Total Number
- Time in Vigorous Exercise
	- Total Number + “mins”

**Numeric display repeats in desc date order down y-axis 



### **User Actions:**
When the user clicks any one of these affordances, call for data is made and views are rendered dynamically.

**BACK:** Navigates user to previous view state
**Top Nav**
- BP button
- Steps button
- Sleep button
- Workouts button
**Date Nav**
- Week back button
- Week forward button
- Month back button
- Month Forward button
**Sub Nav**
- Total Daily Steps button
- Heart Rate Range button

 
### **DevOps**
- Database/Data Structure: ?
- Java
- XML
- Android Studio
- MPAndroidCharts

## **PROCEDURAL**

## **IMPORTS**
**build.gradle**
	`implementation 'com.github.PhilJay:MPAndroidChart:v3.1.0'`

## **JAVA**
### **MainActivity.java**
	import android.os.Bundle;
	import android.view.View;
	import android.widget.Button;

	import androidx.appcompat.app.AppCompatActivity;`

	public class MainActivity extends AppCompatActivity implements View.OnClickListener {
		private ArrayList<StepData> stepDataList;
		private Button btnBP, btnSteps, btnSleep, btnWorkouts, btnTotalSteps, btnHeartRate;

	    @Override
	    protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);
		
		// Initialize step data
		initializeStepData();
	    

		// Initialize buttons
		btnBP = findViewById(R.id.btn_bp);
		btnSteps = findViewById(R.id.btn_steps);
		btnSleep = findViewById(R.id.btn_sleep);
		btnWorkouts = findViewById(R.id.btn_workouts);
		btnTotalSteps = findViewById(R.id.btn_total_steps);
		btnHeartRate = findViewById(R.id.btn_heart_rate);

		// Set click listeners
		btnBP.setOnClickListener(this);
		btnSteps.setOnClickListener(this);
		btnSleep.setOnClickListener(this);
		btnWorkouts.setOnClickListener(this);
		btnTotalSteps.setOnClickListener(this);
		btnHeartRate.setOnClickListener(this);
	    }
	    
	    // Hardcoded daily step values (should be dynamic)
	    private void initializeStepData() {
		stepDataList = new ArrayList<>();
		stepDataList.add(new StepData("Mon", 5000));
		stepDataList.add(new StepData("Tue", 6000));
		stepDataList.add(new StepData("Wed", 7000));
		stepDataList.add(new StepData("Thu", 5500));
		stepDataList.add(new StepData("Fri", 8000));
		stepDataList.add(new StepData("Sat", 9000));
		stepDataList.add(new StepData("Sun", 7500));
		    }
	     
	    private void displayStepBarChart() {
		// Create the bar entries
		ArrayList<BarEntry> barEntries = new ArrayList<>();
		for (int i = 0; i < stepDataList.size(); i++) {
		    StepData stepData = stepDataList.get(i);
		    barEntries.add(new BarEntry(i, stepData.getStepCount()));
		}

		// Create the bar dataset
		BarDataSet barDataSet = new BarDataSet(barEntries, "Step Count");
		barDataSet.setColor(Color.rgb(255, 165, 0)); // Orange color

		// Create the bar data object
		BarData barData = new BarData(barDataSet);
		barData.setBarWidth(0.5f);

		// Get the reference to the bar chart view
		BarChart barChart = findViewById(R.id.bar_chart);

		// Set the bar data to the chart
		barChart.setData(barData);

		// Customize the appearance of the bar chart
		barChart.setBackgroundColor(Color.DKGRAY);
		barChart.setDrawGridBackground(false);
		barChart.getDescription().setEnabled(false);

		// Customize the X-axis labels
		XAxis xAxis = barChart.getXAxis();
		xAxis.setPosition(XAxis.XAxisPosition.BOTTOM);
		xAxis.setValueFormatter(new IndexAxisValueFormatter(getXAxisLabels()));

		// Customize the Y-axis labels
		YAxis yAxisLeft = barChart.getAxisLeft();
		yAxisLeft.setTextColor(Color.WHITE);
		yAxisLeft.setGranularity(1f);
		yAxisLeft.setAxisMinimum(0f);

		// Refresh the chart
		barChart.invalidate();
	    }

	    @Override
	    public void onClick(View view) {
		// Handle button clicks
		switch (view.getId()) {
		    case R.id.btn_bp:
			// Handle BP button click
			break;
		    case R.id.btn_steps:
			// Handle Steps button click
			displayStepBarChart();
			break;
		    case R.id.btn_sleep:
			// Handle Sleep button click
			break;
		    case R.id.btn_workouts:
			// Handle Workouts button click
			break;
		    case R.id.btn_total_steps:
			// Handle Total Steps button click
			break;
		    case R.id.btn_heart_rate:
			// Handle Heart Rate button click
			break;
		}
	    }
	}

### **StepData.java**
	public class StepData {
	    private String date;
	    private int stepCount;

	    public StepData(String date, int stepCount) {
		this.date = date;
		this.stepCount = stepCount;
	    }

	    public String getDate() {
		return date;
	    }

	    public int getStepCount() {
		return stepCount;
	    }
	}



## **XML**
	<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    xmlns:tools="http://schemas.android.com/tools"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent"
	    tools:context=".MainActivity">

	    <!-- Logo at the top -->
	    <ImageView
		android:id="@+id/image_logo"
		android:layout_width="wrap_content"
		android:layout_height="wrap_content"
		android:src="@drawable/logo"
		android:layout_marginTop="16dp"
		android:layout_centerHorizontal="true"/>

	    <!-- Back button on top left -->
	    <Button
		android:id="@+id/btn_back"
		android:layout_width="wrap_content"
		android:layout_height="wrap_content"
		android:text="Back"
		android:layout_alignParentStart="true"
		android:layout_marginStart="16dp"
		android:layout_marginTop="16dp"/>

	    <!-- Horizontal top navigation -->
	    <LinearLayout
		android:id="@+id/layout_top_navigation"
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:orientation="horizontal"
		android:layout_below="@id/image_logo"
		android:padding="16dp">

		<!-- BP button -->
		<Button
		    android:id="@+id/btn_bp"
		    android:layout_width="0dp"
		    android:layout_height="wrap_content"
		    android:layout_weight="1"
		    android:text="BP"/>

		<!-- Steps button -->
		<Button
		    android:id="@+id/btn_steps"
		    android:layout_width="0dp"
		    android:layout_height="wrap_content"
		    android:layout_weight="1"
		    android:text="Steps"/>

		<!-- Sleep button -->
		<Button            android:id="@+id/btn_sleep"
		    android:layout_width="0dp"
		    android:layout_height="wrap_content"
		    android:layout_weight="1"
		    android:text="Sleep"/>

		<!-- Workouts button -->
		<Button
		    android:id="@+id/btn_workouts"
		    android:layout_width="0dp"
		    android:layout_height="wrap_content"
		    android:layout_weight="1"
		    android:text="Workouts"/>
	    </LinearLayout>

	    <!-- Area for MPAndroidChart data -->
	    <FrameLayout
		android:id="@+id/chart_container"
		android:layout_width="match_parent"
		android:layout_height="200dp"
		android:layout_below="@id/layout_top_navigation"
		android:layout_marginTop="16dp"
		android:background="@android:color/darker_gray"/>

	    <!-- Sub navigation -->
	    <LinearLayout
		android:id="@+id/layout_sub_navigation"
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:orientation="horizontal"
		android:layout_below="@id/chart_container"
		android:padding="16dp">

		<!-- Total Steps button -->
		<Button
		    android:id="@+id/btn_total_steps"
		    android:layout_width="0dp"
		    android:layout_height="wrap_content"
		    android:layout_weight="1"
		    android:text="Total Steps"/>

		<!-- Heart Rate button -->
		<Button
		    android:id="@+id/btn_heart_rate"
		    android:layout_width="0dp"
		    android:layout_height="wrap_content"
		    android:layout_weight="1"
		    android:text="Heart Rate"/>
	    </LinearLayout>

	    <!-- Text labels and numeric statistics -->
	    <LinearLayout
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:orientation="vertical"
		android:layout_below="@id/layout_sub_navigation"
		android:padding="16dp">

		<!-- Text label 1 -->
		<TextView
		    android:layout_width="match_parent"
		    android:layout_height="wrap_content"
		    android:text="Label 1"/>

		<!-- Numeric statistic 1 -->
		<TextView
		    android:layout_width="match_parent"
		    android:layout_height="wrap_content"
		    android:text="Statistic 1"/>

		<!-- Text label 2 -->
		<TextView
		    android:layout_width="match_parent"
		    android:layout_height="wrap_content"
		    android:text="Label 2"/>

		<!-- Numeric statistic 2 -->
		<TextView
		    android:layout_width="match_parent"
		    android:layout_height="wrap_content"
		    android:text="Statistic 2"/>
	    </LinearLayout>

	</RelativeLayout>
`





