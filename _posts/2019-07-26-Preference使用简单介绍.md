---
layout:     post
title:      Preference使用简单介绍
subtitle:   
date:       2019-07-26
author:     Mrlove
categories: Android
header-img: img/post-bg-mma-6.jpg
catalog: 	 true
tags:
    - Android
    - Preference
    
---
## Preference 使用简单介绍

------------

### Preference元素的通用XML Attributes说明：

- android:key ：  每个Preference控件独一无二的”ID”,唯一表示此Preference
- android:defaultValue ： 默认值。 例如，CheckPreference的默认值可为”true”，默认为选中状态；  EditTextPreference的默认值可为”110” 
- android:enabled ：      表示该Preference是否可用状态
- android:title ：        每个Preference在PreferenceScreen布局上显示的标题——大标题
- android:summary ：      每个Preference在PreferenceScreen布局上显示的标题——小标题(可以没有）
- android:persistent：    表示Preference元素所对应的值是否写入sharedPreferen文件中，如果是true，则表示写入；否则，则表示不写入该Preference元素的值
- android:dependency：    表示一个Preference(用A表示)的可用状态依赖另外一个Preference(用B表示)。B可用，则A可用；B不可用，则A不可用
- android:disableDependentsState：  与android:dependency相反。B可用，则A不可用；B不可用，则A可用

界面主要由PrefercenScreen、PreferenceCategory和Preference三个主要部分组成  
PrefercenScreen最根的部分;  
PreferenceCategory是每个设置的分组;  
Preference是具体到每个设置元素；
Preference 常用于APP设置模块，比如Android 系统中的Settings 模块  
如图所示：  
![GitHub](https://raw.githubusercontent.com/DoubleWay/DoubleWay.github.io/master/img/2019-07-26/2019-07-26-1.1.png)

### 常用Preference控件
- CheckBoxPreference
- EditTextPreference
- ListPreference
- PreferenceCategory
- RingtonePreference.

### Perference常用使用方法
- 使用XML定义Preference
 1. 将XML 文件保存在res/xml/目录中 例如：seeting.xml
 1. 继承PreferenceActivity在onCreate方法中直接调用
 3. addPreferencesFromResource(R.xml.seeting);添加布局    
 ![GitHub](https://raw.githubusercontent.com/DoubleWay/DoubleWay.github.io/master/img/2019-07-26/2019-07-26-1.2.png)

````
 SettingActivity extends PreferenceActivity
.................
@Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        addPreferencesFromResource(R.xml.seeting);
//addPreferencesFromResource    即给这个PreferenceActivity指定了一个xml
````
- 使用Fragment 片段定义Preference
1. 首先自定Fragment片段  
 a .自定义 SettingsFragment  
 b .preference 实现  布局文件  
````
 public class SettingsFragment extends PreferenceFragment {
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        // Load the preferences from an XML resource
        addPreferencesFromResource(R.xml.preference);
     //自定义 SettingsFragment
    }
}
````
 ![GitHub](https://raw.githubusercontent.com/DoubleWay/DoubleWay.github.io/master/img/2019-07-26/2019-07-26-1.3.png)
 2.  Activity 中调用Fragment  
 a .填充布局  

````
 <?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical" >
    <FrameLayout
        android:id="@+id/fm_pref"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
</LinearLayout>
````
 b .Activity 中调用Fragment  
````
 public class SettingPreferenceActivity extends Activity {
 //Activity 中调用Fragment
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        // TODO Auto-generated method stub
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_preference);
        getFragmentManager().beginTransaction()
                .replace(R.id.fm_pref, new SettingsFragment()).commit();
    }
}
````

### 常用方法
- getFragmentManager、getSupportFragmentManager其实获取的都是Activity里面的Fragment的管理器，getFragmentManager是Activtiy的方法，getSupportFragmentManager是FragmentActivity的方法，FragmentActivity是V4包的类，3.0系统之前先有的。

- getChildFragmentManager是Fragment中的方法，不管是app包还是v4包，都有的方法，获取的是当前这个Fragment中子一级的Fragment的管理器，比如Activity中有个Fragment，Fragment里面又有Fragment。
注意：Fragment中也有getFragmentManager，获取的是这个Fragment的管理器

- Preference相关的两个重要监听接口
 1. Preference.OnPreferenceChangeListener     该监听器的一个重要方法如下：
   boolean onPreferenceChange(Preference preference,Object objValue)
   说明：  当Preference的元素值发送改变时，触发该事件。
   
 2. Preference.OnPreferenceClickListener      该监听器的一个重要方法如下：
   public booleanonPreferenceClick(Preference preference)
   说明：当点击控件时触发发生，可以做相应操作。

那么当一个Preference控件实现这两个接口时，当被点击或者值发生改变时，触发方法是如何执行的呢?事实上，  
 它的触发规则如下：  
 1 先调用onPreferenceClick()方法，如果该方法返回true，则不再调用onPreferenceTreeClick方法   
 如果onPreferenceClick方法返回false，则继续调用onPreferenceTreeClick方法。  
 2 onPreferenceChange的方法独立与其他两种方法的运行。也就是说，它总是会运行。  

###  隐藏(删除) Preference
1. 先在xml布局里面删，然后在java里面删掉调用的相关部分，但如果很多地方都有调用，那么删除就很麻烦；
2. 用removePreference(Preference preference) 方法 删除；//推荐方法
如图：  
![GitHub](https://raw.githubusercontent.com/DoubleWay/DoubleWay.github.io/master/img/2019-07-26/2019-07-26-1.6.png)
````
((PreferenceGroup)findPreference("thirdC")).removePreference(findPreference("ttts"));//这是删除 二级节点
getPreferenceScreen().removePreference(findPreference("thirdC"));//这是 删除整个 一级节点
   ((PreferenceGroup)findPreference("thirdC")).removeAll();//这是 删除整个 一级节点下 所有的二级节点，但不会 删除 一级 节点的 节点名，
   // getPreferenceScreen().removePreference(findPreference("ttts"));//这样 无效，这样 只能删除一级节点
````
