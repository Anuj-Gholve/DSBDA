# B4 - Apache Scala

✅ Tested and working as intended.

---

1. Open your `Terminal` and run the following commands:

```shell
source ~/.bashrc # Not really needed but still
start-master.sh # Considering the shell script is defined in PATH
spark-shell # This will start scala CLI
```

2. Enter paste mode:

```scala
:paste
```

3. Paste the following code:

```scala
object EvenOddCheck {
  def main(args: Array[String]): Unit = {
    val number = 15
    if (number % 2 == 0) {
      println(s"$number is even")
    } else {
      println(s"$number is odd")
    }
  }
}
```

> [!NOTE]
> IF USER INPUT REQUIRED, USE THIS CODE INSTEAD:

```scala
import scala.io.StdIn

object AddTwoNumbers {
  def main(args: Array[String]): Unit = {
    println("Enter the first number:")
    val num1 = StdIn.readInt()
    println("Enter the second number:")
    val num2 = StdIn.readInt()
    val sum = num1 + num2
    println(s"The sum of $num1 and $num2 is $sum")
  }
}
```

4. Press `Ctrl + D` to exit paste mode

5. Execute:

```scala
EvenOddCheck.main(Array.empty[String])
```

> [!NOTE]
> TO EXECUTE USER INPUT WALA CODE, RUN:

```scala
AddTwoNumbers.main(Array.empty[String])
```

> [!TIP]
> Additional Scala codes available at [here](https://git.kska.io/sppu-te-comp-content/DataScienceAndBigDataAnalytics/src/branch/main/Codes/Code-B4%20%28Apache%20Scala%29%20-%20Alternatives.md).

---
