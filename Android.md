Android

# android Activity

## Activity 的生命周期

![](https://img2018.cnblogs.com/blog/622972/201904/622972-20190423093912435-1195525192.png)

## Activity 的四种状态

==运行==状态：肉眼可见，也可操作

==暂停==状态：肉眼可见，不可操作

==停止==状态：肉眼不可见，但对象存在

==死亡==状态：对象被回收

# android 数据存储

## sp存储

- sp存储专门用来存储一些==单一的小数据==
- 可以存储的数据类型 boolean ,float ,int ,long ,String
- 存储路径：==/data/data/packageName/shared_prefs/xxx.xml==
- 可以设置==当前应用读取(私有)==，建议设置为私有
- ==应用卸载==时会删除数据

#### 相关api

- **SharedPreferences**: 对应SP文件接口
    - context.==getSharedPreferences==(String name, int mode) : 得到SP对象
        - name : 文件名(不带.xml)
        - mode : 生成的文件模式(是否是私有的)
    - sp.==edit()== : 得到 Editor 对象
    - sp.getXXX(String name, String defaultValue) : 根据name取相应的数据(defaultValue 默认值)
- \*\*Editor \*\*: 更新SP文件的接口
    - edit.put(name , value ) : 保存一个键值对，==此时没有实际保存到文件中==
    - edit.remove(name) : 根据name从文件中移除某个值
    - commit() : 提交，==此时才真正的保存到文件中==

## 手机内部文件存储

- 应用运行时需要一些==较大的数据或图片==可以使用文件保存在手机内部
- 文件类型：任意
- 文件保存的路径：==/data/data/packageName/files/==
- 可以设置为私有
- 应用卸载时会删除该文件

### 相关api

- 读取文件
    - FileInputStream fis = openFileInput("logo.png");
- 保存文件
    - FileOutputStream fos = openFileOutput("logo.png,MODE_PRIVATE");
- 得到files文件夹对象
    - File fileDir = getFileDir();
- 操作 asserts 下的文件
    - 得到 AssetManager：context.getAssets();
    - 读取文件：InputStream open(filename);
- 加载图片文件
    - Bitmap BitmapFactory.decodeFile(String pathName) (.bmp/.png/.jpg)

## SD卡file外部文件存储

- 手机==数据文件==可以保存到SD卡中
- 文件类型：任意
- 数据的保存路径：
    - 路径一：/storage/emulated/0/Android/data/packageName/files/
    - 路径二：/storage/emulated/0/xxx(==自己创建的文件夹==)/
- 路径一，其它应用可以访问，应用卸载时删除
- 路径二，其它应用可以访问，应用卸载时不会删除
- ==必须==保证==SD卡挂载在手机上==，才能访问读写

### 相关API：

- Environment：操作SD卡的工具类
    - 得到SD卡的状态： Environment.getExternalStorageState()
    - 得到SD卡的路径：Environment.getExternalStorageDirectory()
    - SD卡挂载状态值：Environment.MEDIA_MOUNTED
- context.getExternalFilesDir():
    - 得到/storage/emulated/0/Android/data/packageName/files/xxx.txt
- 操作SD卡的权限：（==“读的权限”可以不用写，加上“写的权限”就够了==）
    - android.permission.WRITE\_EXTERNAL\_STORAGE
    - android.permission.READ\_EXTERNAL\_STORAGE

## SQLite数据库存储

- 应用存储一些==具有一定结构的数据==，比如公司员工信息
- 文件类型：**.db**
- 文件的存储路径：==/data/data/PackageName/databases/xxx.db==
- 默认情况下，==其他应用无法访问==，可以提供ContentProvider提供其他应用操作
- 应用==卸载时会删除==该数据

### SQLite数据库命令行

- adb shell 进入系统根目录
- cd /data/data/databases: 进入包含数据库文件的文件夹中
- sqlite3 xxx.db：连接 xxx.db文件
- .help：查看命令列表
- .tables：查看所有表的列表
- .exit：退出数据库连接
- Ctrl + C ：退出 shell 模式

### SQLite语句

- 建表
  
    - 可以不用指定字段类型，但最好指定
      
    - 主键名称建议使用_id
      
        ```sqlite
        create table student(
               _id integer primary key autoincrement,
               name varchar,
               age int
        )
        ```
    
- 插入
  
    ```sqlite
    insert into student(name,age) values("TOM",10)
    ```
    
- 更新
  
    ```sqlite
    update student set age=14 where name="TOM"
    ```
    
- 查找
  
    ```sqlite
    select name from student where _id=1
    ```
    
- 删除
  
    ```sqlite
    delete from student where _id=1
    ```
    

### 相关API

- SQLiteOpenHelp：数据库操作的抽象帮助类
    - SQLiteOpenHelp(Context context ,String name ,CursorFactory factory ,int varsion) 构造方法，制定 ==数据库名== 和 ==版本号==
    - abstract void OnCreate(SQLiteDatabase db)：用于创建表（当数据库文件创建的时候就调用这个方法）
    - abstract void OnUpgrade()：用于版本更新
    - SQLiteDatabase getReadableDatabase()：得到数据库连接（==getWritableDatabase()，区别在与空间不足时候的处理，getWritableDatabase()会抛出异常，getReadableDatabase()不会做什么处理==）
- SQLiteDatabase：代表与数据库连接的类
    - long insert()：增，返回id值
    - int update()：改
    - int delete()：删
    - Cursor query()：查，返回包含结果数据的Cursor
    - void execSql(sql)：执行SQL语句
    - beginTransaction()：开启事务
    - setTransactionSuccessful()：设置事务是成功的
    - endTransaction()：结束事务，可能提交或回滚事务
    - openDatabase(String path ,CursorFactory factory ,int flags)：得到数据库连接
- Cursor：包含所有查询结果记录的结果集对象(光标,游标)
    - moveToNext()：指针指向下一个位置，如果有内容返回true
    - getInt(columnIndex : Int)：获取指定列数的内容
    - getString(columnIndex : Int)：获取指定列数的内容
    - getgetColumnIndex(colunmName: String)：获取指定名称的列的列序

# ContentProvider

## 理论概述

- ContentProvider是==四大应用组件==之一
- 当前应用使用ContentProvider==将数据库表数据操作暴露给其他应用访问==
- 其他应用需要使用==ContentResolver来调用==ContentProvider的方法
- 他们之间的调用是通过==Uri==来进行交流的

## 相关API

- **ContentProvider** : **内容提供者类**
    - public abstract boolean onCreate() : provider对象创建后调用（应用安装成功或手机启动完成）
    - Cursor query(Uri uri, String\[\] projection, String selection, String\[\] selectionArgs)（查询表数据）
    - Uri insert(Uri uri, ContentValues values)（插入表数据）
    - int delete(Uri uri, String selection, String\[\] selectionArgs)（删除表数据）
    - update(Uri uri, ContentValues values, String selection, String\[\] selectionArgs)（更新表数据）
- **ContentResolver : 内容提供者的解析类**
    - context.getContentResolver() （得到他的对象）
    - insert() 、delete()、update()、query()
    - registerContentObserver(Uri uri, boolean notify, ContentObserver observer)（注册uri的监听）
    - unregisterContentObserver(ContentObserver observer)（解注册uri的监听）
    - notifyChange(Uri uri, ContentObserver observer)（通知监听器）
- **Uri : 包含请求地址数据的类**
    - Uri static parse(String uriString)（得到其对象）
- **UriMatcher : 用于匹配Uri的容器**
    - void addURI(String authority, String path, int code)（添加一个合法的URI）
    - int match(Uri uri)（匹配制定的uri，返回匹配码）
- **ContentUris : 解析uri的工具类**
    - long parseId(Uri contentUri)（解析uri，得到其中的id）
    - Uri withAppendedId(Uri contentUri, long id)（添加id到指定的uri中）

# Android 动画

## 理论概述

- 动画的两种情况
  
    - 同一个图形通过==视图在界面上进行透明度，缩放，旋转，平移的变化==（View动画）
    - 在界面的==同一个位置上不断切换显示不同的图片==（Drawable动画）
- 动画的分类
  
    - View Animation
    - Drawable Animation
- Android 中提供了两种实现动画的方式
  
    - 纯编码的方式
    - Xml配置的方式

## View动画的分类

- 单一动画（Animation）
    - 缩放动画（ScaleAnimation）
    - 透明度动画（AlphaAnimation）
    - 旋转动画（RotateAnimation）
    - 平移动画（TranslateAnimation）
- 复合动画（AnimationSet）
    - 由多个单一动画组合在一起的动画

## Animation的公用功能

- setDuration(long durationMillis)：设置持续时间（单位ms）
  
- setStartOffset(long startOffset)：设置开始的延迟的时间（单位ms）
  
- setFillBefore(boolean fillBefore)：设置最终是否固定在起始状态
  
- setFillAfter(boolean fillAfter)：设置最终是否固定在最后的状态
  
- setAnimationListener(AnimationListener listener)：设置动画监听
  
- 坐标类型：
  
    - Animation.ABSOLUTE：绝对值
    - Animation.RELATIVE\_TO\_SELF：相对自己
    - Animation.RELATIVE\_TO\_PARENT：相对父亲
- 启动动画：view.startAnimation(animation)
  
- 结束动画：view.clearAnimation()
  
- 动画监听器：AnimationListener
  
    - onAnimationStart(Animation animation)：动画开始的回调
    - onAnimationEnd(Animaiton animation)：动画技术的回调
    - onNaimationRepeat(Animation animation)：动画重复执行

## 缩放动画（ScaleAnimation）

- fromX：开始时X轴上的缩放比例

- toX：结束时X轴上的缩放比例

- fromY：开始时Y轴上的缩放比例

- toY：结束时Y轴上的缩放比例

- pivotXType：X轴坐标的类型（计算X轴上的偏移量的方式）

- pivotXValue：中心点在X轴相对视图左顶点在X轴上的偏移量

- pivotYType：Y轴坐标的类型（计算X轴上的偏移量的方式）

- pivotYValue：中心点相对视图左顶点在y轴上的偏移量

  

## ViewPropertyAnimator

直接使用 View.animation()..... .start() 启动动画