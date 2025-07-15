# javac-
public
Android JNI 示例项目
 
一个展示 Android 中 Java 与 C++ 通过 JNI 交互的示例项目，包含基础的方法调用、数据传递等场景，适合初学者了解 JNI 开发流程。
 
功能说明
 
- Java 调用 C++ 方法（字符串返回、数值计算）
- C++ 反向调用 Java 方法
- 完整的 JNI 配置与编译流程
 
环境要求
 
- Android Studio 4.0+
- NDK 21.0+
- JDK 8+
- Android SDK 21+
 
项目结构
 
app/
├── src/
│   ├── main/
│   │   ├── java/com/example/jnidemo/
│   │   │   ├── MainActivity.java      // 主界面与调用示例
│   │   │   ├── NativeUtils.java       // 定义 native 方法
│   │   │   └── JavaUtils.java         // 供 C++ 调用的 Java 类
│   │   └── cpp/
│   │       └── native-lib.cpp         // C++ 实现代码
│   └── jni/                           // JNI 头文件目录
└── build.gradle                       // 项目配置（含 NDK 配置）
 
 
快速开始
 
1. 克隆本仓库到本地：
git clone https://github.com/yourusername/android-jni-demo.git
 
2. 用 Android Studio 打开项目
3. 等待 Gradle 同步完成
4. 连接 Android 设备或启动模拟器，点击运行按钮
 
核心代码示例
 
Java 调用 C++
 
// NativeUtils.java
public native String getHelloFromCpp();
public native int addNumbers(int a, int b);

// 调用方式
NativeUtils utils = new NativeUtils();
String cppStr = utils.getHelloFromCpp(); // 获取 C++ 返回的字符串
int result = utils.addNumbers(3, 5);    // 调用 C++ 计算 3+5
 
 
C++ 实现
 
// native-lib.cpp
JNIEXPORT jstring JNICALL
Java_com_example_jnidemo_NativeUtils_getHelloFromCpp(JNIEnv *env, jobject thiz) {
    return env->NewStringUTF("Hello from C++");
}

JNIEXPORT jint JNICALL
Java_com_example_jnidemo_NativeUtils_addNumbers(JNIEnv *env, jobject thiz, jint a, jint b) {
    return a + b;
}
 
 
注意事项
 
- 首次编译可能需要下载 NDK，请耐心等待
- 方法名必须严格遵循  Java_包名_类名_方法名  格式
- 字符串处理需注意 UTF-8 编码转换
- 复杂场景下建议使用线程避免阻塞 UI 主线程
 
许可证
 
本项目基于 MIT 许可证开源，详见 LICENSE 文件。
