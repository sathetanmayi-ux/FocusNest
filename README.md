package com.example.dailydoc;

import static androidx.core.content.ContextCompat.startActivity;

import android.content.Intent;
import android.os.Bundle;
import android.provider.Settings;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    EditText inputMinutes;
    Button btnStart, btnHistory;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        inputMinutes = findViewById(R.id.inputMinutes);
        btnStart = findViewById(R.id.btnStart);
        btnHistory = findViewById(R.id.btnHistory);

        btnStart.setOnClickListener(v -> {
            String s = inputMinutes.getText().toString().trim();
            if (s.isEmpty()) {
                Toast.makeText(this, "Enter minutes", Toast.LENGTH_SHORT).show();
                return;
            }
            int mins;
            try {
                mins = Integer.parseInt(s);
                if (mins <= 0) throw new NumberFormatException();
            } catch (NumberFormatException e) {
                Toast.makeText(this, "Invalid minutes", Toast.LENGTH_SHORT).show();
                return;
            }
            Intent intent = new Intent(MainActivity.this, FocusActivity.class);
            intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK | Intent.FLAG_ACTIVITY_CLEAR_TASK);
            intent.putExtra("minutes", mins);
            intent.putExtra("duration", mins * 60 * 1000L);
            startActivity(intent);
        });

        btnHistory.setOnClickListener(v -> startActivity(new Intent(this, HistoryActivity.class)));
    }
}

