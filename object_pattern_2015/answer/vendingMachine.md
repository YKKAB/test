### 自動販売機の回答例

**(仕様)**

1. コンソールから金銭投入
  * 正の整数以外が入力されたら、エラーを返す。

1. 投入した金額に対して商品が光る(コンソールに表示させる)
1. ボタンを押す
1. 選んだ商品が出てくる(詳細を表示する)
1. おつりが出てくる


**(実装)**

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;


public class vendingMachineTest {

    public static void main(String[] args) {
        InputStreamReader isr = new InputStreamReader(System.in);
        BufferedReader reader = new BufferedReader(isr);

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
            } else if (isCorrectMoney(input)) {
                // 売買処理
                System.out.println(input);
            } else {
                // 入力エラー
                System.out.println("10円、50円、100円、500円、1000円以外はムリです。");
                System.out.println("お金を入れなおしてください。");
            }
        }
    }

    private static boolean isCorrectMoney(String input) {
        try {
            int money = Integer.parseInt(input);
            if (money == 10 || money == 50 || money == 100 || money == 500 || money == 1000) {
                return true;
            }
            return false;
        } catch (NumberFormatException e) {
            return false;
        }
    }

}

```
