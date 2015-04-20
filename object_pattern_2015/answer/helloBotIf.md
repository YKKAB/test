Main.java
```java
package test;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
    public static void main(String[] args) {
        InputStreamReader isr = new InputStreamReader(System.in);
        BufferedReader reader = new BufferedReader(isr);
        Hellobot bot = new Hellobot();

        // 「end」が入力されるまでループ
        while (true) {
            // コンソールから値を受け付ける処理
            String input = "";
            try {
                System.out.print(">");
                input = new String(reader.readLine().getBytes("UTF-8"));
            } catch (IOException e){
                System.out.println("入力エラー：" + e.getMessage());
                break;
            }

            // 入力判定
            if (input.equals("end")) {
                System.out.println("入力終了");
                break;
            } else {
                bot.say(input);
            }
        }

    }
}
```

Hellobot.java
```java
package test;

public class Hellobot {
    private int helloCount = 0;
    private int hiCount = 0;

    public void say(String input) {
        if (input.equals("Hello") || input.equals("hello")) {
            sayHello();
        } else if (input.equals("Hi") || input.equals("hi")) {
            sayHi();
        } else {
            System.out.println("なに？");
        }
    }
    
    private void sayHello() {
        if (hiCount == 2 && helloCount == 2) {
            System.out.println("おひさー");
        } else if (helloCount == 0) {
            System.out.println("おはー");
            helloCount = 1;
            hiCount = 1;
        } else if (helloCount == 1) {
            System.out.println("さっきもいった");
            helloCount++;
        } else {
            System.out.println("しつこいー");
            helloCount = 3;
        }
    }
    
    private void sayHi() {
        if ( (hiCount == 1 && helloCount == 2) || (hiCount == 1 && helloCount == 1) ) {
            System.out.println("おひさー");
            hiCount++;
        } else if (helloCount >= 3) {
            System.out.println("しつこいー");
        } else {
            System.out.println("おはー");
            helloCount = 1;
            hiCount = 1;
        }
    }
}
```
