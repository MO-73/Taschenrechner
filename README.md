# Taschenrechner
Das Taschenrechner-Projekt ist ein einfaches PHP-Skript, das es Benutzern ermöglicht, grundlegende mathematische Operationen auszuführen, indem sie zwei Zahlen eingeben und einen Operator auswählen
<?php
// Überprüfen, ob das Formular abgesendet wurde
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // Variablen für die Eingaben
    $num1 = $_POST['num1'];
    $num2 = $_POST['num2'];
    $operator = $_POST['operator'];
    
    // Überprüfen, ob beide Zahlen eingegeben wurden
    if (!empty($num1) && !empty($num2)) {
        // Berechnung basierend auf dem ausgewählten Operator
        switch ($operator) {
            case '+':
                $result = $num1 + $num2;
                break;
            case '-':
                $result = $num1 - $num2;
                break;
            case '*':
                $result = $num1 * $num2;
                break;
            case '/':
                // Überprüfen, ob der Divisor nicht Null ist
                if ($num2 != 0) {
                    $result = $num1 / $num2;
                } else {
                    $result = "Division durch Null ist nicht erlaubt.";
                }
                break;
            default:
                $result = "Ungültiger Operator.";
        }
    } else {
        $result = "Bitte geben Sie beide Zahlen ein.";
    }
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Taschenrechner</title>
</head>
<body>
    <h1>Taschenrechner</h1>
    <form method="post">
        <input type="number" name="num1" placeholder="Erste Zahl" required><br><br>
        <input type="number" name="num2" placeholder="Zweite Zahl" required><br><br>
        <select name="operator">
            <option value="+" selected>Addition (+)</option>
            <option value="-">Subtraktion (-)</option>
            <option value="*">Multiplikation (*)</option>
            <option value="/">Division (/)</option>
        </select><br><br>
        <button type="submit">Berechnen</button>
    </form>
    <?php if(isset($result)): ?>
        <h2>Ergebnis:</h2>
        <p><?php echo $result; ?></p>
    <?php endif; ?>
</body>
</html>
