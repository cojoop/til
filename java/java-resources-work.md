# 자바 리소스 작업

`Java`에서 리소스 관리는 중요한 주제 중 하나입니다. 특히 파일, 네트워크 연결, 데이터베이스 연결과 같은 외부 자원들을 다룰 때는 이를 올바르게 관리해야 합니다. 이를 위해 `Java`는 자동 리소스 닫기(`Automatic Resource Management`)를 제공합니다.

## 자바에서의 리소스 작업

리소스 작업은 다양한 형태로 나타날 수 있다.
> 가장 흔한 예는 파일을 읽거나 쓰는 작업

```java
// 파일을 읽어들이는 예제 코드
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class FileReadExample {
    public static void main(String[] args) {
        try {
            BufferedReader reader = new BufferedReader(new FileReader("example.txt"));
            String line = null;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

- 파일을 읽어들이기 위해 `BufferedReader`를 사용합니다.

이 코드에는 한 가지 문제가 있습니다. `BufferedReader`를 사용한 후에는 `close()` 메서드를 호출하여 리소스를 명시적으로 닫아주어야 합니다. 그렇지 않으면 메모리 누수와 같은 문제가 발생할 수 있습니다.

## 자동 리소스 닫기(Automatic Resource Management)

`try-with-resources` 문을 통해 자동 리소스 닫기 기능을 제공합니다. 이를 활용하면 코드를 더 간결하게 작성할 수 있고, 리소스를 명시적으로 닫아주는 번거로움을 줄일 수 있습니다.

위의 예제를 `try-with-resources` 문으로 수정하면 다음과 같습니다.

```java

import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class FileReadExample {
    public static void main(String[] args) {
        try (BufferedReader reader = new BufferedReader(new FileReader("example.txt"))) {
            String line = null;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

- `try-with-resources` 문을 사용하면 `BufferedReader`를 초기화한 후에 자동으로 닫아줍니다.

> 자동 리소스 닫기 기능을 활용하면 코드를 간결하게 작성하고, 리소스 관리에 대한 부담을 줄일 수 있습니다. 하지만 자동 리소스 닫기를 사용할 때에도 예외 처리에 주의해야 합니다.
