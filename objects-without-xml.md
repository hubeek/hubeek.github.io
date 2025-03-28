# Objects Without xml

_Status: Published_
_Created: 2018-03-15 07:01:35_
_Tags: Android Java_

in activity
<code>
@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
//        setContentView(R.layout.activity_main);


        DisplayMetrics displayMetrics = new DisplayMetrics();
        getWindowManager().getDefaultDisplay().getMetrics(displayMetrics);
        float height = displayMetrics.heightPixels;
        float width = displayMetrics.widthPixels;

        RelativeLayout myLayout = new RelativeLayout(this);
        myLayout.setBackgroundColor(Color.BLUE);

        Button myButton = new Button(this);
        myButton.setText("Press me");
        myButton.setBackgroundColor(Color.YELLOW);
        float w = (width*(float)0.3);
        myButton.setLayoutParams(new RelativeLayout.LayoutParams((int)w, (int)w));
        myButton.setX(width*(float)0.1);
        myButton.setY(width*(float)0.1);

        myLayout.addView(myButton);
        setContentView(myLayout);
    }
</code>