# vaGocalculator
```go
package main

import (
    "fmt"
    "strings"
    "strconv"
)

func isRomanNumeral(s string) bool {
    romanNumerals := []string{"I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX", "X"}
    for _, rn := range romanNumerals {
        if rn == s {
            return true
        }
    }
    return false
}

func romanToArabic(roman string) int {
    romanDict := map[string]int{
        "I": 1, "II": 2, "III": 3, "IV": 4, "V": 5,
        "VI": 6, "VII": 7, "VIII": 8, "IX": 9, "X": 10,
    }
    return romanDict[roman]
}

func arabicToRoman(arabic int) string {
    romanDict := map[int]string{
        1: "I", 2: "II", 3: "III", 4: "IV", 5: "V",
        6: "VI", 7: "VII", 8: "VIII", 9: "IX", 10: "X",
    }
    return romanDict[arabic]
}

func calculate(expression string) {
    parts := strings.Fields(expression)
    if len(parts) != 3 {
        fmt.Println("Ошибка: Неверный формат операции.")
        return
    }

    a, operator, b := parts[0], parts[1], parts[2]

    aIsNumeric := false
    bIsNumeric := false

    aInt, aErr := strconv.Atoi(a)
    bInt, bErr := strconv.Atoi(b)

    if aErr == nil {
        aIsNumeric = true
    }

    if bErr == nil {
        bIsNumeric = true
    }

    if (aIsNumeric && bIsNumeric) || (isRomanNumeral(a) && isRomanNumeral(b)) {
        if aIsNumeric && bIsNumeric {
            aInt, _ = strconv.Atoi(a)
            bInt, _ = strconv.Atoi(b)
        } else {
            aInt = romanToArabic(a)
            bInt = romanToArabic(b)
        }

        switch operator {
        case "+":
            result := aInt + bInt
            if isRomanNumeral(a) && isRomanNumeral(b) {
                fmt.Println(arabicToRoman(result))
            } else {
                fmt.Println(result)
            }
        case "-":
            result := aInt - bInt
            if isRomanNumeral(a) && isRomanNumeral(b) {
                fmt.Println(arabicToRoman(result))
            } else {
                fmt.Println(result)
            }
        case "*":
            result := aInt * bInt
            if isRomanNumeral(a) && isRomanNumeral(b) {
                fmt.Println(arabicToRoman(result))
            } else {
                fmt.Println(result)
            }
        case "/":
            if bInt == 0 {
                fmt.Println("Ошибка: Деление на ноль.")
                return
            }
            result := aInt / bInt
            fmt.Println(result)
        default:
            fmt.Println("Ошибка: Неверный оператор.")
        }
    } else {
        fmt.Println("Ошибка: Используются разные системы счисления.")
    }
}

func main() {
    for {
        fmt.Print("Введите арифметическую операцию (например, 'I + II' или '3 * 5'): ")
        var userInput string
        fmt.Scanln(&userInput)
        if userInput == "exit" {
            break
        }
        calculate(userInput)
    }
}
```
