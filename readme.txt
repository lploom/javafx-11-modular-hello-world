// compile
javac --module-path C:\javafx-sdk-11\lib --module-source-path src --module hellomodule -d build

// run
java --module-path C:\javafx-sdk-11\lib;build --module hellomodule/com.ameus.Main

// create jar
jar --create --file build\HelloWorld.jar -C build\hellomodule .

// view jar contents
jar tf build\HelloWorld.jar

// view jar module info
jar --describe-module --file build\HelloWorld.jar

// run jar
java --module-path C:\javafx-sdk-11\lib;build\HelloWorld.jar -m hellomodule/com.ameus.Main

// create custom jre containing only the required modules
jlink --module-path "%JAVA_HOME%\jmods;C:\javafx-jmods-11;build\hellomodule" --add-modules hellomodule --launcher start=hellomodule/com.ameus.Main --output dist

// create another jre (compressed, smaller, suitable for production)
jlink --module-path "%JAVA_HOME%\jmods;C:\javafx-jmods-11;build\hellomodule" --add-modules hellomodule --launcher start=hellomodule/com.ameus.Main --output dist-compressed --compress 2 --no-header-files --no-man-pages --strip-debug

// run with the new jre using the launcher script we created in previous command
dist\bin\start
