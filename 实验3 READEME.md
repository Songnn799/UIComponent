# 实验3_UI组件

首先是导航页面，每个按钮分别跳转到不同的界面演示不同UI组件的用法：

1.SimpleAdapter

2.自定义对话框

3.xml文件定义菜单

4.ACtionMode形式的上下文菜单

![导航界面](https://note.youdao.com/yws/api/personal/file/8029EA744DC3469A9CBEA2C8DBE0DCA6?method=download&shareKey=5d693aadcd67ad0d4246cd351c6a9b73) 



## SimpleAdapter
![SimpleAdapter](https://note.youdao.com/yws/api/personal/file/00FE7685796C4390A9AC52181E540ED6?method=download&shareKey=1c5e8d95c83891b0ff36f53a58da2429)

本界面演示了SimpleAdapter用来装配ListView的用法。ListView每个Item的布局采用相对布局，包含一个ImageView和一个TextView，并且指定ImageView对齐父类布局的右侧。

**注意：ListView条目单击显示颜色可以指定其listSelector属性。** 

    <ListView
        android:id="@+id/simpleListView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:divider="#000"
        android:dividerHeight="2dp"
        android:listSelector="#600"/>
        
**使用Toast显示选中的列表项信息**
```java
simpleListView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> adapterView, View view, int i, long l) {
                Toast.makeText(getApplicationContext(),animalName[i],Toast.LENGTH_LONG).show();//show the selected image in toast according to position
            }
        });
```
## 自定义对话框的实现
![CustomDialog](https://note.youdao.com/yws/api/personal/file/7F91C70D7DAA4A2693643019DF1C500D?method=download&shareKey=d31cf885c79f3346e4876f2eb6f2ecd8)

**自定义对话框使用getLayoutInflater()获取LayoutInflater实例，并利用LayoutInflater的inflate()方法从自定义布局文件中加载对话框的布局，从而实现自定义对话框。对话框的布局如下：**

    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    	android:orientation="vertical"
    	android:layout_width="wrap_content"
    	android:layout_height="wrap_content">
	    <ImageView
	        android:src="@drawable/header_logo"
	        android:layout_width="match_parent"
	        android:layout_height="64dp"
	        android:scaleType="center"
	        android:background="#FFFFBB33"
	        android:contentDescription="@string/app_name" />
	    <EditText
	        android:id="@+id/username"
	        android:inputType="textEmailAddress"
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:layout_marginTop="16dp"
	        android:layout_marginLeft="4dp"
	        android:layout_marginRight="4dp"
	        android:layout_marginBottom="4dp"
	        android:hint="@string/username" />
	    <EditText
	        android:id="@+id/password"
	        android:inputType="textPassword"
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:layout_marginTop="4dp"
	        android:layout_marginLeft="4dp"
	        android:layout_marginRight="4dp"
	        android:layout_marginBottom="16dp"
	        android:fontFamily="sans-serif"
	        android:hint="@string/password"/>
    </LinearLayout>
    
**java代码如下：**
```java
public class CustomDialog extends Activity {


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_custom_dialog);
        Button btn_custom_dialog = (Button)findViewById(R.id.custom_dialog_btn);
        btn_custom_dialog.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                createDialog();
            }
        });
    }

    public void createDialog() {
        AlertDialog.Builder builder = new AlertDialog.Builder(this);
        // Get the layout inflater
        LayoutInflater inflater = getLayoutInflater();

        // Inflate and set the layout for the dialog
        // Pass null as the parent view because its going in the dialog layout
        builder.setView(inflater.inflate(R.layout.custom_dialog, null))
                // Add action buttons
                .setPositiveButton(R.string.signin, new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialog, int id) {
                        // sign in the user ...
                    }
                })
                .setNegativeButton(R.string.cancel, new DialogInterface.OnClickListener() {
                    public void onClick(DialogInterface dialog, int id) {
                        //LoginDialogFragment.this.getDialog().cancel();
                    }
                });
        builder.create();
        builder.show();
    }

}
```
## 使用XML定义菜单
![XmlDefineMenu01](https://note.youdao.com/yws/api/personal/file/B4A10F150E8D4DDF96A5F3FB27F0E854?method=download&shareKey=920169f3ecadf5a0703f76a7edf8dcc2)   
![XmlDefineMenu02](https://note.youdao.com/yws/api/personal/file/94E69E9723C4411BB861D9DDD9EE1576?method=download&shareKey=6a9a2b674aced1b766c76d2827b7871f)   
![XmlDefineMenu03](https://note.youdao.com/yws/api/personal/file/5AE5F522BE604ACFBB8035C7E2193331?method=download&shareKey=16c49cba65a674d93c29a299295c340d)   


**在res文件夹下新建menu文件夹，并新建一个xml文件来定义菜单，具体的XML文件内容:**

    <menu xmlns:android="http://schemas.android.com/apk/res/android">
	    <item android:title="@string/menu_Font">
	        <menu>
	            <item
	                android:id="@+id/menu_font_small"
	                android:title="@string/menu_font_small"/>
	            <item
	                android:id="@+id/menu_font_middle"
	                android:title="@string/menu_font_middle"/>
	            <item
	                android:id="@+id/menu_font_big"
	                android:title="@string/menu_font_big"/>
	        </menu>
	
	    </item>
	    <item
	        android:id="@+id/menu_normal"
	        android:title="@string/menu_Normal">
	    </item>
	    <item android:title="@string/menu_Color">
	        <menu>
	            <item
	                android:id="@+id/menu_color_red"
	                android:title="@string/menu_color_red" />
	            <item
	                android:id="@+id/menu_color_black"
	                android:title="@string/menu_color_black"/>
	        </menu>
	    </item>
    </menu>

**具体Java代码如下：**
```java
public class XmlDefineMenu extends Activity {
    TextView tv_test;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_xml_define_menu);
        tv_test = (TextView) findViewById(R.id.tv_test);
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        this.getMenuInflater().inflate(R.menu.menu_settings, menu);
        return true;
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        switch (item.getItemId()) {
            case R.id.menu_font_small:
                tv_test.setTextSize(10*2);
                break;
            case R.id.menu_font_middle:
                tv_test.setTextSize(16*2);
                break;
            case R.id.menu_font_big:
                tv_test.setTextSize(20*2);
                break;
            case R.id.menu_normal:
                Toast.makeText(XmlDefineMenu.this, "这是普通菜单项", Toast.LENGTH_SHORT).show();
                break;
            case R.id.menu_color_red:
                tv_test.setTextColor(Color.RED);
                break;
            case R.id.menu_color_black:
                tv_test.setTextColor(Color.BLACK);
                break;
        }
        return true;
    }
}

```
## 创建ActionMode模式的上下文菜单
![ActionModeContextMenu](https://note.youdao.com/yws/api/personal/file/60D8057668EC4A6DBBCA137D23DD508C?method=download&shareKey=5fd60d33b44c3e3b39fcbe38180d7710) 

在 ListView 或 GridView 中启用批处理上下文操作

如果在 ListView 或 GridView 中有一组项目（或 AbsListView 的其他扩展），且需要允许用户执行批处理操作，则应：

- 实现 AbsListView.MultiChoiceModeListener 接口，并使用 setMultiChoiceModeListener() 为视图组设置该接口。在侦听器的回调方法中，您既可以为上下文操作栏指定操作，也可以响应操作项目的点击事件，还可以处理从 ActionMode.Callback 接口继承的其他回调。
- 使用 CHOICE_MODE_MULTIPLE_MODAL 参数调用 setChoiceMode()。

Java代码如下：

    ListView listView = getListView();
    listView.setChoiceMode(ListView.CHOICE_MODE_MULTIPLE_MODAL);
    listView.setMultiChoiceModeListener(new MultiChoiceModeListener() {
    
	    @Override
	    public void onItemCheckedStateChanged(ActionMode mode, int position,
	                                          long id, boolean checked) {
	        // Here you can do something when items are selected/de-selected,
	        // such as update the title in the CAB
	    }
	
	    @Override
	    public boolean onActionItemClicked(ActionMode mode, MenuItem item) {
	        // Respond to clicks on the actions in the CAB
	        switch (item.getItemId()) {
	            case R.id.menu_delete:
	                deleteSelectedItems();
	                mode.finish(); // Action picked, so close the CAB
	                return true;
	            default:
	                return false;
	        }
	    }
	
	    @Override
	    public boolean onCreateActionMode(ActionMode mode, Menu menu) {
	        // Inflate the menu for the CAB
	        MenuInflater inflater = mode.getMenuInflater();
	        inflater.inflate(R.menu.context, menu);
	        return true;
	    }
	
	    @Override
	    public void onDestroyActionMode(ActionMode mode) {
	        // Here you can make any necessary updates to the activity when
	        // the CAB is removed. By default, selected items are deselected/unchecked.
	    }
	
	    @Override
	    public boolean onPrepareActionMode(ActionMode mode, Menu menu) {
	        // Here you can perform updates to the CAB due to
	        // an invalidate() request
	        return false;
	    }
    });
