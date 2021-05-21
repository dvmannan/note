package com.example.one_note;

import android.content.Intent;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.support.v7.widget.LinearLayoutManager;
import android.support.v7.widget.RecyclerView;
import android.view.View;
import android.widget.TextView;

import com.example.one_note.data.databaseHelper;
import com.example.one_note.model.user;
import com.example.one_note.util.nrecyclerAdapter;

import java.util.List;

public class ALL extends AppCompatActivity implements nrecyclerAdapter.OnRowClickListener{

    RecyclerView nrecyclerview;
    nrecyclerAdapter nrecycleradapter;
    public List<user> noteList;
    TextView some;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_a_l_l);
        databaseHelper db = new databaseHelper(this);

        noteList = db.getuser();
        // Setting up notes recycler view
        nrecyclerview = findViewById(R.id.NRecyclerView);
        nrecycleradapter = new nrecyclerAdapter(noteList, this, this);
        nrecyclerview.setAdapter(nrecycleradapter);
        nrecyclerview.setLayoutManager(new LinearLayoutManager(this));

        // Check whether the note list is empty or not. If it's empty, show a text telling it
        some = findViewById(R.id.some);
        if (noteList.isEmpty()) some.setVisibility(View.VISIBLE);

    }

    @Override
    public void onItemClick(int position)
    {
        Intent intent = new Intent(ALL.this, UPDATION.class);
        intent.putExtra("note", noteList.get(position));
        startActivity(intent);
        finish();
    }
}
