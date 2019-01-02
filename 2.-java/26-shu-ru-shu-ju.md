### 导入java.io.\*包进行输入数据

```
import java.io.*;
public class input_demo {

    public static void main(String[] args) throws IOException {
        BufferedReader buf = new BufferedReader(new InputStreamReader(System.in));//创建buf对象
        String str = buf.readLine();//用readLine方法()读入字符串存入str中，且须处理IOException异常
        char c = (char) buf.read(); //读取一个字符
        System.out.println(str);
    }

}
```

### 导入java.util.\*包进行输入数据

```
import java.util.*;
public class input_demo2 {

    public static void main(String[] args) {
        Scanner sca = new Scanner(System.in);
        int a = sca.nextInt();
    }

}


相应的类型的数据读取方法:
nextByte()、nextDouble()、nextInt()、nextLong()、nextShort()、next()、nextLine()
```



