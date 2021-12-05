# App
#Calculator
#Code này ở phần Layout activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="6dp"
    tools:context=".MainActivity">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="#009c2a"
        android:gravity="center_horizontal"
        android:text="Cộng trừ nhân chia"
        android:textColor="#ffffff"
        android:textSize="25sp"
        android:textStyle="bold" />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <TextView
            android:layout_width="80dp"
            android:layout_height="wrap_content"
            android:text="Số thứ nhất: " />

        <EditText
            android:id="@+id/etNumber1"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:inputType="number" />
    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <TextView
            android:layout_width="80dp"
            android:layout_height="wrap_content"
            android:text="Số thứ hai: " />

        <EditText
            android:id="@+id/etNumber2"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:inputType="number" />
    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center_horizontal"
        android:orientation="horizontal">

        <Button
            android:id="@+id/btnAddition"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="+" />

        <Button
            android:id="@+id/btnSubtraction"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="&#8722;" />

        <Button
            android:id="@+id/btnMultiplication"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="&#215;" />

        <Button
            android:id="@+id/btnDivision"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="&#247;" />
    </LinearLayout>

    <TextView
        android:id="@+id/tvResult"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="#009c2a"
        android:gravity="left"
        android:paddingLeft="5dp"
        android:paddingStart="5dp"
        android:text="Kết quả: 0"
        android:textColor="#ffffff"
        android:textSize="25sp"
        android:textStyle="bold" />

</LinearLayout>
#Class MainActivity
package levuduy.kotlinsimplecalculator

import android.support.v7.app.AppCompatActivity
import android.os.Bundle
import android.widget.Toast
import kotlinx.android.synthetic.main.activity_main.*

class MainActivity : AppCompatActivity() {
    var number1: Double = 0.0
    var number2: Double = 0.0
    var result: Double = 0.0

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        events()
    }

    private fun events() {
        btnAddition.setOnClickListener {
            cal("+")
        }

        btnSubtraction.setOnClickListener {
            cal("-")
        }

        btnMultiplication.setOnClickListener {
            cal("*")
        }

        btnDivision.setOnClickListener {
            cal("/")
        }
    }

    private fun cal(type: String) {
        tvResult.text = "Kết quả: 0"
        if (etNumber1.text.isEmpty()) {
            etNumber1.requestFocus()
            Toast.makeText(this@MainActivity, "Vui lòng nhập số thứ nhất", Toast.LENGTH_SHORT).show()
            return
        }

        if (etNumber2.text.isEmpty()) {
            etNumber2.requestFocus()
            Toast.makeText(this, "Vui lòng nhập số thứ hai", Toast.LENGTH_SHORT).show()
            return
        }

        number1 = etNumber1.text.toString().toDouble()
        number2 = etNumber2.text.toString().toDouble()

        result = when (type) {
            "+" -> number1 + number2
            "-" -> number1 - number2
            "*" -> number1 * number2
            "/" -> number1 / number2
            else -> 0.0
        }

        tvResult.text = "Kết quả: ${result.toString()}"
    }

}
