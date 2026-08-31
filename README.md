# EX:NO:05: Develop a program to create a simple calculator using android studio.
## AIM:
To create and design an android application for a simple calculator using android studio.

## EQUIPMENTS REQUIRED: 
Android Studio(Latest Version)

## ALGORITHM:
Step 1: Open Android Studio and click on File → New → New Project.

Step 2: Enter the application name as Calculator, select the required Minimum SDK, and click Finish.

Step 3: Select Empty Activity and create the Android project.

Step 4: Design the calculator interface with number and operator buttons in activity_main.xml.

Step 5: Implement addition, subtraction, multiplication, division, clear, delete, and equals operations in MainActivity.java.

Step 6: Use Implicit Intent with ACTION_SEND to share the calculated result with other applications.

Step 7: Save and run the application, perform calculations, and verify the result and sharing functionality.

## PROGRAM:
```
Program to create and design an android application simple calculator using Intent.
Developed by: Vaishnavi S.A
Registeration Number : 212223220119
```

## MainActivity.java

```
package com.example.calculator;

import android.os.Bundle;
import android.widget.Button;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    TextView tvExpression, tvResult;

    String currentInput = "";
    double firstNumber = 0;
    String operator = "";
    boolean isNewInput = true;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        tvExpression = findViewById(R.id.tvExpression);
        tvResult = findViewById(R.id.tvResult);

        // Number buttons
        int[] numberButtons = {
                R.id.btn0, R.id.btn1, R.id.btn2, R.id.btn3, R.id.btn4,
                R.id.btn5, R.id.btn6, R.id.btn7, R.id.btn8, R.id.btn9
        };

        for (int id : numberButtons) {

            Button btn = findViewById(id);

            btn.setOnClickListener(v -> {

                if (isNewInput) {
                    currentInput = "";
                    isNewInput = false;
                }

                currentInput += btn.getText().toString();

                tvResult.setText(currentInput);
            });
        }

        // Operators
        findViewById(R.id.btnPlus)
                .setOnClickListener(v -> setOperator("+"));

        findViewById(R.id.btnMinus)
                .setOnClickListener(v -> setOperator("-"));

        findViewById(R.id.btnMultiply)
                .setOnClickListener(v -> setOperator("*"));

        findViewById(R.id.btnDivide)
                .setOnClickListener(v -> setOperator("/"));

        // Equals
        findViewById(R.id.btnEquals)
                .setOnClickListener(v -> calculate());

        // Clear
        findViewById(R.id.btnClear)
                .setOnClickListener(v -> clearCalculator());
    }

    private void setOperator(String op) {

        if (currentInput.isEmpty()) {
            return;
        }

        firstNumber = Double.parseDouble(currentInput);
        operator = op;

        tvExpression.setText(currentInput + " " + op);

        isNewInput = true;
    }

    private void calculate() {

        if (currentInput.isEmpty() || operator.isEmpty()) {
            return;
        }

        double secondNumber = Double.parseDouble(currentInput);
        double result = 0;

        switch (operator) {

            case "+":
                result = firstNumber + secondNumber;
                break;

            case "-":
                result = firstNumber - secondNumber;
                break;

            case "*":
                result = firstNumber * secondNumber;
                break;

            case "/":

                if (secondNumber == 0) {
                    tvResult.setText("Error");
                    clearValues();
                    return;
                }

                result = firstNumber / secondNumber;
                break;
        }

        tvExpression.setText(
                firstNumber + " " + operator + " " + secondNumber
        );

        if (result == (long) result) {
            tvResult.setText(String.valueOf((long) result));
            currentInput = String.valueOf((long) result);
        } else {
            tvResult.setText(String.valueOf(result));
            currentInput = String.valueOf(result);
        }

        isNewInput = true;
    }

    private void clearCalculator() {

        clearValues();

        tvExpression.setText("");
        tvResult.setText("0");
    }

    private void clearValues() {

        currentInput = "";
        firstNumber = 0;
        operator = "";
        isNewInput = true;
    }
}
```
## activity_main.xml

```
<?xml version="1.0" encoding="utf-8"?>

<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <TextView
        android:id="@+id/tvExpression"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text=""
        android:textSize="20sp"
        android:gravity="right"
        android:padding="10dp"/>

    <TextView
        android:id="@+id/tvResult"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="0"
        android:textSize="32sp"
        android:textStyle="bold"
        android:gravity="right"
        android:padding="10dp"/>

    <Button
        android:id="@+id/btnClear"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="CLEAR"/>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:id="@+id/btn7"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="7"/>

        <Button
            android:id="@+id/btn8"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="8"/>

        <Button
            android:id="@+id/btn9"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="9"/>

        <Button
            android:id="@+id/btnDivide"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="/"/>

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:id="@+id/btn4"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="4"/>

        <Button
            android:id="@+id/btn5"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="5"/>

        <Button
            android:id="@+id/btn6"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="6"/>

        <Button
            android:id="@+id/btnMultiply"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="*"/>

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:id="@+id/btn1"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="1"/>

        <Button
            android:id="@+id/btn2"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="2"/>

        <Button
            android:id="@+id/btn3"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="3"/>

        <Button
            android:id="@+id/btnMinus"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="-"/>

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:id="@+id/btn0"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="3"
            android:text="0"/>

        <Button
            android:id="@+id/btnEquals"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="="/>

        <Button
            android:id="@+id/btnPlus"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="+"/>

    </LinearLayout>

</LinearLayout>
```
## OUTPUT
<img width="1919" height="1020" alt="Screenshot 2026-08-21 094617" src="https://github.com/user-attachments/assets/15e9998a-c164-4169-b111-441da68cd097" />

<img width="1919" height="1025" alt="Screenshot 2026-08-21 094631" src="https://github.com/user-attachments/assets/b28019a9-0e6a-4d24-8d1d-bbe3b3f7ccdc" />


## RESULT
Thus a Simple Android Application create a simple calculator using Android Studio is developed and executed successfully.
