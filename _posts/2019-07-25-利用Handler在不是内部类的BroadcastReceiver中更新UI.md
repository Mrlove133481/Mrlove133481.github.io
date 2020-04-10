---
layout:     post
title:      利用Handler在不是内部类的BroadcastReceiver中更新UI
subtitle:   
date:       2019-07-25
author:     Mrlove
categories: Handler
header-img: img/post-bg-BJJ.jpg
catalog: 	 true
tags:
    - java
    - Handler
    
---
&emsp;&emsp;我们知道Receiver也是在主线程中运行的，如果将Receiver写成activity的内部类，可以直接在 onReceive（）方法中获得主线程的UI控件，对UI进行刷新，但是如果我们将Receiver写成单独的一个类，那这样就可能比较麻烦了，因为我们获取activity中的UI控件就变得困难。  
&emsp;&emsp;就算我们利用LayoutInflater.from(C).inflate(R.layout.mainframe,null)方法来获得布局和控件，但是这不是取得你的Context中的控件，而是将mainframe.xml中的控件创建出来一份，与原本的Context无关。所以这时候我就想到了利用handler来传递信息，在主线程中更新UI。  
&emsp;&emsp;我的目标是，在activity中发送一个广播，Receiver收到广播后，发送一个message，handler收到这个消息后，通过handlemessage（）方法对UI进行刷新，下面是我的源码：  
&emsp;&emsp;首先是界面的布局，在界面上就比较简单，点击按钮发送一个广播，然后textview的内容发生改变：  
````
<Button
    android:id="@+id/send_broadcast"
    android:text="send_broadcast"
    android:onClick="sendBroadcast"
    android:layout_width="match_parent"
    android:layout_height="wrap_content" />
    <TextView
        android:id="@+id/receiver_text"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:textSize="20dp"
        android:text="00000"
        />
`````
&emsp;&emsp;然后注册我们自己的Receiver，为了获得activity中的handler，提供一个构造方法，将handler传递过来。收到广播后通过handler发送mesage：  
`````
 public MyReceiver(Handler handler){
        this.handler=handler;
    }
    @Override
    public void onReceive(Context context, Intent intent) {
        // TODO: This method is called when the BroadcastReceiver is receiving
        // an Intent broadcast.
        Message message=new Message();
        message.what=1;
        message.obj="收到了广播";
        handler.sendMessage(message);
        Log.d(TAG, "onReceive: ++++++++++++");
    }
`````
&emsp;&emsp;最后是mainactivity，在mainactivity中发送广播，创建handler实例，收到message后，更新UI：  
`````
/*创建handler，在handlemessage中进行UI操作*/
 private TextView receiverText;
  private MyReceiver receiver;
  private String TAG="mainactivity";
  private  Handler handler=new Handler(){
      @Override
      public void handleMessage(@NonNull Message msg) {
          super.handleMessage(msg);
          Log.d(TAG, "handleMessage:+++++++++ ");
          switch (msg.what){
              case 1:
                  Log.d(TAG, "handleMessage:+++++++++ ");
                  receiverText.setText((String)msg.obj);
          }
      }
  };

 /*动态注册广播*/
        IntentFilter filter=new IntentFilter("com.example.receiver");
        receiver=new MyReceiver(handler);
        registerReceiver(receiver,filter);
/* 发送广播*/
  public void sendBroadcast(View v){
      Intent intent=new Intent("com.example.receiver");
      sendBroadcast(intent);

  }
``````
最后的效果如图所示：  
<div align="center">
	<img src="/img/2019-07-25/2019-07-25-1.1.png">  
</div>
<div align="center">
	<img src="/img/2019-07-25/2019-07-25-1.2.png">  
</div>

