package com.example.user.colort2;

import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.Paint;
import android.graphics.drawable.ColorDrawable;
import android.util.AttributeSet;
import android.view.MotionEvent;
import android.view.View;
import android.widget.Toast;

import java.util.Random;

public class NewView extends View {
    int count = 4;
    int[][] tiles = new int[count][count];
    int darkColor = Color.GRAY;
    int brightColor = Color.YELLOW;
    int color = darkColor;
    int width, height, heightTile, widthTile;
    MainActivity activity;

    public NewView(Context context) {
        super(context);
        activity = (MainActivity) context;
        RandomColorTiles();
    }

    private void RandomColorTiles(){
        Random r = new Random();
        for (int i = 0; i < count; i++) {
            for (int j = 0; j < count; j++) {
                int c = r.nextBoolean() ? darkColor : brightColor;
                tiles[i][j] = c;
            }
        }
    }

    public NewView(Context context, AttributeSet attrs) {
        super(context, attrs);
    }

    @Override
    protected void onDraw(Canvas canvas) {
        //super.onDraw(canvas);
        width = canvas.getWidth();
        height = canvas.getHeight();
        Paint p = new Paint();
        int colori = 0;
        int colorj = 0;
        heightTile = height / count;
        widthTile = width / count;
        for (int i = 0; i < height - heightTile; i += heightTile) {
            for (int j = 0; j < width; j += widthTile) {
                int color = tiles[colori][colorj];
                p.setColor(color);
                canvas.drawRect(j, i, j + widthTile, i + heightTile, p);
                colorj++;
            }
            colori++;
            colorj = 0;
        }
    }

    private boolean win(){
        int color = tiles[0][0];
        for (int i = 0; i < count; i++){
            for (int j = 0; j < count; j++){
                if (tiles[i][j] != color)
                    return false;
            }
        }
        return true;
    }

    @Override
    public boolean onTouchEvent(MotionEvent event) {
        if (event.getAction() == MotionEvent.ACTION_DOWN) {
            int x = (int) event.getX();
            int y = (int) event.getY();
            x /= (width / count);
            y /= (height / count);
            for (int i = 0; i < count; i++) {
                tiles[y][i] = tiles[y][i] == brightColor ? darkColor : brightColor;
                tiles[i][x] = tiles[i][x] == brightColor ? darkColor : brightColor;
            }
            invalidate();
            if (win()) {
                Toast winner = Toast.makeText(activity, "WIN!", Toast.LENGTH_LONG);
                winner.show();
            }
        }
        return true;
    }
}
