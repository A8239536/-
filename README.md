# -
第六組五子棋
#ifndef ChessBoard_h
#define ChessBoard_h
const int n = 15;
int chessBoardInfor[n][n];
class ChessBoard {

public:
	ChessBoard();
	void initWindow();
	void drawChessBoard(int x, int y);
};
#endif // !Chessboard_h

#include"ChessBoard.h"
#include<Windows.h>
#include<iostream>
using namespace std;
ChessBoard::ChessBoard() {
	initWindow();
	drawChessBoard(n / 2, n / 2);
}
void ChessBoard::initWindow() {
	SetConsoleTitleA("五子棋"); 
	system("color E0");
	system("mode con cols=51 lines=18");
}
void ChessBoard::drawChessBoard(int x, int y) {
	system("cls");
	for (int i = 0;i < n;i++)
	{
		for (int j = 0;j < n;j++)
		{
			if (chessBoardInfor[i][j] == 1)
				cout << " ●";
			else if (chessBoardInfor[i][j] == 2)
				cout << " ○";
			else if (i == x && j == y)
				cout << " ╬ ";
			else if (i == 0 && j == 0)
				cout << " ┏ ";
			else if (i == 0 && j == n - 1)
				cout << " ┓ ";
			else if (i == n - 1 && j == 0)
				cout << " ┗ ";
			else if (i == n - 1 && j == n - 1)
				cout << " ┛ " << endl;
			else if (i == 0)
				cout << " ┳ ";
			else if (i == n - 1)
				cout << " ┻ ";
			else if (j == 0)
				cout << " ┣ ";
			else if (j == n - 1)
				cout << " ┫ ";
			else
				cout << " ┼ ";
		}
		cout << "\n";
	}
}
	
	
	
#ifndef ChessGame_h
#define ChessGame_h
class ChessGame {
public:
	ChessGame();
	void init();
	void play();
	int put();
	int judge(int x, int y);
	int g_x, g_y;
	int g_current;
};
#endif // !ChessGame_h

	
#include"ChessGame.h"
#include"ChessBoard.h"
#include<Windows.h>
#include<conio.h>
ChessGame::ChessGame() {
	init();
}
void ChessGame::init() {
	memset(chessBoardInfor, 0, sizeof(chessBoardInfor));
	g_x = n / 2;
	g_y = n / 2;
	g_current = 1;
}
void ChessGame::play() {
	int p = 0;
	while (1)
	{
		ChessBoard().drawChessBoard(g_x, g_y);
		if (p > 0)
		{
			if (p == 1)
				MessageBox(GetForegroundWindow(), "黑棋獲勝", "五子棋", 1);
			else
				MessageBox(GetForegroundWindow(), "白棋獲勝", "五子棋", 1);
			break;
		}

		char input = getch();
		switch (input)
		{
		case 32:
			if (1 == put())
			{
				if (judge(g_x, g_y) == 0)
					g_current = 3 - g_current;
				else
					p = judge(g_x, g_y);
			}
			break;
		case 72:
			g_x--;if (g_x < 0) g_x = n - 1;
			break;
		case 80:
			g_x++;if (g_x > n - 1) g_x = 0;
			break;
		case 75:
			g_y--;if (g_y < 0) g_y = n - 1;
			break;
		case 77:
			g_y++;if (g_y > n - 1) g_y = 0;
			break;
		}
	}
}
int ChessGame::put() {
	if (chessBoardInfor[g_x][g_y] == 0)
	{
		chessBoardInfor[g_x][g_y] = g_current;
		return 1;
	}
	else
		return 0;
}
int ChessGame::judge(int x, int y) {
	int t = 0;
	for (int i = 1;i < 5;i++)
	{
		if (x - i > -1)
		{
			if (chessBoardInfor[x - i][y] == chessBoardInfor[x][y])
				t++;
			else
				break;
		}
		else
			break;
	}
	for (int i = 1;i < 5;i++)
	{
		if (x + i < n)
		{
			if (chessBoardInfor[x + i][y] == chessBoardInfor[x][y])
				t++;
			else
				break;
		}
		else
			break;
	}
	if (t > 3)return chessBoardInfor[x][y];
	t = 0;
	for (int i = 1;i < 5;i++)
	{
		if (y - i > -1)
		{
			if (chessBoardInfor[x][y - i] == chessBoardInfor[x][y])
				t++;
			else
				break;
		}
		else
			break;
	}
	for (int i = 1;i < 5;i++)
	{
		if (y + i < n)
		{
			if (chessBoardInfor[x][y + i] == chessBoardInfor[x][y])
				t++;
			else
				break;
		}
		else
			break;
	}
	if (t > 3)return chessBoardInfor[x][y];
	t = 0;
	for (int i = 1;i < 5;i++)
	{
		if (y - i > -1 && x - i > -1)
		{
			if (chessBoardInfor[x - i][y - i] == chessBoardInfor[x][y])
				t++;
			else
				break;
		}
		else
			break;
	}
	for (int i = 1;i < 5;i++)
	{
		if (x + i < n && y + i < n)
		{
			if (chessBoardInfor[x + i][y + i] == chessBoardInfor[x][y])
				t++;
			else
				break;
		}
		else
			break;
	}
	if (t > 3)return chessBoardInfor[x][y];
	t = 0;
	for (int i = 1;i < 5;i++)
	{
		if (y - i > -1 && x + i < n)
		{
			if (chessBoardInfor[x + i][y - i] == chessBoardInfor[x][y])
				t++;
			else
				break;
		}
		else
			break;
	}
	for (int i = 1;i < 5;i++)
	{
		if (x - i > -1 && y + i < n)
		{
			if (chessBoardInfor[x - i][y + i] == chessBoardInfor[x][y])
				t++;
			else
				break;
		}
		else
			break;
	}
	if (t > 3)
		return chessBoardInfor[x][y];
	else
		return 0;
}
	
	
#include<iostream>
#include"ChessBoard.h"
#include"ChessGame.h"
using namespace std;
int main() {
	ChessGame game;
	game.play();
	return 0;
}
