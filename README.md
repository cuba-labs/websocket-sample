Example of WebSockets configuration for web module of CUBA application.
Based on the following Spring guide: https://spring.io/guides/gs/messaging-stomp-websocket/

* Add required dependencies to [build.gradle](build.gradle):

```groovy
configure(webModule) {

...
   
    dependencies {
        compile('org.springframework:spring-websocket:5.2.3.RELEASE')
        compile('org.springframework:spring-messaging:5.2.3.RELEASE')
        compile('com.fasterxml.jackson.core:jackson-databind:2.10.3')
``` 

* Turn on async support for `CubaDispatcherServlet` in the [web/WEB-INF/web.xml](modules/web/web/WEB-INF/web.xml):

```xml
    <servlet>
        <servlet-name>dispatcher</servlet-name>
        <servlet-class>com.haulmont.cuba.web.sys.CubaDispatcherServlet</servlet-class>
        <load-on-startup>1</load-on-startup>
        <async-supported>true</async-supported> 
    </servlet>
```
* Copy configuration and controller code from spring guide:
  * [modules/web/src/com/example/cubastomp/web/WebSocketConfig.java](modules/web/src/com/example/cubastomp/web/WebSocketConfig.java)
  * [modules/web/src/com/example/cubastomp/web/GreetingController.java](modules/web/src/com/example/cubastomp/web/GreetingController.java)

* Sample client side application is placed in [modules/web/web/VAADIN](modules/web/web/VAADIN) directory. Run CUBA app and find client-side app here: http://localhost:8080/cs/VAADIN/index.html

Pay attention to websocket endpoint address. Due to CUBA specifics it contains **dispatch** suffix:
```
var socket = new SockJS('/cs/dispatch/gs-guide-websocket');
```