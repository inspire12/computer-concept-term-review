# SharedPreference 

 xml 파일에 필요한 데이터를 <Key, Value> 로 저장하여 쉽게 읽고 쓰게 함 <br>
 주로 사용 : android에 최초실행 여부, 간단한 설정한 값(진동 여부) 등 <br>
 저장 가능 데이터 타입 : Boolean / String / Int / Float / Long <br>
 경로 data/data/패키지명/shared_prefs/SharedPreference 에 파일 저장

## 사용법 

데이터 저장
'''
val pref = getSharedPreference("mPref", MODE_PRIVATE) // 여러 엑티비티에서 사용 가능
val editor: SharedPreferences.Editor = pref.edit()
editor.putString("test", "TEST")
editor.commit() // 완료
'''
- MODE_PRIVATE : 자기 app 내에서 사용할때, 기본값
- MODE_WORLD_READABLE : 다른 app에서 읽기 가능
- MODE_WORLD_WRITEABLE : 다른 app에서 쓰기 가능

데이터 불러오기 
'''
val test: SharedPreferences = getSharedPreferences("test", MODE_PRIVATE);
firstData = test.getString("test");
'''

데이터 삭제 (xml)
1. 특정 데이터 삭제 
'''
editor.remove("test")
editor.commit()
'''
2. 모든 데이터 삭제 
'''
editor.clear()
editor.commit()
'''

Util화 
'''
// 선언
companipon object PreferencesUtil{
 
    fun setPreferences(Context context, String key, String value) {
        pref:SharedPreferences  = context.getSharedPreferences("pref", context.MODE_PRIVATE)
        editor:SharedPreferences.Editor  = pref.edit()
        editor.putString(key, value)
        editor.commit()
    }
 
    fun getPreferences(Context context, String key):String {
        SharedPreferences pref = context.getSharedPreferences("pref", context.MODE_PRIVATE)
        pref = context.getSharedPreferences("pref", context.MODE_PRIVATE)
        return pref.getString(key, "")
    }
}
 
//저장
PreferencesUtil.setPreferences(context, "ID", Strid);
PreferencesUtil.setPreferences(context, "PW", StrPw);
 
//불러오기
val ID= PreferencesUtil.getPreferences(context, "ID");
val Pw= PreferencesUtil.getPreferences(context, "Pw");
 
Log.d("PreferencesUtil", "ID: " + ID);
Log.d("PreferencesUtil", "Pw: " + Pw);
'''

### 참고사항 
[nive 블로그](http://nive.tistory.com/6)