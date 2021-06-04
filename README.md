# Age-Calculator
A kotlin program to calculate your age

package com.aidencipher.ageinminutes

import android.app.DatePickerDialog
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.View
import android.widget.Button
import android.widget.TextView
import android.widget.Toast
import java.text.SimpleDateFormat
import java.util.*

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val button: Button = findViewById(R.id.thisbutton)
        button.setOnClickListener {view ->
            clickDatePicker(view)
        }
    }

    private fun clickDatePicker(view: View) {
        val myCalendar = Calendar.getInstance()
        val year = myCalendar.get(Calendar.YEAR)
        val month = myCalendar.get(Calendar.MONTH)
        val day = myCalendar.get(Calendar.DAY_OF_MONTH)
        val dpd = DatePickerDialog(this, DatePickerDialog.OnDateSetListener{
                view, selectedyear, selectedmonth, selecteddayOfMonth ->

            val selectedDate = "$selecteddayOfMonth/${selectedmonth+1}/$selectedyear"

            val tvSelectedDate = findViewById<TextView>(R.id.tvSelectedDate)
            tvSelectedDate.text = selectedDate

            val sdf = SimpleDateFormat("dd/MM/yyyy", Locale.ENGLISH)

            val theDate = sdf.parse(selectedDate)

            val selectedDateInMinutes = theDate!!.time / 60000

            val currentDate = sdf.parse(sdf.format(System.currentTimeMillis()))

            val currentDateToMinutes = currentDate!!.time / 60000

            val differenceInMinutes = currentDateToMinutes - selectedDateInMinutes

            val ageInDays = differenceInMinutes / 60 / 24 / 30 / 12

            val tvSelectedDateInMinutes = findViewById<TextView>(R.id.tvSelectedDateInMinutes)

            tvSelectedDateInMinutes.text = ageInDays.toString()


        }, year, month, day)
        dpd.datePicker.maxDate = Date().time - 86400000
        dpd.show()
    }
}
