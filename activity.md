#activity

<pre>
基本的页面单元。掌控着一群View控件的逻辑和生命周期。
简单的说的话，可以看成web开发中的一个html页面
</pre>

##生命周期
<img src="./img/1.gif"/>

Activity其实是继承了ApplicationContext这个类，我们可以重写以下方法
<pre>
public class Activity extends ApplicationContext {
        protected void onCreate(Bundle savedInstanceState){};        
        protected void onStart(){};           
        protected void onRestart(){};        
        protected void onResume(){};       
        protected void onPause(){};        
        protected void onStop(){};        
        protected void onDestroy(){};
}
</pre>

<ul>
  <li>打开应用时先后执行了onCreate()->onStart()->onResume()三个方法</li>
  <li>按BACK键时，这个应用程序将结束，应用将先后调用onPause()->onStop()->onDestory()三个方法</li>
  <li>按HOME键时，Activity先后执行了onPause()->onStop()这两个方法</li>
  <li>再次重新打开应用时，Activity先后执行了onRestart()->onStart()->onResume()这三个方法</li>
</ul>

例：
<pre>
public class ActivityDemo extends Activity {
    
    private static final String TAG = "ActivityDemo";
    private EditText mEditText;
    //定义一个String 类型用来存取我们EditText输入的值
    private String mString;
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        mEditText = (EditText)findViewById(R.id.editText);
        Log.e(TAG, "start onCreate~~~");
    }
     
    @Override
    protected void onStart() {
        super.onStart();
        Log.e(TAG, "start onStart~~~");
    }
    //当按HOME键时，然后再次启动应用时，我们要恢复先前状态
    @Override
    protected void onRestart() {
        super.onRestart();
        mEditText.setText(mString);
        Log.e(TAG, "start onRestart~~~");
    }
     
    @Override
    protected void onResume() {
        super.onResume();
        Log.e(TAG, "start onResume~~~");
    }
     
    //当我们按HOME键时，我在onPause方法里，将输入的值赋给mString
    @Override
    protected void onPause() {
        super.onPause();
        mString = mEditText.getText().toString();
        Log.e(TAG, "start onPause~~~");
    }
     
    @Override
    protected void onStop() {
        super.onStop();
        Log.e(TAG, "start onStop~~~");
    }
     
    @Override
    protected void onDestroy() {
        super.onDestroy();
        Log.e(TAG, "start onDestroy~~~");
    }
     
}
</pre>





