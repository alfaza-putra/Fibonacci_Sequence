# Fibonacci_Sequence

Nama  : Alfaza putra adjie ariefiansyah

NIM   : 312210512

Kelas : TI.22.A5

Mata Kuliah : Pemrograman Mobile 1

Dosen Pengampu : Donny Maulana, S.Kom.,M.M.S.I.

Tugas : Buatlah Method Program java Toast Number, dengan menghasilkan Bilangan Fibonacci

## Daftar Isi
| No.| DAFTAR ISI |        Here                           |
|----|------------|----------------------------------------|
| 1. | Layout     | [Click Here](#layout)               |
| 2. | Java       | [Click Here](#java-class)     |
| 3. | Design     | [Click Here](#tampilan-design)      |
| 4. | Hasil Run  | [Click Here](#hasil-run)            |

> - Disini, saya akan mengerjakan dan menjelaskan tugas dari mata kuliah "Pemrograman Mobile 1" yaitu membuat sebuah aplikasi untuk menampilkan bilangan Fibonacci. Selain itu saya juga akan merubah sedikit tampilan dari yang diperintahkan pada tugas, yaitu menambah tombol `Restart` dan menambah tombol `Masukkan Angka Limit` 


## Layout
Pada layout ini, saya membuat tiga button dan satu textview :
1. `button_limit`, berfungsi sebagai tombol “Set Limit” yang nantinya ketika di tekan akan muncul sebuah pop-up untuk masukan limit angka yang ingin kita hitung.
2. `button_count`, berfungsi sebagai tombol “count” yang nantinya ketika tombol ditekan akan menghitung bilangan fibonaccinya sesuai dengan yang kita limit. Juga berbeda warna pada setiap angka, agar tidak keliru.
3. 'button_back', berfungsi sebagai tombol restart yang nantinya angka akan kembali ke awal.
4. Textview `show_count`, yang berfungsi untuk menampilkan angka atau bilangan fibonaccinya yang tepat berada di tengah.

Berikut adalah coding pada menu layout :

> - **activity_main.xml**
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">


    <Button
        android:id="@+id/numberMax"
        android:layout_width="199dp"
        android:layout_height="55dp"
        android:background="@color/colorPrimary"
        android:onClick="numberMax"
        android:text="NumMax"
        android:textColor="@color/white"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/button2"
        android:layout_width="199dp"
        android:layout_height="55dp"
        android:background="@color/colorPrimary"
        android:onClick="CountUP"
        android:text="Count"
        android:textColor="@color/white"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent"/>

    <TextView
        android:id="@+id/show_count"
        android:layout_width="407dp"
        android:layout_height="626dp"
        android:background="@color/yellow"
        android:gravity="center_vertical"
        android:text="0"
        android:textAlignment="center"
        android:textColor="@color/colorPrimary"
        android:textSize="160dp"
        android:textStyle="bold"
        app:layout_constraintBottom_toTopOf="@id/button2"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/numberMax"
        app:layout_constraintVertical_bias="1.0"
        tools:ignore=",Rtlcompat"/>

    <Button
        android:id="@+id/button3"
        android:layout_width="210dp"
        android:layout_height="56dp"
        android:background="@color/colorPrimary"
        android:onClick="Reset"
        android:text="Back"
        android:textColor="@color/white"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="1.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/show_count"
        app:layout_constraintVertical_bias="0.0"/>

    <EditText
        android:layout_width="207dp"
        android:layout_height="57dp"
        android:background="@drawable/custom_input"
        android:hint="Nama"
        android:paddingStart="12dp"
        android:textSize="15sp"
        tools:layout_editor_absoluteX="200dp"
        tools:layout_editor_absoluteY="-1dp"
        tools:ignore="ExtraText,MissingConstraints" />





</androidx.constraintlayout.widget.ConstraintLayout>
```

> - **Strings.xml**
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="app_name">Fibonacci</string>
    <string name="button_label_toast">Toast</string>
    <string name="button_label_count">Count</string>
    <string name="count_initial_value">0</string>
    <string name="coast_message">Welcome Toast</string>
    <string name="Reset">Reset</string>
</resources>
```

> - **Colors.xml**
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="black">#FF000000</color>
    <color name="white">#FFFFFFFF</color>
    <color name="colorPrimary">#0000FF</color>
    <color name="yellow">#FFFF00</color>
    <color name="muda">#00BCD4</color>
    <color name="green">#4CAF50</color>
</resources>/
```


## Java class
Pada Java class `MainActivity.java` berisi semua coding untuk menjalankan aplikasi. Seperti fungsi untuk tombol-tombol, dialog set limit, warna yang berbeda pada setiap angka, lalu warna background yang bisa berubah dan rumus bilangan fibonacci.
```
package com.example.fibonacci;

import androidx.appcompat.app.AppCompatActivity;

import android.annotation.SuppressLint;
import android.os.Bundle;
import android.view.View;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {
    private int count = 1;
    private TextView showCount;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        showCount = findViewById(R.id.show_count);
    }

    public void showToast(View view) {
        Toast toast = Toast.makeText(this, "Welcome Toast!", Toast.LENGTH_SHORT);
        toast.show();
    }

    @SuppressLint("SetTextI18n")
    public void CountUP(View view) {
        if (count < 0) {
            count = 0;
        }

        int result = generateFibonacci(count);

        if (result <= 1000) {
            showCount.setText(Integer.toString(result));
            count++;
        }
    }


    private int generateFibonacci(int n) {
        if (n <= 0) {
            return 0;
        } else if (n == 1) {
            return 1;
        }

        int first = 0;
        int second = 1;
        for (int i = 2; i <= n;  i++) {
            int next = first + second;
            first = second;
            second = next;
        }
        return first;

    }
    public void Reset(View view) {
        count = 1;
        showCount.setText("0");
    }
},
```


## Tampilan design



![Screenshot 2023-11-03 092237](https://github.com/syifaaurellia/DeretBilanganFibonacci/assets/129705943/a79edc4f-8a10-4b1d-b8a8-2e3f2640013b)

## Hasil Run 




https://github.com/syifaaurellia/DeretBilanganFibonacci/assets/129705943/b2579c6d-156c-48c6-9911-e0f44a777395

