Ця програма реалізує класичну гру "Крестики-нолики" за допомогою консольного інтерфейсу. Гравці вводять свої ходи через координати рядка і стовпця, а гра перевіряє переможця після кожного ходу і визначає, чи є нічия.

Основні функції програми включають:
- `drawBoard`: Функція відображення ігрового поля у консолі.
- `checkWinner`: Функція перевірки переможця шляхом аналізу рядків, стовпців та діагоналей.
- `main`: Основна функція програми, в якій відбувається основний цикл гри. Гравці чергуються вводити свої ходи, і гра продовжується до тих пір, поки не буде виявлено переможця або досягнуто нічиєї.

Кожен гравець має позначення (X або O), і їхні ходи записуються на ігровій дошці. Якщо трійка однакових позначень з'являється в рядку, стовпці або діагоналі, гравець, що встановив ці позначення, перемагає. Якщо всі клітинки зайняті, а переможця немає, гра завершується нічиєю.

Ця програма написана на мові програмування C++ та може бути виконана у будь-якому середовищі, що підтримує компіляцію і виконання коду C++, такому як Visual Studio або будь-яке інше середовище розробки C++.
 ```
#include <iostream>
#include <vector>
using namespace std;

// Функція для відображення ігрової дошки
void drawBoard(const vector<vector<string>>& board)
{
    for (int row = 0; row < 3; ++row)
    {
        for (int col = 0; col < 3; ++col)
        {
            cout << board[row][col];
            if (col < 2) cout << " | ";
        }
        cout << endl;
        if (row < 2) cout << "---------" << endl;
    }
}

// Функція для перевірки переможця
string checkWinner(const vector<vector<string>>& board)
{
    // Перевірка рядків та стовпців
    for (int i = 0; i < 3; ++i)
    {
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2] && board[i][0] != " ")
            return board[i][0];
        if (board[0][i] == board[1][i] && board[1][i] == board[2][i] && board[0][i] != " ")
            return board[0][i];
    }
    // Перевірка діагоналей
    if (board[0][0] == board[1][1] && board[1][1] == board[2][2] && board[0][0] != " ")
        return board[0][0];
    if (board[0][2] == board[1][1] && board[1][1] == board[2][0] && board[0][2] != " ")
        return board[0][2];
    // Якщо переможця немає
    return "";
}

int main()
{
    vector<vector<string>> board(3, vector<string>(3, " "));
    string currentPlayer = "X";

    while (true)
    {
        drawBoard(board);

        // Отримання ходу гравця
        int row, col;
        cout << "Player " << currentPlayer << ", enter your move (row and column): ";
        cin >> row >> col;

        // Валідація введення
        if (row < 0 || row >= 3 || col < 0 || col >= 3 || board[row][col] != " ") {
            cout << "Invalid move. Please try again." << endl;
            continue;
        }

        // Оновлення дошки ходом гравця
        board[row][col] = currentPlayer;

        // Перевірка переможця
        string winner = checkWinner(board);
        if (winner != "")
        {
            drawBoard(board);
            cout << "Player " << winner << " wins!" << endl;
            break;
        }

        // Перевірка нічии
        bool isDraw = true;
        for (const auto& row : board) {
            for (const auto& cell : row) {
                if (cell == " ")
                {
                    isDraw = false;
                    break;
                }
            }
        }
        if (isDraw)
        {
            drawBoard(board);
            cout << "It's a draw!" << endl;
            break;
        }

        // Зміна гравця
        currentPlayer = (currentPlayer == "X") ? "O" : "X";
    }

    return 0;
}
