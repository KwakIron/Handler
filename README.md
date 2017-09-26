# Handler
```
public class MainActivity extends AppCompatActivity {
    int imgids[] = {R.mipmap.s_1,R.mipmap.s_2,R.mipmap.s_3,R.mipmap.s_4
                    ,R.mipmap.s_5,R.mipmap.s_6,R.mipmap.s_7,R.mipmap.s_8};
    int imgStart = 0;
    boolean flag = true;
    ImageView imageView;
    final Handler HANDLER = new Handler(){
        @Override
        public void handleMessage(Message msg) {
            super.handleMessage(msg);
            if(msg.what == 100 & flag){
                imageView.setImageResource(imgids[imgStart++ % 8]);
                Log.e("ddddd","======="+imgStart);
            }
        }
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        imageView = (ImageView)findViewById(R.id.imageView);

            new Timer().schedule(new TimerTask() {
                @Override
                public void run() {
                    HANDLER.sendEmptyMessage(100);
                }
            }, 0, 300);


    }
    public void next(View view){
        Intent intent = new Intent(MainActivity.this,Handler2Activity.class);
        startActivity(intent);
        flag = false;
    }

    @Override
    protected void onResume() {
        super.onResume();
        flag = true;
    }
}
