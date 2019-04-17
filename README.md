实验目的
---
    使用PrefereceFragment实现设置页面
    设置项说明
    总共四组设置项
    In-line preferences 
        CheckBoxPreference
    Dialog-based preferences: 
        EditTextPreference 
        ListPreference 
    Launch preferences 
        PreferenceScreen: 跳转到另一个PreferenceScreen 
        PreferenceScreen: 启动一个网页
    Preference attributes 
        CheckBox: 父选项
        CheckBox: 子选项，当父选项勾选时呈现
关键代码
---
1.preferences.xml
```
<PreferenceScreen xmlns:android="http://schemas.android.com/apk/res/android">
    <PreferenceCategory
        android:title="In-line preferences">
        <CheckBoxPreference
            android:key="checkbox_preference"
            android:title="Checkbox preference"
            android:summary="This is a check box"/>
    </PreferenceCategory>
    <PreferenceCategory
        android:title="Dialog-based preferences">
        <EditTextPreference
            android:dialogTitle="Enter your favorite animal"
            android:key="edit_text_preference"
            android:title="Edit text preference"
            android:summary="An Example that uses an edit text dialog"/>
        <ListPreference
            android:dialogTitle="Choose one"
            android:entries="@array/setting"
            android:entryValues="@array/setting_value"
            android:key="list_preference"
            android:title="List preference"
            android:summary="An Example that uses a list dialog"/>
    </PreferenceCategory>
    <PreferenceCategory
        android:title="Launch preferences">
        <PreferenceScreen
            android:key="screen_preferences"
            android:title="Screen Preferences"
            android:summary="Shows another screen of preferences">
            <CheckBoxPreference
                android:key="toggle_preference"
                android:title="Toggle preference"
                android:summary="Preference that is on the next screen but same hierarchy"/>
        </PreferenceScreen>
        <PreferenceScreen
            android:title="Intent preference"
            android:summary="Launches an Activity from an Intent">
            <intent
                android:action="android.intent.action.VIEW"
                android:data="http://www.baidu.com"/>
        </PreferenceScreen>
    </PreferenceCategory>
    <PreferenceCategory
        android:title="Preference attribute">
        <CheckBoxPreference
            android:key="parent_checkbox_preference"
            android:title="Parent checkbox preference"
            android:summary="This is visually a parent"/>
        <CheckBoxPreference
            android:key="child_checkbox_preference"
            android:dependency="parent_checkbox_preference"
            android:title="Child checkbox preference"
            android:summary="This is visually a child"/>
    </PreferenceCategory>
</PreferenceScreen>
```
2.SettingsFragment.java
```
public class SettingsFragment extends PreferenceFragment {
    @Override
    public void onCreate(Bundle savedInstanceState){
        super.onCreate(savedInstanceState);
        addPreferencesFromResource(R.xml.preferences);
    }
}
```
3.MainActivity.java
```
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        //setContentView(R.layout.activity_main);
        getFragmentManager().beginTransaction()
                .replace(android.R.id.content, new SettingsFragment())
                .commit();
    }
}
```
结果截图
---
![image](https://github.com/YongxuanWu/PreferenceFragment/blob/master/app/src/main/res/pictures/IMG_20190417_155512.jpg)
![image](https://github.com/YongxuanWu/PreferenceFragment/blob/master/app/src/main/res/pictures/IMG_20190417_155535.jpg)
![image](https://github.com/YongxuanWu/PreferenceFragment/blob/master/app/src/main/res/pictures/IMG_20190417_155550.jpg)
![image](https://github.com/YongxuanWu/PreferenceFragment/blob/master/app/src/main/res/pictures/IMG_20190417_155602.jpg)
![image](https://github.com/YongxuanWu/PreferenceFragment/blob/master/app/src/main/res/pictures/IMG_20190417_155618.jpg)
![image](https://github.com/YongxuanWu/PreferenceFragment/blob/master/app/src/main/res/pictures/IMG_20190417_155636.jpg)
