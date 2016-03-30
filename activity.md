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
        protected void onCreate(Bundle savedInstanceState){
          //onCreate()被调用时，Activity还不可见
        };        
        protected void onStart(){
          //onStart() 被调用时，Activity可能是可见了，但还不是可交互的
        };           
        protected void onRestart(){};        
        protected void onResume(){
                //在 Activity 从 Pause 状态转换到 Active 状态时被调用
        };       
        protected void onPause(){
                //Paused 当 Activity 被另一个透明或者 Dialog 样式的 Activity                  覆盖时的状态。此时它依然与窗口管理器保持连接，系统继续维护其内部状态，
                所以它仍然可见，但它已经失去了焦点故不可与用户交互。
        };        
        protected void onStop(){
                //当 Activity 被另外一个 Activity 覆盖、失去焦点并不可见时处于 Stoped 状态
        };        
        protected void onDestroy(){};
}
</pre>

<ul>
  <li>打开应用时先后执行了<b>onCreate()->onStart()->onResume()</b>三个方法</li>
  <li>按BACK键时，这个应用程序将结束，应用将先后调用<b>onPause()->onStop()->onDestory()</b>三个方法</li>
  <li>按HOME键时，Activity先后执行了<b>onPause()->onStop()</b>这两个方法</li>
  <li>再次重新打开应用时，Activity先后执行了<b>onRestart()->onStart()->onResume()</b>这三个方法</li>
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





